# Journal des interventions — ZuluTek Android

## 2026-11-22 — Reprise de l'audit fonctionnel et sécurisation du moteur Android

### Objet

Poursuite de la remise en état de l'APK Android ZuluTek à la suite des retours utilisateur : écran LCD blanc, sortie audio limitée à un clic, clavier et commandes de synthèse jugés inopérants ou instables, problèmes de séquenceur et de boîte à rythmes.

Cette intervention s'inscrit dans la chaîne de PR empilées :
- [PR #44 — Fix APK touch circuit bend (REC + LCD)](https://github.com/FlyingZulu/FZuluTek/pull/44)
- [PR #45 — Harden Android USB audio and ZuluLink handling](https://github.com/FlyingZulu/FZuluTek/pull/45)
- [PR #46 — Serialize Android DSP state across JNI and Oboe](https://github.com/FlyingZulu/FZuluTek/pull/46)

La PR #46 est ouverte, basée sur `fix/apk-audio-network-transport` (PR #45). À la dernière vérification de cette entrée, son head est `c9e0232fef23572ee5346691d952213c60fbdd50`, et GitHub la signale comme mergeable. Elle n'est pas fusionnée.

### Périmètre autorisé et interdictions

- Autorisation explicite de corriger le code Kotlin de l'APK et son moteur natif Android C/C++.
- **Interdiction absolue de modifier le firmware FM-1, ses patches, ses sources embarquées ou d'autres projets sans autorisation distincte.**
- Ne pas transposer automatiquement les compromis matériels ECO du FM-1 à l'APK Android. L'application Android peut conserver davantage de ressources DSP.
- Ne pas considérer « SCL » comme un défaut : l'utilisateur a précisé que c'était une faute de frappe pour SEL.
- Toute évolution de commande doit respecter les contrôles et encodeurs tels que décrits dans la documentation du projet.

### Faits et corrections apportés dans la chaîne de travail

#### PR #44 — tactile REC / LCD
- Correction ciblée du geste de circuit-bend tactile lorsque REC est maintenu et que le LCD est touché.
- L'utilisateur a confirmé que le comportement REC / LCD touch bend est OK.
- PR ouverte/non fusionnée au moment de ce journal.

#### PR #45 — transport USB et ZuluLink
- Correction de l'encapsulation des messages USB-MIDI au format d'événements de 4 octets.
- Renforcement du nettoyage du périphérique/interface USB, des permissions et du cycle de vie AudioRecord.
- Validation d'en-tête et appariement des pairs ZuluLink renforcés.
- Documentation de passation ajoutée.
- Point d'architecture important : ZuluLink transporte du contrôle/tempo/commandes sur UDP, pas un flux audio.
- Le chemin USB Audio Class PCM via AudioRecord/AudioTrack ne constitue pas à lui seul un pont complet vers le sampler natif. Aucun mécanisme public d'injection PCM dans le sampler natif n'a été établi par cet audit.
- PR empilée sur PR #44 ; ne pas supposer qu'elle est fusionnée.

#### PR #46 — concurrence JNI / callback Oboe
- Ajout d'un verrou d'état natif partagé récursif pour sérialiser les appels JNI qui modifient ou consultent l'état du moteur.
- Le callback audio Oboe utilise un essai non bloquant (`try_lock`). Si le verrou est occupé, le callback rend un bloc silencieux en sortie ou abandonne le bloc d'entrée plutôt que d'attendre et bloquer le thread audio.
- `nativeStop` reste hors du verrou pour éviter un interblocage avec l'arrêt du flux audio.
- `nativeDestroy` arrête d'abord le flux Oboe, puis prend le verrou avant la destruction.
- Le verrouillage est une première sécurisation ; il peut entraîner des blocs audio perdus/silencieux en cas de contention. Une file de commandes lock-free ou une séparation stricte des états peut être préférable à terme, après mesure.
- Les modifications concernent le moteur natif de l'APK Android uniquement.

### Correction de commande importante : ALG

L'utilisateur a rappelé : **ALG est un encodeur rotatif**. La documentation de l'application décrit les sept contrôles comme SELECT / PRESET / ALGO / K1…K4 ; la rotation d'ALG sur MAIN règle la forme d'onde (AT_WAVE).

Une première implémentation avait incorrectement associé l'appui long d'ALG au changement de moteur. Cette interprétation était erronée et a été retirée de `MainActivity.kt`. La documentation de passation et le corps de la PR #46 ont été corrigés en conséquence.

Consigne durable : ne jamais utiliser l'appui long d'ALG comme sélecteur de moteur, et ne pas détourner sa rotation de la fonction de forme d'onde. Le changement de moteur doit rester sur les commandes prévues par le projet (notamment HOME / sélection de partie et le contrôle MIDI CC 80, selon le contexte).

### Cartographie des commandes à respecter

Constats tirés du code Android audité :
- Sur MAIN, les 16 touches blanches déclenchent les slots du looper ; elles ne sont donc pas toutes des touches de clavier mélodique.
- Les touches noires jouent des notes sur MAIN, sous réserve des fonctions spéciales et combinaisons prévues par la page.
- La page FX/SIREN donne accès au clavier chromatique complet.
- Ne pas conclure à une panne du moteur uniquement parce que les touches blanches de MAIN ne jouent pas des notes : vérifier d'abord le mapping de page et le comportement attendu.
- Les contrôles de transport, de séquenceur et de boîte à rythmes doivent être testés avec leur mapping propre ; ne pas réaffecter les encodeurs au hasard pour masquer une panne.

### Audit LCD et audio : état réel

Les fichiers `LcdView.kt`, `SurfaceView.kt`, `MainActivity.kt` et `ztek_engine.cpp` ont été relus.

- Le dessin du LCD contient bien une routine de rendu qui remplit le fond et compose l'image. Le code inspecté ne suffit pas à expliquer à lui seul le LCD blanc observé sur l'appareil. Le problème de layout, de dimensions, de superposition ou d'invalidation n'est donc **pas encore résolu ni isolé**.
- Le callback Oboe appelle le rendu DSP natif et écrit les échantillons dans le buffer de sortie. Cela ne prouve pas que les voix sont effectivement déclenchées, routées et mixées à un niveau audible.
- Les causes du « clic seulement » restent à isoler : déclenchement des notes, gate/enveloppes, sélection/routage des voix, gain/mixage, état de démarrage du moteur et interaction avec le callback audio.
- L'audit a également identifié que la capture USB PCM n'est pas actuellement reliée à une API d'injection dans le sampler natif. Ne pas présenter cette fonction comme opérationnelle.
- Aucun correctif LCD ni correctif définitif de rendu sonore n'est revendiqué dans cette entrée.

### Validation et limites

- Au dernier contrôle, le workflow GitHub associé au commit `c9e0232fef23572ee5346691d952213c60fbdd50` était encore **in_progress** : [workflow 44988417923](https://github.com/FlyingZulu/FZuluTek/actions/runs/44988417923). Ne pas le déclarer réussi sans relecture de son résultat final.
- Aucun APK construit à partir de ce head n'a été généré ou livré dans cette intervention.
- Aucun test physique sur téléphone Android ou FM-1 n'a été réalisé ici.
- La compilation, le son continu, la contention du callback, le mapping des commandes, le LCD, les séquenceurs et la boîte à rythmes restent à valider sur un appareil.
- L'APK précédemment disponible à partir de PR #45 ne contient pas les modifications ultérieures de PR #46 ; ne pas la distribuer comme build courant.

### Consignes pour les futurs agents

1. Lire ce journal, `AGENTS.md` à la racine de FZuluTek et `docs/ANDROID-AUDIO-NETWORK-HANDOFF.md` avant toute intervention.
2. Reprendre depuis le head courant de la PR #46 et vérifier l'état GitHub réel avant d'écrire. Ne pas supposer que les SHA mentionnés ici sont encore les plus récents.
3. Maintenir les changements Android dans le périmètre autorisé. Aucun changement dans le firmware, les patches FM-1 ou les autres dépôts sans autorisation explicite.
4. Respecter le mapping documenté des commandes physiques. En particulier, ALG est un encodeur rotatif et son appui long ne sélectionne pas le moteur.
5. Séparer les faits vérifiés, les hypothèses et les tests matériels. Ne jamais annoncer « corrigé » sur la seule base d'une lecture de code ou d'une compilation.
6. Pour le diagnostic audio, instrumenter et vérifier successivement : démarrage Oboe, fréquence/format/canaux, callbacks, déclenchement note/gate, sélection de voix, enveloppes, bus de mixage, gain final et écriture des buffers. Éviter de masquer une absence de son en augmentant arbitrairement le volume.
7. Pour le LCD blanc, vérifier les mesures réelles du composant, ses bornes, le parent/layout, l'ordre de dessin, le fond réellement affiché et les invalidations ; ajouter une trace visuelle temporaire seulement si elle permet d'isoler une hypothèse précise.
8. Pour les séquenceurs et la drum machine, suivre les événements de bout en bout (UI → Kotlin → JNI → moteur DSP → callback audio) avant de modifier le mapping.
9. Éviter les longues listes de tests manuels à l'utilisateur. Fournir d'abord un APK diagnostique réellement construit et demander une seule observation ciblée si nécessaire.
10. Après chaque intervention, mettre à jour ce journal avec la date, les fichiers touchés, les commits/PR, les vérifications réellement exécutées, leurs résultats et les points encore ouverts.

### Suite de travail recommandée

Priorité 1 : obtenir le résultat final du workflow du head courant et corriger toute erreur de compilation.

Priorité 2 : tracer la chaîne de déclenchement d'une note jusqu'au buffer Oboe et identifier pourquoi la sortie se limite à un clic.

Priorité 3 : isoler le LCD blanc par mesures/layout et test de dessin minimal, puis corriger uniquement la cause démontrée.

Priorité 4 : vérifier le mapping réel du clavier, des encodeurs, des séquenceurs et de la drum machine sans modifier les fonctions documentées.

Priorité 5 : générer un nouvel APK à partir d'un commit validé et consigner son SHA-256, le workflow et les limites de test.


## 2026-11-22 — Addendum : reprise effective de l'audit LCD / audio / clavier

### État de la branche au moment de la reprise
- PR [#46](https://github.com/FlyingZulu/FZuluTek/pull/46) toujours ouverte, non fusionnée, signalée mergeable par GitHub.
- Head observé : `c9e0232fef23572ee5346691d952213c60fbdd50` (11 commits, 6 fichiers modifiés).
- La description de PR renvoie désormais vers ce registre. Vérifier le head à nouveau avant toute écriture ultérieure.
- Les fichiers Android ont été lus depuis la branche `fix/android-native-audio-thread-safety`, et non depuis une APK locale ou une branche supposée.

### Faits techniques nouvellement confirmés
1. **Démarrage audio côté Kotlin :** `MainActivity.onCreate()` appelle `ZtekAudio.start()` mais ignore actuellement le booléen de retour. En cas d'échec de création/démarrage Oboe, l'interface poursuit son initialisation ; les méthodes de contrôle Kotlin deviennent ensuite des no-op si le handle vaut zéro. C'est une piste concrète pour le silence/clic, pas encore une cause prouvée. Une correction utile devra rendre l'échec visible et enregistrer l'état réel du flux, sans inventer un succès.
2. **État moteur initial :** après le démarrage, l'UI impose `setEngine(0)`, configure BPM, tonalité, échelle et paramètres de voix. Vérifier le résultat effectif du flux Oboe et les appels de note avant de conclure à un défaut DSP.
3. **LCD / superposition :** `rootLayout` est un `FrameLayout` avec fond sombre ; `SurfaceView` (qui est une View Android personnalisée, pas un `android.view.SurfaceView`) est ajoutée en premier, puis `LcdView` au-dessus. Le LCD est positionné ensuite par `placeLcdInBezel()`, déclenché par le layout et un `post`. Le fond de la fenêtre n'explique donc pas à lui seul un écran blanc ; contrôler dimensions, position effective, échelle/transformation et dessin de LcdView après layout.
4. **Rafraîchissement LCD :** le tick UI tourne toutes les 250 ms et appelle `lcd.invalidate()` (sauf throttling ECO). Ce mécanisme existe bien ; cela ne prouve pas que la vue a une taille/position non nulle ni que son `onDraw` est exécuté.
5. **Contrat clavier confirmé dans les sources :** la géométrie définit 16 touches blanches et 11 noires ; le hit-test traite les noires avant les blanches. Les commentaires de contrat indiquent les blanches comme slots du looper et les noires comme notes sur MAIN. Le clavier chromatique complet est prévu sur FX/SIREN. Ne pas requalifier les touches blanches de MAIN en notes sans vérifier la bible.
6. **ALG confirmé :** encodeur rotatif de forme d'onde sur MAIN. La mauvaise association long-press → changement de moteur est supprimée. Ne pas la réintroduire.

### Fichiers et zones relus
- `MainActivity.kt` : `onCreate`, démarrage moteur, création/ajout des vues, positionnement du LCD, tick de rafraîchissement et lifecycle `onDestroy`.
- `LcdView.kt` : structure `LcdState`, dimensions logiques 240×240 et commentaires du contrat de rendu RGB565.
- `SurfaceView.kt` : géométrie du clavier, zones de hit-test et gestion des touches longues.
- `ZtekAudio.kt` : façade JNI, handle nul en cas d'absence de moteur, `start()`, `noteOn/noteOff` et paramètres.
- `ztek_engine.cpp` : structure d'état DSP et callback Oboe avec verrou non bloquant déjà ajouté par PR #46.

### Modifications effectuées dans cette addendum
- Aucune modification de code n'est revendiquée dans cette étape de reprise.
- Cette entrée consigne les constats et pistes à vérifier avant de changer le comportement.
- Aucun firmware, patch embarqué ni autre projet n'a été modifié.

### Prochaines opérations, ordre de preuve
1. Examiner `placeLcdInBezel()`, le `onSizeChanged/onDraw` complet du LCD et les paramètres de layout mesurés. Si possible, ajouter une trace de diagnostic temporaire dans l'APK pour relever largeur/hauteur/position et nombre de dessins.
2. Rendre le statut de `ZtekAudio.start()` observable dans l'UI/logcat, puis vérifier que le callback Oboe est effectivement appelé avec un format/fréquence/canaux cohérents.
3. Suivre une seule note : événement tactile → `SurfaceListener` → `ZtekAudio.noteOn/noteOff` → JNI → état de voix/gate → rendu → buffer Oboe. Relever aussi le niveau crête avant/après mix/master.
4. Suivre PLAY/STOP et un step de séquenceur sur la même chaîne ; ne pas corriger simultanément clavier, séquenceur et moteur.
5. Après chaque changement, construire une APK depuis le head mis à jour via CI, consigner le workflow et le SHA-256 de l'artefact. Aucune validation matérielle ne peut être revendiquée sans test sur appareil.

### Rappel de méthode
Chaque nouvelle entrée doit distinguer explicitement : **observation**, **hypothèse**, **modification commitée**, **test exécuté**, **résultat** et **reste à faire**. Le silence du moteur, l'écran blanc et les commandes non fonctionnelles restent des symptômes rapportés par l'utilisateur tant qu'une reproduction instrumentée n'a pas identifié leur cause.


## 2026-11-22 — Correctif : note-off garanti après appui long sur touche blanche

### Symptôme / analyse
Le chemin tactile des touches blanches dans `SurfaceView.onTouchEvent()` émettait un événement DOWN immédiat, puis un événement long après 500 ms. Le callback long remettait `longPosted` à `false`. Au relâchement, l'événement UP était conditionné par `if (longPosted)` : il était donc supprimé dès que l'appui long avait été déclenché.

Ce défaut pouvait laisser une note blanche tenue sur la page SIREN ou laisser sans OFF une note déclenchée via LINK. Il pouvait aussi interrompre les actions momentanées dépendant du relâchement. C'est une cause concrète pouvant expliquer une partie des comportements clavier signalés ; elle n'explique pas à elle seule les autres pannes.

### Modification commitée
- Fichier : `app-zulutek/src/main/java/com/zulutek/preview/SurfaceView.kt`
- Commit code : `3828c3b5fb4985811dd6c1c8aaea7c5ee9d1a873`
- Changement : le relâchement blanc est toujours envoyé sur `ACTION_UP/ACTION_CANCEL`, même si le callback long s'est exécuté.
- Le callback long et le mapping des touches restent inchangés.
- Documentation de passation mise à jour dans `docs/ANDROID-AUDIO-NETWORK-HANDOFF.md`, commit `886d8635fc51002e10acfca70e8a2022adb5390c`.

### État PR
- PR [#46](https://github.com/FlyingZulu/FZuluTek/pull/46), branche `fix/android-native-audio-thread-safety`.
- Head constaté après les commits ci-dessus : `886d8635fc51002e10acfca70e8a2022adb5390c`.
- PR ouverte, non fusionnée ; mergeable : `false`.

### Validation
- Lecture du flux tactile et vérification statique de la condition de relâchement effectuées.
- Aucun build APK/CI ni test physique sur appareil n'est encore revendiqué.
- Test ciblé à réaliser sur prochain APK : appui bref et appui long (>500 ms) en SIREN, puis vérification du note-off au relâchement ; répéter en LINK pour vérifier l'envoi OFF ; vérifier que l'enregistrement long du looper reste fonctionnel.

### À poursuivre
Le correctif ne résout pas le LCD blanc, le son limité à un clic, les moteurs de synthèse, le transport Play/Stop, les séquenceurs ni la boîte à rythmes. Continuer l'instrumentation par chaîne (UI → Kotlin → JNI → DSP → Oboe), en commençant par rendre observable le résultat de `ZtekAudio.start()` et le callback de sortie. Respecter strictement l'interdiction de toucher au firmware FM-1 et aux patches.
