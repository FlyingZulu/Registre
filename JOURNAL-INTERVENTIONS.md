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


## 2026-11-22 — Mise à jour de passation après audit du démarrage audio

### Documentation Android
- Mise à jour de `docs/ANDROID-AUDIO-NETWORK-HANDOFF.md` pour indiquer la vraie branche de travail `fix/android-native-audio-thread-safety`.
- Ajout du constat que `MainActivity.onCreate()` ignore le retour booléen de `ZtekAudio.start()`. Si Oboe ne démarre pas, l'UI poursuit son initialisation alors que le handle audio peut rester nul. C'est une piste d'observabilité, pas une cause prouvée du clic seul.
- Ajout du cycle de vie des touches blanches et du correctif UP/CANCEL après appui long.
- Commit documentation : `16157d85c8f4513212a122cd70c1389a73b0db88`.

### Inspection DSP supplémentaire
- `ztek_create()` initialise la voix ATEK303, le bus de voix, les tranches de mixage à 0,8 et le master à 0,8 ; le routage de voix vers FX est initialisé.
- `ztek_note_on()` route vers `at_gate()` pour le moteur 0, ou `bass_gate()` pour les moteurs 1..4 ; le rendu choisit `at_render()` ou `bass_render()` selon le moteur.
- Ces chemins existent dans le code, mais ne prouvent ni que le callback Oboe tourne réellement sur l'appareil, ni que le signal produit est audible. Il reste à instrumenter le callback et les crêtes DSP/bus/master.
- `ztek_start()` tente le mode Oboe exclusif puis partagé, à 48 kHz float stéréo. L'état réel du flux et le résultat du callback ne sont pas encore exposés à l'UI.

