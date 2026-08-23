# CLAUDE.md - Contexte pour Claude Code

## Ce repo

**monecrin-desktop-releases** — Repo **public**, **sans code source**, destiné à héberger les
releases publiques signées du client desktop **Mon Écrin** (installateurs Windows + `SHA256SUMS.txt`
+ signature Ed25519), sur le modèle `LockNote-Pro-releases`. Nom harmonisé, contrepartie de
`monecrin-desktop-windows`/`-commun`/`-linux`/`-ios`.

## ⚠️ PAS la cible active de publication actuellement

Ce repo est un **mirror créé le 05/08/2026** (`git clone --mirror` + `git push --mirror`) de l'ancien
`ctardy/monecrin-sync-releases` — même historique/tags git, **mais AUCUNE GitHub Release** dessus
(les assets binaires des Releases GitHub ne sont **pas** répliqués par un mirror git, seuls les refs
le sont). Le job Jenkins `monecrin-desktop-release` publie toujours vers
**`ctardy/monecrin-sync-releases`** (l'original), pas vers ce repo — vérifié en conditions réelles
le 05/08/2026 (release `v0.1.0-beta` publiée sur `monecrin-sync-releases`, pas ici).

**Le client lui-même (`monecrin-desktop-commun/crates/core/src/tuning.rs`) a l'URL de vérification
de mise à jour codée en dur sur `monecrin-sync-releases`.** Basculer la publication et cette URL vers
ce repo est un chantier à part entière (republier les assets historiques, changer l'URL client,
tester l'auto-update de bout en bout) — **non fait, ne pas basculer l'un sans l'autre** : ça
casserait l'auto-update de tout le parc installé.

**Repos frères** : `monecrin-desktop-commun` (crates partagées), `monecrin-desktop-windows` (GUI,
héberge les scripts `build-installer.sh`/`sign-release.sh`/`publish-release.sh`),
`monecrin-desktop-linux` (placeholder), `monecrin-desktop-ios` (placeholder), `monecrin-core`
(backend), `monecrin-android`, `monecrin-iphone`.

## Si un jour la bascule est décidée

1. Republier (ou au moins recréer) les Releases GitHub existantes de `monecrin-sync-releases` ici
   (assets binaires, pas seulement les tags)
2. Changer l'URL dans `monecrin-desktop-commun/crates/core/src/tuning.rs`
3. Changer `REPO=` dans `monecrin-desktop-windows/scripts/publish-release.sh`
4. Tester l'auto-update de bout en bout sur un poste réel avant tout déploiement large

Détail complet : `CHANGELOG.md` infra (`/opt/.claude/`) du 05/08/2026, mémoire Claude Code
`project_monecrin_repo_split_20260805`.

---

## Mémoire d'architecture centralisée

Les décisions d'architecture et les discussions techniques transverses du projet sont archivées
dans le dépôt core : `../monecrin-core/docs/discussions/` — fiches `/disc` rangées par module et
par date, plus les synthèses dans `syntheses/`.

Avant toute tâche d'architecture, tout refactoring ou toute analyse qui dépasse le périmètre de ce
dépôt, **consulter ce dossier**. Les règles propres à ce dépôt, ci-dessus, restent prioritaires
pour tout ce qui lui est spécifique. Le protocole complet `/disc` et `/synthese` est décrit dans
`../monecrin-core/CLAUDE.md`.
