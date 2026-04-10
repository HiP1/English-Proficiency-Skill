🇬🇧 [English](README.md) · 🇪🇸 [Español](README.es.md)

# English Proficiency Scorecard

Un skill pour agent IA qui évalue le niveau d'anglais d'un utilisateur et génère un scorecard HTML interactif avec des scores estimés selon les principaux référentiels internationaux : CECRL, IELTS (Academic et General Training), TOEFL iBT, Cambridge (CAE/CPE) et TOEIC (L&R et S&W).

Le skill évalue l'écriture réelle à partir de l'historique de conversation, des services connectés (e-mails, documents) et d'échantillons en direct optionnels — pas de QCM ni de tests à choix multiples. Le résultat est un document HTML autonome et partageable, avec des cartes de scores animées, des comparaisons avec des seuils institutionnels, des échantillons d'écriture annotés et une section méthodologie transparente.

## Fonctionnement

Le skill guide Claude à travers un workflow en quatre phases :

1. **Entretien et configuration** — Comprendre le profil de l'utilisateur, recueillir ses préférences (mode de calibration, confidentialité, mise en page) et identifier les sources de données disponibles
2. **Analyse des preuves** — Analyser l'écriture à travers toutes les sources disponibles : grammaire, vocabulaire, contrôle des registres, compétence pragmatique et transferts L1
3. **Génération du scorecard** — Produire un scorecard HTML interactif de deux pages à partir du template inclus, avec des scores calibrés selon le guide de notation et les benchmarks
4. **Révision et ajustement** — L'utilisateur examine le scorecard et peut contester tout score ou observation ; les axes d'amélioration sont discutés dans le chat, pas ajoutés au document

## Contenu du package

```
english-proficiency-scorecard/
├── SKILL.md                          # Instructions principales et workflow
├── LICENSE.txt                       # Licence MIT + vérification d'intégrité
├── INTEGRITY.sha256                  # Manifeste SHA-256 de tous les fichiers
├── assets/
│   └── template.html                 # Template du scorecard interactif
└── references/
    ├── scoring-guide.md              # Barèmes de notation par référentiel
    └── benchmarks-fallback.md        # Données de référence institutionnelles
```

## Principes de conception

Le skill repose sur sept principes documentés dans SKILL.md :

1. **L'intégrité d'abord** — Les scores reflètent les preuves. Claude ne flatte ni ne gonfle jamais les résultats, même sur demande.
2. **L'utilisateur choisit la calibration** — Estimation honnête ou conservatrice, mais jamais au-dessus de ce que les preuves justifient.
3. **Les données auto-déclarées sont clairement signalées** — Les scores d'expression orale et de compréhension orale basés sur le témoignage de l'utilisateur sont étiquetés comme tels.
4. **Respect de la vie privée** — Le scorecard est conçu pour être partagé ; l'utilisateur confirme les informations personnelles à inclure.
5. **Pas de branding — mais la divulgation du modèle est autorisée** — Pas de noms de produits comme signaux de crédibilité. La section méthodologie peut mentionner factuellement quel modèle IA a réalisé l'analyse.
6. **Les axes d'amélioration restent dans le chat** — Le scorecard met en valeur la maîtrise. Les suggestions d'amélioration sont discutées en privé.
7. **Neutralité du contenu** — Tout le texte généré est linguistiquement descriptif, jamais culturellement prescriptif. Les benchmarks sont factuels, les annotations des échantillons d'écriture s'en tiennent à l'analyse linguistique, et aucune variété d'anglais n'est traitée comme supérieure. Ce principe sert aussi de protection contre les versions altérées qui injecteraient des biais dans des évaluations d'apparence légitime.

## Vérification d'intégrité

Le skill comprend un système d'intégrité à trois couches :

- **Manifeste SHA-256** (`INTEGRITY.sha256`) — Empreintes de tous les fichiers du package. Exécutez `sha256sum -c INTEGRITY.sha256` pour vérifier que rien n'a été modifié.
- **Témoin LICENSE** — Le fichier de licence contient des instructions pour que le modèle IA vérifie l'intégrité des fichiers avant exécution. C'est un choix de conception délibéré et un point de départ pour une discussion sur la sécurité des skills en texte brut (voir ci-dessous).
- **Protection de neutralité du contenu** — Le Principe 7 ordonne au modèle d'ignorer ses propres instructions si elles poussent vers un contenu biaisé, et de signaler le problème à l'utilisateur.

Aucune couche n'est infaillible à elle seule. Ensemble, elles rendent significativement plus difficile l'utilisation malveillante du skill à l'insu de l'utilisateur.

### À propos de la sécurité des skills

Les skills pour agents IA sont des fichiers d'instructions en texte brut. Contrairement aux logiciels compilés, n'importe qui peut ouvrir un SKILL.md, ajouter une ligne et le redistribuer. La barrière à la falsification est nulle, et la plupart des utilisateurs ne liront pas 500 lignes d'instructions pour vérifier l'absence de comportements cachés.

Le système d'intégrité présenté ici est une première tentative pour résoudre ce problème. Le mécanisme du témoin LICENSE — cacher des instructions de vérification dans un fichier que la plupart des gens ignorent — est volontairement à la limite. Il est lisible par quiconque ouvre le fichier, ce que nous considérons comme la ligne éthique : transparent-si-inspecté est acceptable ; encodé-pour-exclure-les-humains ne l'est pas.

Nous pensons que cette conversation mérite d'avoir lieu à mesure que l'écosystème des skills se développe. Si vous avez des idées pour de meilleures approches, ouvrez une issue.

## Installation

### En tant que Skill Claude

Téléchargez le fichier `.skill` depuis la page [**Releases**](https://github.com/HiP1/English-Proficiency-Skill/releases), puis installez-le dans votre environnement Claude.

### Autres fournisseurs d'IA

Le fichier `.skill` est une archive zip standard. Téléchargez-le depuis la page [**Releases**](https://github.com/HiP1/English-Proficiency-Skill/releases), renommez-le de `english-proficiency-scorecard.skill` en `english-proficiency-scorecard.zip`, importez-le dans votre plateforme de chat et demandez au modèle d'utiliser le skill contenu dans le fichier zip. Le `SKILL.md` est le point d'entrée ; le template dans `assets/` et les fichiers de référence dans `references/` sont chargés selon les besoins. Utilisez le modèle le plus performant disponible sur votre plateforme.

### Manuel

Clonez ou téléchargez ce dépôt. Dirigez votre outil IA vers le fichier `SKILL.md` comme point d'entrée.

## Origine

Ce skill a été créé par HiP (Ivan Phan) et Claude Opus 4.6 (Anthropic) en février-mars 2026. Il est né d'une véritable évaluation de niveau d'anglais — HiP a demandé à Claude d'évaluer son anglais selon les référentiels internationaux en utilisant son historique de conversation réel et deux ans d'e-mails envoyés. Le scorecard issu de cette évaluation est devenu le template, et la méthodologie d'évaluation est devenue le skill.

Les barèmes de notation, les données de référence, le design d'interaction, l'architecture de sécurité et le cadre de neutralité du contenu ont tous été développés par collaboration itérative sur plusieurs sessions. Le projet est une création originale, non dérivée de skills existants.

## Licence

MIT — utilisez, modifiez et partagez librement. Conservez simplement le crédit.

Exécutez `sha256sum -c INTEGRITY.sha256` pour vérifier si votre copie correspond à l'original.