### État PR et validations
- PR [#46](https://github.com/FlyingZulu/FZuluTek/pull/46) reste ouverte et non fusionnée.
- Head vérifié : `16157d85c8f4513212a122cd70c1389a73b0db88`; mergeable selon GitHub : `false`.
- Le connecteur n'a retourné aucun workflow CI associé aux derniers commits. Aucun APK récent ne doit être présenté comme construit ou testé.
- Aucune validation physique Android/FM-1 n'a été réalisée dans cette étape.

### Priorité suivante
Ajouter une instrumentation diagnostique minimale et peu intrusive : résultat du démarrage Oboe, état/fréquence/format/canaux du flux, compteur de callbacks et crête de sortie. Afficher un avertissement clair si le démarrage échoue. Ensuite seulement, construire l'APK via CI et suivre une note de l'événement tactile jusqu'au buffer de sortie. Ne pas augmenter les gains ni modifier le mapping à l'aveugle.


## 2026-11-22 — Clavier APK : touches blanches et noires roses

### Demande
L'utilisateur demande que les touches du clavier de l'APK soient blanches et que les touches noires soient roses.

### Modification effectuée
- Fichier : `app-zulutek/src/main/java/com/zulutek/preview/SurfaceView.kt`.
- Commit palette : `f88d38a69bf5a846aefb2270db913f77b8ac7cd8`.
- Touches blanches : dégradé ivoire clair `#FFFEFC → #E4E0E5`.
- Touches noires : dégradé rose `#FF8BC8 → #D92B83`.
- Palette dédiée, indépendante du skin DA ZULU / MAISON : les couleurs du clavier restent donc blanc/rose même si l'utilisateur change de skin.
- Les états actifs gardent le mélange ambre existant.
- Aucun changement de géométrie, hit-test, notes, slots looper, glissando, ni événements tactiles.

### Documentation
- `docs/ANDROID-AUDIO-NETWORK-HANDOFF.md` complété avec les couleurs, le périmètre et les limites de validation.
- Commit documentation : `67e52a4ffb8f80f705993f9a90a155c9b6fe9151`.

### Build et état de PR
- Le push du commit code a déclenché GitHub Actions « Build APK », run [44988931691](https://github.com/FlyingZulu/FZuluTek/actions/runs/44988931691), run #337. Au dernier relevé, statut `in_progress` ; ne pas annoncer de build réussi ni distribuer d'APK avant vérification de la conclusion et de l'artefact.
- PR [#46](https://github.com/FlyingZulu/FZuluTek/pull/46) : ouverte, non fusionnée. Head incluant la documentation : `67e52a4ffb8f80f705993f9a90a155c9b6fe9151`.
- Pas de test visuel sur appareil pour l'instant. À vérifier après build : rendu blanc/rose sous les deux skins, visibilité des états ambre, zones tactiles inchangées et absence de régression des touches/looper.

### Suite de mission
Le travail global continue : écran LCD blanc, audio qui ne produit qu'un clic, moteurs synthé, transport, séquenceurs et boîte à rythmes restent à diagnostiquer. Priorité de preuve : rendre observable le démarrage Oboe et son callback, puis suivre une note jusqu'au buffer de sortie. Ne pas retoucher au firmware FM-1 ni aux patches embarqués.


## APK Android — rendre l'échec de démarrage audio visible (2026-11-22)

- Constat : `MainActivity.onCreate()` ignorait le booléen de `ZtekAudio.start()`. Si `nativeCreate()` ou `nativeStart()` échouait, l'interface s'initialisait malgré un handle audio nul ; les commandes de synthèse devenaient alors silencieusement inopérantes.
- Correction : journal `ZuluTekAudio` au succès/échec et Toast explicite en cas d'échec. Pas de modification du DSP, du gain, du routage, du mapping tactile ni du firmware.
- Commit code : `8ca0aaf54911a9bfe616823ffa2882e3046fe88b`.
- Commit documentation : 7239becdf6eb03ee042e5c03b03c2c9951432ff0.
- Validation : inspection statique uniquement pour ce changement. Le run CI #337 (`44988931691`) est SUCCESS mais porte le commit antérieur `f88d38a69bf5a846aefb2270db913f77b8ac7cd8` ; il ne valide donc pas cette nouvelle modification. Build et test appareil restent à faire.
- Suite : compiler le nouveau head, observer Logcat tag `ZuluTekAudio`, puis mesurer les callbacks Oboe et le niveau crête si le flux démarre.


## APK Android — instrumentation du LCD blanc (2026-11-22)

- L'inspection statique trouve un fond noir explicite dans `LcdView.onDraw()` et un blit du framebuffer RGB565 ; `MainActivity` place le LCD selon `surface.lcdRect()`. Aucune cause certaine du LCD blanc n'est établie.
- Instrumentation `ZuluTekLCD` : taille de la vue, premier dessin, visibilité, échelle et placement calculé par SurfaceView. Aucun changement du rendu ni de la géométrie.
- Commits : placement `7b34b62f5dfbba303b6780597c5fe18883e0e80a` ; taille/dessin `a4f3fa0d40528903e75204b6cc4b5c8c6bf39053` ; documentation 41cd8689ffe3718f9cded10340990e25e7f60ecf.
- CI #342 lancé sur le head `a4f3fa0d40528903e75204b6cc4b5c8c6bf39053` ; résultat pas encore connu. Aucun test appareil.
- Étape suivante : sur téléphone, filtrer Logcat `ZuluTekLCD` et comparer tailles/placement/trace du premier dessin. Ne pas modifier le moteur graphique avant ces observations.



## APK Android — audit sélection moteur synthé (2026-11-22)

- Constat : `HOME` court alterne les parties et sélectionne localement LEAD/engine 0 et BASSE/engine 1. Les moteurs 2 FM, 3 SUB et 4 8BIT ne sont pas sélectionnables par un contrôle tactile local identifié dans `MainActivity.kt`.
- Le seul sélecteur 0..4 observé est le MIDI CC 80 entrant via ZuluLink. Le setter natif `ztek_set_engine()` accepte bien `0..4` : la lacune est côté interface locale.
- Aucun mapping modifié : ALG reste l'encodeur waveform, HOME long reste LINK. Un contrôle local doit être choisi avant d'altérer les commandes tactiles.
- Lecture statique uniquement, aucun test appareil. Détail consigné dans le handoff Android.


## Suivi CI / PR après consolidation (2026-11-22)

- Head actuel de la PR #46 : `577fee2fd3961a2af4e236e7e15c1fced56dd33d` (code diagnostic audio + traces LCD + audit moteur + handoff).
- Run #343 (`44989374629`) sur le head `41cd8689ffe3718f9cded10340990e25e7f60ecf` et run #344 (`44989463361`) sur le head courant sont tous deux indiqués `in_progress` lors du dernier contrôle ; aucun artefact associé n'est encore publié.
- PR #46 reste ouverte et non fusionnée. Les PR #44 et #45 restent également ouvertes (chaînage de branches). Ne pas fusionner isolément une PR empilée sans vérifier la séquence et la base.


## Résultat build APK diagnostic (2026-11-22)

- Run #343 (`44989374629`) : `success` ; compilation et publication des APK réussies.
- Artefact `zulu-apk-343` (6 315 769 octets), SHA-256 `8a5c30f1f9a9c6c89af0766495d240eb96a0208f5993337ff961c0584f405663`.
- Cet artefact correspond au head `a4f3fa0d40528903e75204b6cc4b5c8c6bf39053` et contient les changements de code diagnostic audio + instrumentation LCD. Le head actuel `577fee2fd3961a2af4e236e7e15c1fced56dd33d` ajoute seulement la documentation de l'audit moteur et le suivi du registre depuis ce code ; run #344 vérifie le head courant.
- Le build réussi ne prouve pas le comportement sur appareil. Pas de test Android réel effectué.


## APK Android — ajout du sélecteur local de moteur (2026-11-22)

- Lacune confirmée : auparavant HOME court n'exposait que LEAD/engine 0 et BASSE/engine 1 ; moteurs 2 FM, 3 SUB et 4 8BIT disponibles seulement via CC80 externe.
- Ajout d'une ligne `ENGINE` dans OPTIONS (page 16) : SEL sélectionne la ligne, ALG règle 0..4 ; valeurs ATEK303 / PLUK / FM / SUB / 8BIT.
- Changement immédiat par `ZtekAudio.setEngine()`, valeur affichée sur LCD et persistée (`SharedPreferences engine`). CC80 synchronise également préférence et partie affichée.
- Mapping principal préservé : ALG reste waveform sur MAIN ; HOME court conserve BASSE/LEAD/DRUMS/LOOP ; HOME long reste LINK.
- Commits : MainActivity `c157c75a6f17ff010b64829b5048d77d0879f55c` ; LcdView `69729922105169b115dfcb4739cfb29a543f81ad` ; bible `${ds.result.commit_sha}` ; handoff `${hs.result.commit_sha}`.
- Validation statique uniquement ; build CI du nouveau head et test tactile réel à faire.


## Suivi build après ajout du sélecteur moteur (2026-11-22)

- Head PR #46 : `5f44914f6800d564d1a82e5f1c1fc6e0cb258540`.
- Build #348 / run `44989679449` déclenché pour ce head ; statut `in_progress` au dernier contrôle.
- L'artefact `zulu-apk-343` (run #343) ne contient PAS le sélecteur local des moteurs ; ne pas le présenter comme APK final. Attendre l'artefact du run #348 ou d'un build ultérieur sur le head courant.


## APK ZuluTek — réglage VHS indépendant de ECO (2026-11-22)

- Inspection : les scanlines du LCD étaient dessinées uniquement si `!ecoOn` ; le mode ECO supprimait donc involontairement l’effet VHS.
- Réparation : nouvelle ligne VHS dans OPTIONS (SEL pour sélectionner, ALG pour ON/OFF), activée par défaut pour préserver le rendu antérieur et persistée sous la clé SharedPreferences `vhs`.
- ECO est désormais indépendant : il conserve son rôle de throttling/gestion des animations ; l’effet VHS dépend exclusivement de `st.vhsOn`.
- Shift court sur VHS et reset global restaurent VHS=ON. Aucun changement au firmware, à la palette du clavier, aux zones tactiles ou au moteur audio.
- Commits code : LcdView `81352ba2c67949e42fb9e871a8d84f46105cf4d5`, MainActivity `ab3305b035152e0c3dbc696740a1ab07303d5c87`. Documentation : bible eee336a386a04cd867d8245e1b7925a71f767ad8, handoff c9e2756c3139452aee91f7bfab810edb84c07ebf.
- Validation : inspection statique uniquement ; build CI et essai sur appareil non encore réalisés. Cette intervention ne prétend pas résoudre les autres symptômes signalés (LCD blanc, couleurs du clavier, son limité au clic, fiabilité générale des contrôles).

- Revue complémentaire : correction de la borne de sélection visuelle OPTIONS (0..6) pour rendre VHS sélectionnable, commit `fe0838d47d65ce86a868dc39d52730720a2d014d` ; handoff complété : 497c4cf976bd3c33aa989eea40c92c99153656c2.

- Revue du pipeline LCD : les retours anticipés de nombreuses pages évitaient l’ancien overlay VHS placé en fin de `onDraw()`. Déplacement de l’overlay dans `blitTo()` pour couvrir toutes les pages LCD, commit `0297db2a17e8b729e8d81c1bd35dce78caa7312f` ; handoff `04bf3820422a77fd7df1e5c94507ec28379310a2`. Validation statique uniquement, build et appareil en attente.

- Audit clavier APK : les constantes ivoire (`#FFFFFEFC`→`#FFE4E0E5`) et rose (`#FFFF8BC8`→`#FFD92B83`) sont effectivement consommées par les boucles de dessin des touches ; seul l’état actif les mélange vers l’ambre. Aucune substitution DA ZULU/MAISON identifiée. La teinte turquoise signalée n’est pas expliquée par le code inspecté : vérification sur APK et appareil/capture nécessaire. Pas de changement clavier non justifié. Handoff : 16a5ea4551bc1db4faa7ae7a3162a488a4e5047f.

- Audit tactile LCD : `lcd.setOnTouchListener` ne traite que BEND (REC+touch), PATCH et XY ; les autres gestes sont consommés sans sélection/édition générique des paramètres MAIN/pages. Ce manque est documenté dans le handoff 7f1558c7b3c3dfad38af4b9e1d272596538b03b9. Pas de mapping générique ajouté tant que chaque paramètre n’a pas été relié à son encodeur et à son setter natif ; préserver les zones BEND/PATCH/XY.


## 2026-11-22 — VHS subtil, aléatoire et réactif aux modulations (APK)
- Demande confirmée : scanlines « traits fins », rendu subtil ; artefacts randomisés et réactifs aux LFO/tools.
- `LcdView.kt` : trame fine à faible opacité (pas logique de 3 px), faible jitter, micro-artefacts horizontaux rares (1–2 segments courts) régénérés à intervalles pseudo-aléatoires ; intensité/fréquence légèrement influencées par l’activité moyenne des sources de modulation. Overlay conservé dans `blitTo()`, donc limité à l’affichage LCD.
- `MainActivity.kt` : échantillonnage des 16 sources via `ZtekAudio.srcVal` toutes les 250 ms côté thread UI lorsque VHS est activé ; aucun traitement dans le callback audio. LFO non activés automatiquement. VHS OFF désactive l’overlay ; ECO indépendant.
- Commits : `f6365be209f855054d872c3a7fed4cc17436e0b9` (rendu), `1e6038b54f516f0296d4748c7d88b923b0e78feb` (lecture des sources), documentation ci-jointe.
- Validation au moment de la note : modifications enregistrées sur la branche PR #46 ; CI et test sur appareil à confirmer. Pas de modification firmware FM-1.


## 2026-11-22 — Validation CI et micro-déplacement VHS (APK)

- Build #360 / run `44992055595` : terminé avec succès pour le commit code `1e6038b54f516f0296d4748c7d88b923b0e78feb`; étapes de compilation et publication APK réussies ; artefact `zulu-apk-360` disponible (6 317 258 octets). L'étape Release APK dédiée a été ignorée par le workflow ; il s'agit de l'artefact CI de test.
- Build #361 / run `44992074995` : terminé avec succès pour le head documentation `f60a5172650d8ac93d8381b8d68067ec40052acf`.
- Amélioration après revue : ajout d'un vrai micro-déplacement horizontal aléatoire d'une tranche de 1–2 lignes LCD, limité à un pixel logique et déclenché rarement ; la probabilité augmente légèrement avec la modulation. Il s'agit d'un redraw de la tranche, uniquement dans le rendu LCD, sans toucher au framebuffer audio ni au callback audio. Commit LcdView `fead29cd20935683454a553b2c020beba59bf28c`.
- Nettoyage MainActivity : suppression de la seconde lecture redondante des 16 sources lorsque VHS est activé ; lecture de secours conservée sur pages 6..10 lorsque VHS est désactivé. Commit `96728ede72f0aed37d2ce51c2e05440a4c400f16`.
- Build #362 / run `44992316338` déclenché pour le commit LcdView ; statut `in_progress` au moment de cette note. Attendre sa réussite et vérifier l'artefact avant de valider le dernier micro-déplacement.
- PR #46 reste ouverte, non fusionnée, empilée sur PR #45. Aucun changement du firmware FM-1. Aucun essai sur appareil Android physique à ce stade.


## 2026-11-22 — Résultat build #362 et validation du head suivant

- Build #362 / run `44992316338` : **succès** sur `fead29cd20935683454a553b2c020beba59bf28c`. Compilation APK de test et publication réussies. Artefact `zulu-apk-362`, 6 317 504 octets, non expiré. L'étape Release APK dédiée est restée ignorée.
- Le build #362 ne contient pas le commit MainActivity `96728ede72f0aed37d2ce51c2e05440a4c400f16` (suppression du polling redondant). Le head de PR #46 a ensuite reçu une mise à jour documentaire `b2a83024807d204ae44f7f46e145837b64ad7c47` ; le build du head intégrant les deux derniers changements doit encore être vérifié.
- Handoff Android actualisé dans `docs/ANDROID-AUDIO-NETWORK-HANDOFF.md`.
- PR #46 reste ouverte et non fusionnée, empilée sur PR #45. Aucun firmware/patch embarqué FM-1 modifié. Aucun essai sur appareil Android physique.


## 2026-11-22 — Build #363 : head code complet validé

- Build #363 / run `44992319340` : **succès** sur le head code `96728ede72f0aed37d2ce51c2e05440a4c400f16`, qui comprend le micro-déplacement VHS et le nettoyage du polling MainActivity.
- Étapes « Construire les APK de test » et « Publier les APK » réussies ; artefact `zulu-apk-363`, 6 317 494 octets, non expiré.
- L'étape Release APK dédiée est ignorée (branche non-main) : artefact de build/debug CI, pas une release signée revendiquée.
- Build #364 / run `44992522444` en cours sur le commit documentaire `b2a83024807d204ae44f7f46e145837b64ad7c47`, lancé par push du handoff mis à jour. Son résultat reste à vérifier.
- Aucun test sur appareil Android physique ; rendu réel, latence audio, tactile et symptômes LCD blanc/clavier restent ouverts. PR #46 ouverte, non fusionnée, empilée sur PR #45. Firmware FM-1 inchangé.


## 2026-11-22 — Diagnostic LCD/audio et correction RGB565

- Build #365 / run `44992852556` : **succès**, commit `beb3be0767772b4b14bd56ca79b1a0e265e9c6d4`; artefact `zulu-apk-365`, 6 317 817 octets. Ajout de logs Oboe one-shot : premier callback (rate/canaux/format/device/burst), première contention du verrou, niveau de crête après déclenchement de note.
- Build #366 / run `44992855477` : **succès**, commit `9a1c46afc245d448669d60a7d1d24e7240ad3b7f`; artefact `zulu-apk-366`, 6 318 429 octets. Ajout du diagnostic du premier blit LCD : taille view/canvas, clip, échelle, offset et pixels non noirs.
- Revue de la conversion RGB565 : le masque rouge antérieur conservait 8 bits au lieu de 5. Correction dans LcdView, commit `7753fa2e9892f48f0971c9ec038e6542527fe54d`, alpha conservé et canaux quantifiés 5/6/5.
- Optimisation du diagnostic audio : le calcul de crête est maintenant déclenché une seule fois après une note, et non à chaque callback silencieux ; commit `cb384588d184118e899c62f2f6dce71a9152c927`.
- Builds #367 / run `44992903393` (RGB565) et #368 / run `44992946473` (head diagnostic audio optimisé) encore en cours au moment de la note.
- PR #46 ouverte/non fusionnée ; aucun firmware FM-1 modifié. Aucun essai matériel Android réalisé : ces logs attendent une capture Logcat sur appareil pour conclure sur les symptômes LCD blanc et audio clic seul.


## 2026-11-22 — Head diagnostic compilé et handoff synchronisé

- Build #368 / run `44992946473` : compilation APK de test et publication réussies sur `cb384588d184118e899c62f2f6dce71a9152c927` ; artefact `zulu-apk-368`, 6 318 292 octets, non expiré. Release dédiée ignorée sur branche PR.
- Le build #368 comprend les logs one-shot Oboe, le diagnostic premier blit LCD, la conversion RGB565 corrigée et le calcul de crête déclenché uniquement après note.
- Handoff mis à jour dans FZuluTek au commit `ac074c0dcb706a58f1bc5b1932e43505a4e0cfa2` ; un build documentaire supplémentaire est attendu.
- Build #367 sur le commit intermédiaire `7753fa2e9892f48f0971c9ec038e6542527fe54d` toujours en cours au dernier contrôle ; non bloquant puisque #368 valide un commit descendant incluant cette correction.
- Aucun test Android physique ; collecte Logcat requise pour conclure. PR #46 reste ouverte/non fusionnée ; aucune modification FM-1 firmware.


## 2026-11-22 — Complément CI

- Build #367 / run `44992903393` : **succès** sur le commit intermédiaire RGB565 `7753fa2e9892f48f0971c9ec038e6542527fe54d`. La correction est également incluse dans #368, qui valide le descendant complet.
- Build #369 / run `44993081445` : en cours sur le commit documentaire `ac074c0dcb706a58f1bc5b1932e43505a4e0cfa2` au dernier contrôle.


## 2026-11-22 — Build #369 : handoff documentaire validé

- Build #369 / run `44993081445` : **succès** sur le commit `ac074c0dcb706a58f1bc5b1932e43505a4e0cfa2`.
- Compilation et publication des APK de test réussies ; artefact `zulu-apk-369`, 6 318 368 octets, non expiré. L'étape Release APK dédiée est ignorée sur cette branche de PR : il s'agit d'un artefact debug CI, pas d'une release signée.
- Ce build valide le head documentaire/handoff après le build #368 qui avait déjà compilé le code complet de diagnostic LCD/audio et la correction RGB565.
- PR #46 reste ouverte et non fusionnée, basée sur PR #45. Aucun test physique Android n'a été réalisé ; les symptômes LCD blanc et audio limité à un clic restent à diagnostiquer avec Logcat sur appareil.
- Aucun firmware FM-1, patch embarqué ni autre projet modifié.
