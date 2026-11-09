# Documentation de développement

Ce dossier contient le journal des modifications faites par Claude Code sur le projet
(règle définie dans `CLAUDE.md`, section « Commits et documentation »).

Claude ne crée ni branche ni commit : chaque fiche sert à relire le travail avant de le committer soi-même.

## Convention de nommage

    YYYY-MM-DD-HH-MM_description-courte.md

- date et heure locales au moment de la modification
- description courte en minuscules, mots séparés par des tirets, sans accents
- exemple : `2026-11-09-11-34_fichiers-md-claude.md`

## Contenu minimal d'une fiche

Partir de [`_modele.md`](_modele.md) :

- **Date**
- **Branche** git en cours
- **Fichiers créés / modifiés / supprimés**
- **Raisons** de la modification
- **Agents utilisés** (sous-agents Claude Code lancés, ou « aucun »)
- **À faire / points d'attention** (facultatif)

Une fiche par tâche demandée (pas une par fichier).
