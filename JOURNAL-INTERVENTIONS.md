# Journal des interventions — ZuluTek Android

## 2026-11-25 — Respect strict des règles Zulu

Seul Flying Zulu peut autoriser explicitement une dérogation aux règles des projets Zulu. Reprendre exactement le livrable demandé et vérifier la référence avant toute reproduction à l’identique. Toute variante ou substitution exige son accord. [Règle dans les Méthodes Zulu](https://github.com/FlyingZulu/Atelier-zulu/commit/9700e8df329400caa6bc694b48f53ebb8f890b1c)

## 2026-11-25 — Garage · Composition et mémoires de deck

Le tiroir étiqueté donne accès à un panneau que l’utilisateur peut épingler et placer. Le redimensionnement du panneau est souhaité. Quatre mémoires permettent de rappeler les dispositions d’essai. À terme, les decks des différents projets et les gestes éprouvés sur le banc pourront être repris dans Zulu Control. [Relais EAST/WEST](https://github.com/FlyingZulu/Atelier-zulu/blob/5f5f56fa6585210a32500c2aba67eae866823a22/projets/liaison-east-west.md#composer-et-rappeler-un-deck-dessai)

## 2026-11-25 — Garage · Usage final

**Décision de Flying Zulu.** Le Garage et son banc d’essai serviront à l’utilisateur pour tester, diagnostiquer et régler l’application ou le firmware de son instrument. [Méthodes Zulu](https://github.com/FlyingZulu/Atelier-zulu/blob/a2ae9c273b773eb611bcb2b812766311745ecdb0/methodes/README.md#5-garage--diagnostic-accessible-à-lutilisateur).

## 2026-11-25 — Garage · Éléments testés et outils du banc

**Décision de Flying Zulu.** Identifier les éléments internes au BLOK et les outils de test. Les organes voisins sont choisis selon la fonction testée, audio ou MIDI. Les organes simulés se raccordent aux ports avec des signaux et des routages comparables à l’instrument final, pour éprouver chaque brique, Lego ou BLOK isolément. [Carte du circuit](https://github.com/FlyingZulu/Atelier-zulu/blob/a64435898025367ef89e7bedfa97a425745ad79b/projets/carte-circuit-garage.md#éléments-testés-et-outils-du-banc).

## 2026-11-25 — Garage · Plans de vue du deck

**Décision de Flying Zulu.** Cadenas fermé, le deck reste fixe devant. Les tiroirs hors deck défilent derrière, dans l’ordre du signal. Décision de conception consignée. Le comportement reste à vérifier sur le Redmi. [Référence Garage](https://github.com/FlyingZulu/Atelier-zulu/blob/a879aa67df872726e52aeb15c5714685e8ac7d9d/projets/liaison-east-west.md#plans-de-vue-du-deck).

**Commandes et réouverture.** L’icône Tiroirs affiche Ancre et Cadenas. Le deck retrouve ses cartes et leur disposition après fermeture et réouverture. Un bouton dédié dans le tableau de bord supérieur est proposé, avec une icône de cartes à jouer. Essais sur Redmi à effectuer. [Référence Garage](https://github.com/FlyingZulu/Atelier-zulu/blob/bebf6408b1d471ac00abd7199d918433041c1e0f/projets/liaison-east-west.md#plans-de-vue-du-deck).

## 2026-11-25 — Règle impérative de prise d’information

**Décision de Flying Zulu.** Consulter les références pertinentes et vérifier l’existant avant de répondre, de proposer ou de modifier. Si une incertitude subsiste, poser une question ciblée avant d’avancer sur le point concerné. [Règle inscrite dans les méthodes Zulu](https://github.com/FlyingZulu/Atelier-zulu/blob/f03dc5d7132b32b4b509bbfb279a1559bc960acc/methodes/README.md#règles-à-ne-pas-déroger).

**Précision.** Retrouver les consignes et décisions déjà documentées dans GitHub, Notion et les échanges ChatGPT du projet. Pour le Garage, recouper la consigne d’origine avec le Registre et le banc actuel. Solliciter Flying Zulu uniquement si un point précis reste à trancher. [Règle complétée](https://github.com/FlyingZulu/Atelier-zulu/blob/388321fc7402abe67bef3d6147cf1aa8e5e17d42/methodes/README.md#règles-à-ne-pas-déroger).

**Responsabilité des agents.** Flying Zulu rappelle son exigence « je suis pas là pour m'occuper des agents comme d'une classe d'apprentis dissipés, j'ai besoin d'ingénieurs ». Sa formulation figure dans les [Règles à ne pas déroger](https://github.com/FlyingZulu/Atelier-zulu/blob/f8fc1dcced6be97fcc1eadf3c6402bb68f19832e/methodes/README.md#règles-à-ne-pas-déroger).

**Mises à jour.** Vérifier les dernières informations du projet et du Registre avant de répondre ou d’intervenir. Distinguer les faits vérifiés des hypothèses et clarifier les points incertains avant d’agir. [Règle mise à jour](https://github.com/FlyingZulu/Atelier-zulu/blob/a69e4fc0dbce7c8575b5861d351ec10f2141f4cf/methodes/README.md#règles-à-ne-pas-déroger).

## 2026-11-25 — EastBlOk 0186 et WestBlOk 0020 · GARAGE commun

**Architecture.** Les deux APK sont produites par le même projet Android et la même activité GARAGE. Chaque variante charge son moteur natif. Le bandeau et l’icône identifient le bloc. Les panneaux exposent les réglages du moteur.

**Parité.** Bandeau DSP, deck et potards détachables, Kits, Snaps, MIDI Learn, Piano/Grille, gammes, diagnostic, capture, Yadaa!, Turing et ARP partagent le même câblage Android. Les deux guides donnent le chemin du signal. L’édition des sources OSC 1/2 et les réglages de synthèse East restent spécifiques.

**Validation.** Tests hôte de la chaîne Java/JNI jusqu’au stéréo pour les deux moteurs, avec PCM direct, granulateur, FM, transports et STOP. Comparaison West avec 0019 identique sur le rendu testé. L’interface, le micro et le MIDI physique restent à confirmer sur Android.

## 2026-11-25 — EastBlOk 0185 et WestBlOk 0019 · Deck et édition des notes

**Modifications.** La croix des tiroirs libres reste accessible. Le bandeau déverrouille le rangement du deck pour accrocher ou décrocher une carte. West expose ses potards, le dernier potard touché s’inverse et affiche un trait épais. En paysage, un maintien sur son nom l’accroche comme carte. Les sélecteurs se replient, et Reverse est vert menthe. Les deux bancs présentent les quatre commandes de déclenchement et transport sur une rangée. L’Undo/Redo du bandeau partage trois niveaux d’historique pour les mutations et les silences des deux générateurs. Les grains actifs sont montrés sur la forme d’onde. Capture en Normal, Intermédiaire ou Lo-fi. Guides et schémas intégrés.

**Validation.** APK signées avec appellations EastBlOk et WestBlOk et guides vérifiés. Sur ordinateur, le scénario Mutation Turing → deux trous ARP dans un appui → trou Turing s’annule et se rétablit dans l’ordre sur les deux moteurs. Gestes, rendu, qualité du micro et écoute restent à vérifier sur Android.

## 2026-11-25 — EastBlOk 0184 et WestBlOk 0018 · Bancs de validation

**Repères à la sortie.** East 0184 ↔ West 0018. La ligne de départ V1 attend le retour des testeurs.

**Mise à niveau.** Banque de 27 PCM commune, avec deux OVNI et cinq sons de jouets. Tenue par boucle fondue en PCM direct. Quatre prises Audio In de 30 s par banc, REC rouge, départ au relâchement et arrêt à l’appui suivant. Fenêtre granulaire initiale de 500 ms avec déplacement sur la forme d’onde. Ladder 2 ou 4 pôles, 4 par défaut. Guides intégrés avec schémas, repère visuel de dernière commande. East bleu ciel et West orange clair.

**Vérifications.** Signature et guides des APK, rendu de la banque et de la tenue, durée de capture du tampon, quatre combinaisons de sources et deux Lad‌ders dans East, quatre voix et trois réponses du LPG dans West. Horloges et mélange Turing/ARP contrôlés sur ordinateur. Gestes, micro et écoute restent à confirmer sur appareil.

## 2026-11-24 — WestBlOk 0017 · Tiroirs, Kits, Snaps et Ladder

**Version à la sortie.** EastBlOk 0183, dernière livraison vérifiée du binôme.

**Changements.** Bandeau bleu ciel avec accès au bas du banc et les commandes SNAP, KIT, ASSIGN. Rappel des quatre slots depuis la mémoire après préchargement, mode KIT pour choisir puis confirmer le slot d’enregistrement. Commandes de voix directes et réglages fins en sous-tiroirs. Fader Zulu avec huit banques ZU roses et huit LU jaunes, menu accessible replié, enregistrement via KIT + SNAP. Ladder deux ou quatre pôles, quatre par défaut. Guide intégré avec l’histoire des inspirations du WestBlOk et les nouveaux gestes.

**Validation.** APK compilée et signature vérifiée. Rendu hôte des quatre voix et trois réponses du LPG jusqu’à la sortie stéréo. Les rendus Ladder quatre pôles sont identiques à ceux calculés avec le moteur 0016. Variation de pente en deux pôles et commutations de filtre testées. Gestes Android, rappel sur appareil et écoute à confirmer sur Redmi.

## 2026-11-24 — WestBlOk 0016 · Phaser et repère binôme

**Version à la sortie.** WestBlOk 0016 avec EastBlOk 0183 comme dernière livraison vérifiée. Le rapport du GARAGE conserve le numéro East fixé lors de la compilation.

**Changements.** Phaser stéréo à quatre étages dans Modulation avec Vitesse, Profondeur et Mix. Les cinq effets conservent leurs vitesses jusqu’à mi-course. Le maximum monte de 6,4 à 7,68 Hz.

**Validation DSP.** Un rendu sur ordinateur vérifie le signal direct à Mix zéro, l’effet des cinq modes, la stéréo et la vitesse maximale. Écoute et charge DSP à confirmer sur Redmi.

## 2026-11-24 — WestBlOk 0015 · Mode jeu et rangement

**Changements.** Repère rotatif des potards renforcé. Le tiroir du bandeau permanent masque les en-têtes des panneaux accrochés et laisse les touches du clavier accessibles. Il restitue les poignées, les réglages de clavier et la poignée de largeur en paysage. Icône Android W et guide intégré mis à jour.

**Validation.** APK compilée, signature, version, icône et guide vérifiés. Les vérifications sur ordinateur des Snaps et du morphing passent. Le rendu, le redimensionnement et les gestes des tiroirs restent à vérifier sur Redmi.

## 2026-11-24 — WestBlOk 0014 · Capture Snap silencieuse et Kits

**Changements.** Panneaux accrochés au premier plan devant le banc. Capture Snap depuis le tiroir du fader Zulu, ciblage comme ASSIGN, réglage de brouillon sans modifier le son, tap pour confirmer et glissé vers le bas pour enregistrer le côté ZU ou LU. Le tiroir Kits propose la bibliothèque ou un slot à la sauvegarde, et les quatre raccourcis affichent le nom du kit.

**Validation.** APK compilée, signature et guide 0014 vérifiés. Le test sur ordinateur a contrôlé l’édition silencieuse, la confirmation, le changement de cible et les quatre états du morphing. La gestuelle des panneaux, les noms de slots et le rappel d’un kit avec captures restent à vérifier sur Redmi.

## 2026-11-24 — Ancrer les décisions Zulu validées

**Décision de Flying Zulu.** Partir des gestes, du vocabulaire et des icônes déjà validés. Ancrer chaque décision confirmée dans la référence du sujet. Si une évolution est validée, elle devient la norme et le Registre conserve la trace du changement. Une ambiguïté se clarifie avec Flying Zulu avant de modifier la référence.

**Référence.** [Méthodes de l’Atelier · Ancrer une décision validée](https://github.com/FlyingZulu/Atelier-zulu/blob/main/methodes/README.md#ancrer-une-décision-validée)

## 2026-11-24 — WestBlOk 0013 · Quatre états du fader Zulu

**Livraison test.** Cette version regroupe les potards verticaux, les poignées masquables, le redimensionnement en paysage, les dispositions par orientation, les Kits avec captures, les quatre slots et les paires Snap. ZU et LU s’activent indépendamment. Le fader reste sans effet avec les deux côtés éteints. Un côté inactif utilise la référence, et les deux côtés actifs font évoluer les paramètres entre les deux Snaps.

**Validation.** APK compilée, signée et guide 0013 vérifié dans le paquet. Les quatre états ZU/LU et les paramètres absents d’un côté ont été vérifiés sur ordinateur. Les gestes, la rotation, la restauration des kits avec audio et l’écoute sont à vérifier sur le Redmi.

## 2026-11-24 — WestBlOk 0012 · Potards, Kits et Snaps

**Livraison test.** Potards à geste vertical, poignées masquables depuis le bandeau et panneaux épinglés redimensionnables en paysage. Dispositions portrait et paysage conservées séparément. Rappel de l’état à l’ouverture, bibliothèque Kits avec captures et quatre slots rapides. Capture sélective des paramètres ZU et LU, sauvegarde des paires et fader Zulu horizontal après DELAY.

**Décisions pour ce test.** Réouverture et rappel avec Turing et ARP à l’arrêt. Le cadenas du fader protège sa position. La 0012 porte son propre numéro après la compilation 0011 mise en pause.

**Validation.** APK compilée, signature et guide intégré vérifiés. Interpolation, valeurs discrètes et restauration des mappings et masques de notes contrôlés sur ordinateur. Sauvegarde et rappel de captures, rotation, gestes et usage MIDI physique à vérifier sur le Redmi.

## 2026-11-24 — WestBlOk 0011 · Tiroirs compacts et position des panneaux

**Changements livrés.** Tiroirs plus courts. Croix ronde à gauche et crochet rond à droite, à l’intérieur du panneau. Glissé vers le haut sur le crochet pour déplacer, glissé vers le bas pour passer devant. Alignement magnétique près des bords. Fermeture vers le tiroir d’origine et conservation de la position et du rang tant que le crochet reste actif. Pour le clavier, glissé vers la droite sur le cadenas pour basculer le verrou de registre.

**Validation.** APK compilée et signature vérifiée. Guide 0011 et gestes contrôlés dans le paquet. Les interactions tactiles, la pile et le rendu en portrait et paysage restent à essayer sur le Redmi.

## 2026-11-24 — WestBlOk 0010 · Clavier et panneaux accrochés

**Changements livrés.** Zones de touches du piano distinctes. Cadenas de registre commun au piano et à la grille. Glisser change l’octave en silence quand le cadenas est ouvert. Grille de bas gauche vers haut droite, fondamentale colorée. Le crochet fixe le clavier en bas en portrait ou paysage. Les autres panneaux accrochés forment un groupe fixe réordonnable. La fermeture rend la ligne au tiroir d’origine et la réouverture retrouve le rang mémorisé pendant la session.

**Validation.** APK compilée et signature vérifiée. Guide 0010 contrôlé dans le paquet. Géométrie des touches, ordre des rangées et bornes MIDI contrôlés sur ordinateur. Les gestes, le rendu Android et les panneaux accrochés restent à essayer sur le Redmi dans les deux orientations.

## 2026-11-24 — WestBlOk 0009 · GARAGE, clavier et gammes

**Changements livrés.** Panneaux indépendants repliables avec fermeture réservée, choix Off / Paléo / Ladder et Sources avant Turing / ARP. Rotation selon Android. Piano et grille 32 notes, gammes prédéfinies et personnalisées, repli du clavier et activation indépendante pour Turing et ARP. MIDI Learn par contact sur la commande, avec état et confirmation dans le bandeau temporaire. Guide 0009 intégré, texte à défilement vertical.

**Validation.** APK compilée et signature vérifiée. Guide contrôlé dans le paquet. Quantification contrôlée sur ordinateur pour les 4 095 sélections non vides, toutes les fondamentales et toutes les notes MIDI. Rendu de l’interface en portrait et paysage, sauvegarde après redémarrage et contrôleur MIDI physique à vérifier sur téléphone.

## 2026-11-24 — WestBlOk 0008 · Mode d’emploi dans l’APK

**Changement livré.** Le bouton **Mode d’emploi** au bas du banc ouvre le guide complet embarqué, hors connexion. Le guide de la version 0008 inclut le schéma de routage, la procédure de diagnostic, le bandeau DSP, MIDI Learn et les Oblitérateurs.

**Validation.** Compilation Android et signature vérifiées. Le HTML du guide, sa version et ses sections ont été contrôlés dans l’APK signée. L’ouverture et la lisibilité sur le Redmi restent à vérifier.

**Règle d’itération.** Mettre à jour le guide intégré avec chaque APK et consigner les changements ainsi que les vérifications dans ce registre. [Méthodes de travail Zulu](https://github.com/FlyingZulu/Atelier-zulu/tree/main/methodes)

## 2026-11-24 — ZuluBlOk · Traçabilité des liaisons

**Décision de Flying Zulu.** Chaque liaison doit être identifiable entre les briques d’un Lego, entre Legos et entre blocs. Le schéma indique d’où part le signal, où il arrive, ce qui l’active et comment vérifier qu’il passe. Les chemins audio et les commandes de notes ou de paramètres sont repérables séparément.

**Mode opératoire.** Le schéma et la procédure de diagnostic sont accessibles depuis le mode d’emploi du bloc. Tester chaque étage seul, puis la liaison avec le suivant. En cas de panne, relever la dernière liaison qui répond et la première qui échoue, avec la version, le routage, le geste et le diagnostic. Mettre le schéma à jour avec les changements de connexion. [Méthodes de travail Zulu](https://github.com/FlyingZulu/Atelier-zulu/tree/main/methodes)

**Clarté des décisions.** Consigner des décisions simples et précises. Si une consigne semble contredire une décision précédente, ou si son sens est incertain, demander à Flying Zulu de clarifier et attendre sa réponse avant d’inscrire la décision ou de poursuivre le travail concerné.

**Application au WestBlOk 0006.** Guide de test complété avec le trajet audio, l’entrée FM, les commandes et des points de contrôle. Dans le banc, la molette transmet désormais la valeur Cutoff au moteur. L’aperçu PCM fonctionne indépendamment de la source de la voix, et une destination Turing de timbre laisse le clavier jouer en direct lorsque l’ARP est arrêté.

**Validation.** APK compilée et signature vérifiée. Rendus et essais sur ordinateur pour les sources, l’enveloppe, les horloges, le filtre et la stéréo. Vérifications du microphone, de la molette physique et du contrôleur MIDI sur téléphone à effectuer.

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


## 2026-11-22 — Audit complémentaire des transports Android

- ZTF : filtrage des réponses par caractère de commande ; garde-fous sur taille/allocation et progression des offsets de lecture/écriture afin d'éviter les boucles infinies sur réponses malformées ou sans progression.
- USB-MIDI : un paquet d'événement de 4 octets n'est déclaré envoyé que si les 4 octets ont été transférés.
- ZuluLink : démarrage des deux sockets transactionnel avec nettoyage et possibilité de nouvel essai en cas d'échec ; erreur exposée dans Logcat ; notification UI en cas de changement d'adresse IP d'un pair.
- ZuluLink entrant : validation des valeurs MIDI, tempo fini et borné, beat fini/non négatif, timestamp et PING.
- Commits Android : `e65ad086b07fb14707799f92b673e9c12c60ee0f`, `8889a214f13c3531912cbd5f49ac3300fc04bfa3`, `dc0918f002f9e90f2d7345b735fa06da7b7cad49`, `3a00748d2b9b9e2b4923f0f252468f4c035cdc76`, `433490e915324460166e9dda39f428b12024b1df`, `6a8eb2e20b16af52d74bcacb57ea8b0c4cf963dc`.
- Builds #370 à #373 réussis. Build #374 / run `44994695432` réussi, artefact debug `zulu-apk-374` (6 319 159 octets). Build #375 / run `44994810690` encore en cours au moment de cette entrée sur le dernier head réseau.
- Handoff Android mis à jour dans FZuluTek au commit `6234e541f44af9738fedb894fc8036ca9338c77c`.
- Aucun test USB/FM-1 ni réseau multi-appareils effectué. Les retours synchrones trompeurs de `Fm1Usb.ping()/pull()/push()` restent à refondre vers une API asynchrone après revue des appelants.
- Aucun firmware FM-1, patch embarqué ou autre projet modifié.


### Résultat du build #375
- Build #375 / run `44994810690` : **succès** sur `6a8eb2e20b16af52d74bcacb57ea8b0c4cf963dc`, incluant les validations de champs ZuluLink entrants.
- Compilation et publication réussies ; artefact debug `zulu-apk-375`, 6 319 460 octets, non expiré. Release dédiée ignorée sur la branche PR.
- Le build #376 sur le head documentaire `6234e541f44af9738fedb894fc8036ca9338c77c` a réussi ; artefact `zulu-apk-376` (6 319 448 octets).
- PR #46 reste ouverte et non fusionnée ; aucun test matériel USB/FM-1 ou réseau multi-appareils.


## 2026-11-22 — Ordonnancement connexion USB et contrat asynchrone

- Défaut : `MainActivity.linkScan()` lançait PING / liste fichiers / WATCH immédiatement après `scan()`, avant la fin éventuelle de la permission Android et de l'ouverture de l'interface USB.
- Correction : callback `Fm1Usb.onConnected` émis seulement après transport ZTF prêt ; les premières requêtes sont maintenant mises en file après ce signal.
- Les API `ping/pull/push/pushNamed/pullNamed` ne renvoient plus de faux résultats synchrones avant exécution du worker. Les résultats passent par les callbacks de statut/progression.
- Appelants Kotlin inspectés : 11 fichiers de l'app Android ; les usages de ces méthodes ne consomment pas les valeurs de retour supprimées.
- Commits : `088051da7f3b6cbbe05aca0e5e97b8431b2499c3`, `7a3acd1cd00e615f662b84f747e20b4b0f64512a`, `774f685c35a12aae59fd0f6f70b111af09b9635d`.
- Builds #376 à #379 : succès ; artefacts debug publiés. Le #379 valide le head contenant le contrat asynchrone.
- Handoff Android mis à jour au commit `14b9da61490c8f20cfdedf03039e4f4235ab218a`.
- Aucun essai physique USB/FM-1. Aucun firmware ou patch embarqué modifié.


## 2026-11-22 — Préservation des notifications ZTF en direct

- `ZtfTransport.request()` mettait de côté les notifications PQ_CHANGED pendant les requêtes companion, mais `zrequest()` ignorait les trames companion pendant les commandes ZTF brutes. Les opérations PING/LOAD/paramètres pouvaient donc perdre des changements en direct.
- Correction : `zrequest()` parse les trames companion reçues pendant l'attente et les remet dans la file des notifications, tout en continuant à filtrer la réponse ZTF par commande.
- Commit : `5331cb00924fb14820fe9cd6af08f38002a83cf9`.
- Build #376 / run `44994960851` : succès, artefact `zulu-apk-376` (6 319 448 octets). Build #377 / run `44995039610` : succès, artefact `zulu-apk-377` (6 319 507 octets). Builds #378 / #379 / #380 étaient encore en cours au dernier contrôle. Build #381 / run `44995223691` compile la correction de notifications.
- Handoff FZuluTek mis à jour au commit `a7fbee7648c967d3737c0372933c942676a004fe`.
- Aucun essai matériel USB/FM-1 effectué ; firmware et patches inchangés.


### Résultats CI supplémentaires — builds #378 et #379
- Build #378 / run `44995046947` : succès, head `7a3acd1cd00e615f662b84f747e20b4b0f64512a`, artefact debug `zulu-apk-378` (6 319 627 octets).
- Build #379 / run `44995115379` : succès, head `774f685c35a12aae59fd0f6f70b111af09b9635d`, artefact debug `zulu-apk-379` (6 319 423 octets).
- Builds #381 et #382 : succès ; artefacts et détails consignés dans la section de résultats ci-dessous.


### Résultats CI — builds #380 à #382 (22/11/2026)
- Build #380 / run `44995169635` : succès sur le handoff intermédiaire `14b9da61490c8f20cfdedf03039e4f4235ab218a`, artefact debug `zulu-apk-380` (6 319 490 octets).
- Build #381 / run `44995223691` : succès sur le commit code `5331cb00924fb14820fe9cd6af08f38002a83cf9`, qui préserve les notifications companion `PQ_CHANGED` pendant les requêtes ZTF brutes ; artefact debug `zulu-apk-381` (6 319 501 octets).
- Build #382 / run `44995254811` : succès sur le handoff final `a7fbee7648c967d3737c0372933c942676a004fe`, artefact debug `zulu-apk-382` (6 319 497 octets).
- Pour les trois runs, compilation et publication APK réussies ; étape Release dédiée ignorée (aucune release signée revendiquée).
- PR #46 reste ouverte, non fusionnée, mergeable. Aucun essai matériel Android, USB/FM-1 ou réseau multi-appareils effectué ; les symptômes LCD blanc et audio clic seul restent à diagnostiquer sur appareil avec Logcat.


## 2026-11-22 — Idempotence du scan USB FM-1 (APK)

- Audit du cycle de vie : l'entrée répétée dans la page LINK ou un nouveau scan pendant une session déjà connectée pouvait ouvrir une seconde connexion USB, remplacer les références du transport/thread de surveillance et laisser l'ancien watcher actif.
- Correction ciblée dans `Fm1Usb.openNow()` : si un transport est déjà connecté, le worker le réutilise et réémet `onConnected` au lieu d'ouvrir une seconde connexion. Les scans répétés pendant une session active deviennent idempotents.
- Commit : `d6feaae17f7d01470352d8e63da7183c483318a1`.
- Build #384 / run [45009852514](https://github.com/FlyingZulu/FZuluTek/actions/runs/45009852514) en cours au moment de cette note ; ne pas considérer la correction validée avant le résultat CI.
- Revue complémentaire : les requêtes companion, ZTF brutes et la lecture watch partagent le même `ReentrantLock` dans `ZtfTransport`. Relecture des validations de longueur et de plages ZuluLink ; aucun autre défaut confirmé ni changement supplémentaire justifié.
- Aucun test matériel Android/USB/FM-1. Aucun firmware ni patch embarqué modifié. PR #46 reste ouverte et non fusionnée.


## 2026-11-22 — Validation USB et arrêt propre du watcher

- Build #384 réussi sur la correction d'idempotence du scan : APK CI `zulu-apk-384`, 6 319 459 octets. Release dédiée ignorée.
- Build #385 réussi sur le handoff actualisé : APK CI `zulu-apk-385`, 6 319 473 octets. Release dédiée ignorée.
- Revue du watcher de paramètres : `ZtfTransport.poll()` attend sur `ZtfLink.read()`, dont la file de réception est interruptible. L'ancien `catch(Exception)` pouvait absorber l'interruption et lancer un sommeil de reprise de 500 ms ; une reconnexion rapide risquait de laisser l'ancien watcher actif.
- Correction dans `Fm1Usb.kt`, commit `fc9cfbb86ef992f027e41234b51aec3c2d22049d` : arrêt explicite à l'interruption, y compris pendant les temporisations ; les erreurs ordinaires ne déclenchent une reprise que si la connexion reste active.
- Validation CI de ce dernier commit en attente. Pas de test matériel, aucun firmware ni patch embarqué modifié, PR #46 non fusionnée.


## 22/11/2026 — Audit USB FM-1 : débranchement et ré-énumération

- Défaut statique confirmé : le chemin de scan idempotent ne comparait que `connected` et `transport != null`. Après retrait physique, un indicateur de connexion périmé pouvait conduire à réutiliser un transport appartenant à l'ancienne énumération USB.
- Correction dans FZuluTek : receiver `ACTION_USB_DEVICE_DETACHED`, fermeture sérialisée sur le worker, interruption du watcher, fermeture du lien MIDI et remise à zéro de l'identité du périphérique actif. Le chemin de réutilisation exige désormais l'égalité de l'identifiant USB actif et du périphérique rescanné.
- Commits code : `b883f1fe8722194b191011473742a97740b17538`, `556f65de08db939b9a519788733e16cc4f1fa2f3`. Handoff FZuluTek : `ab224fa44bb5a713d4ecce59c81b459f13fbe057`.
- CI en attente au moment de cette entrée ; essais physiques à faire : débranchement pendant transfert, reconnexion rapide, scans répétés et autorisation USB.
- Aucun firmware FM-1, patch embarqué ou projet hors périmètre modifié. PR #46 non fusionnée.


## 22/11/2026 — Audit Oboe : nettoyage après échec de démarrage

- Défaut statique confirmé dans `ztek_start()` : si `openStream()` réussissait mais `requestStart()` échouait, `z->out` restait non nul. Un appel ultérieur pouvait donc retourner un faux succès via le test `if (z->out) return 1`, sans flux audio démarré et sans possibilité de retry.
- Correction Android dans `app-zulutek/src/main/cpp/ztek_engine.cpp` : fermeture puis remise à `nullptr` du flux lorsque `requestStart()` échoue. Aucun changement DSP, aucun changement du chemin de rendu réussi.
- Commit code FZuluTek : `34bd37e5228551746cf215b9d99429094350c0ff`.
- Build CI en attente ; aucun essai sur appareil Android/Oboe. Aucun firmware FM-1, patch embarqué ou projet hors périmètre modifié.


## 22/11/2026 — APK FIRST FZulu-Control : version SHA test et réparation CI

### Périmètre et décisions

- Périmètre **APK Android seulement** dans `FlyingZulu/FZulu-Control`, module `app-zulutek` ; aucun firmware FM-1 ni patch embarqué modifié.
- La batterie de tests réels sur téléphone est **réservée à la fin** de l'audit. Pas de validation matérielle implicite.
- La documentation de suivi est répliquée vers la page Notion « Registre — carnet de bord ZuluTek » ; ce dépôt Registre reste le journal canonique.

### Modifications effectivement committées

- PR draft [FZulu-Control #4](https://github.com/FlyingZulu/FZulu-Control/pull/4), branche `audit/apk-debug-build-badge` : badge LCD de build SHA très lisible pendant 10 secondes au démarrage et rappel dans OPTIONS, affichage réservé au debug (commits `4adcca5`, `ceccbbe`).
- Protocole de recette différée : `docs/APK-FIRST-TEST-PLAN.md` (commit `d71768e`).
- La première CI de la PR a échoué avec deux erreurs Kotlin `Unresolved reference: BuildConfig` sur `LcdView.kt` et `MainActivity.kt`, [run 45013905364](https://github.com/FlyingZulu/FZulu-Control/actions/runs/45013905364). Correctif committé : activer `buildConfig true` dans `app-zulutek/build.gradle` (commit `7b7cf5c`).
- Carnet technique de branche : `docs/APK-AUDIT-LOG.md` (commit `0a1e1f1`).

### Validations réellement exécutées

- Avant les nouveaux changements : CI `main` [run 45013837531](https://github.com/FlyingZulu/FZulu-Control/actions/runs/45013837531) **success**.
- Après le correctif : CI de branche [run 45014296470](https://github.com/FlyingZulu/FZulu-Control/actions/runs/45014296470) **success**, puis [run 45014306463](https://github.com/FlyingZulu/FZulu-Control/actions/runs/45014306463) **success**, HEAD `0a1e1f1cb4a0288e9f2d78e7b3b33e15d77450ba`. Il s'agit d'une preuve de build CI, **pas** d'une recette utilisateur ni d'une validation debug/release visuelle.

### Points ouverts / risques

- PR #4 encore en draft, non fusionnée dans le cadre de cette intervention.
- Audit fonctionnel Android complet encore à conduire ; checks audio, séquenceurs, UI et connectivité, puis recette sur appareil en fin de parcours.
- Risque de sécurité à examiner : configuration de signature avec secret en clair dans `app-zulutek/build.gradle`. Ne pas modifier la signature effective sans plan de migration pour les APK déjà installées.
- Coordination nécessaire avec les autres interventions APK (notamment FZuluTek PR #44-#46) pour éviter de confondre dépôts, branches et validations.


## 22/11/2026 — Ressources GitHub favorites : accès à qualifier

- Demande : exploiter les dépôts favoris du compte `FlyingZulu` pour identifier des composants utiles à l'audit et aux réparations APK ZuluTek.
- Vérifié : compte GitHub connecté `FlyingZulu`. Tentative de lecture des favoris par l'endpoint `/user/starred` via l'intégration : **bloquée par les restrictions des endpoints autorisés**. Tentatives de lecture publique de la page Stars et de `/users/FlyingZulu/starred` : non accessibles depuis cette session.
- **Aucun favori individuel n'a été identifié ni validé**. Aucune dépendance ni aucun code externe intégrés ; licences et compatibilité encore non examinées.
- Suite : obtenir une liste exportée ou des liens individuels vers les favoris, puis sélectionner les ressources adaptées au DSP Android, UI, USB-MIDI et ZuluLink. Ne pas présumer que les dépôts suggérés par une recherche publique sont des favoris de l'utilisateur.


## Suivi audit APK ZuluTek — 22/11/2026, 17:25 (Paris)

- PR [FZuluTek #48](https://github.com/FlyingZulu/FZuluTek/pull/48) conservée en brouillon ; branche `audit/zulutek-usb-midi-20261122`.
- **Nouveau correctif committé** : `c4e9a375`, dans `ZuluLink.kt`, capture de sockets UDP non nullables dans les lambdas des threads de réception pour éviter un problème de typage Kotlin avec les variables locales nullables mutables. Rapport GitHub complété au commit `ff7790e6`.
- **Contrôles effectués** : lecture de la branche et du rapport, comparaison avec la tête précédente `0ec6f690` (identique avant intervention), interrogation des workflows PR de cette tête (aucun run retourné). **Aucun build Gradle, test Android, test réseau, audio, USB ou matériel exécuté** ; la CI du nouveau commit reste à vérifier.
- **Ouvert** : retours prématurés des API asynchrones `Fm1Usb`, concurrence ZTF, reconnexion USB, RIFF/WAV, tests ZuluLink, audio et UI ; secret de signature en clair à traiter uniquement après décision de migration.
- **Décisions nécessaires** : migration de signature et contrat d'API asynchrone. Aucun flash, rotation de clé ni fusion.


## Suivi audit APK ZuluTek — 22/11/2026, 19:25 (Paris)

- Périmètre : [FZuluTek PR #48](https://github.com/FlyingZulu/FZuluTek/pull/48), branche `audit/zulutek-usb-midi-20261122`, toujours en brouillon ; aucune intervention sur le firmware.
- **Code committé** : `51dc900a7b594f5df754bc78f133d929d45b24e2` — `ZtfTransport.fileWrite` refuse désormais `chunk <= 0` avant tout début de transfert. Garde prudente contre des appels avec bloc nul ou négatif ; aucun changement du protocole nominal.
- **Rapport GitHub committé** : `661113106e44ec3cde3af0a66066ce382848fc68` — ajout de la passe d'audit et des limites dans `docs/AUDIT-APK-2026-11-22.md`.
- **Contrôles réellement effectués** : comparaison GitHub de la branche contre `main` avant modification (15 commits d'avance, aucun retard) ; lecture statique de `Fm1Usb.kt` et `ZtfTransport.kt` ; interrogation des runs PR associés à la tête précédente `ff7790e6` (aucun run retourné).
- **Non validé** : compilation Gradle, CI des nouveaux commits, tests unitaires du cas `chunk=0`, Android, USB-MIDI, ZTF réel, audio, réseau, matériel.
- **Risques ouverts** : réponses ZTF non corrélées à la commande dans `zrequest`, retours prématurés des API USB asynchrones, reconnexion USB, parsing WAV/RIFF, ZuluLink et recette UI/DSP. Décisions nécessaires sur contrat API USB et stratégie de signature ; aucune clé changée.
- Aucun flash, aucune fusion, aucune rotation de clé.


## 22/11/2026 — Candidate musicale ZuluTek Android

- **Livraison** — APK debug ARM64 `ZuluTek-debug-56b64f53.apk`, badge `B56b64f53`, commit [`56b64f53`](https://github.com/FlyingZulu/FZuluTek/commit/56b64f539a58c11bae022d8630b02b976fe8e89e). SHA-256 du fichier signé `4002987adc3918ede0228e7a6b81dd75a6206eaadddbd0658d52b7f28227c596`. PR #48 en brouillon. [Build GitHub Actions](https://github.com/FlyingZulu/FZuluTek/actions/runs/45057315064)
- **Changements committés** — Relâchement des notes maintenues, gestes à plusieurs doigts, accords REC et transports Shift, resampling GLO+pad, lecture SMP interpolée et quantifiée au tempo, démarrage Oboe et ZuluLink, CC collectifs et redémarrage UDP. Corrélation des réponses ZTF et statut LOAD. [Rapport d’audit](https://github.com/FlyingZulu/FZuluTek/blob/audit/zulutek-usb-midi-20261122/docs/AUDIT-APK-2026-11-22.md)
- **Validé** — Assemblage Gradle local, contrôle du badge embarqué et de l’ABI, intégrité de l’APK et signature v2/v3 avec le certificat Zulu historique. Banc stéréo natif ASan/UBSan sans rapport, détection de fuites désactivée dans cet environnement. Cinq moteurs et relâchements, séquenceur, ARP, drums, looper MIDI, resampling, SMP simulé, sirène, FX/LFO, macro, SNAP et export/import de preset. Tests ZTF Kotlin et codec Python verts. ZuluLink en UDP local, cinq exécutions de deux cycles chacune après la correction du redémarrage.
- **À tester sur appareil** — Mise à jour de l’installation existante, sortie audio Oboe, gestes et affichage Android, micro, persistance des presets après relance, USB-MIDI et ZTF/UAC sur le FM‑1, ZuluLink entre appareils. Aucun essai physique effectué. [Recette musicale unique](https://github.com/FlyingZulu/FZuluTek/blob/56b64f539a58c11bae022d8630b02b976fe8e89e/docs/RECETTE-APK.md)
