# Création des agents Claude Code (haiku / sonnet / opus)

- **Date** : 2026-11-09 12:09
- **Branche** : feature/02-new-claude-files
- **Demande** : créer des agents pour répartir le travail, avec un modèle adapté à la difficulté

## Fichiers

| Action | Fichier | Rôle |
|--------|---------|------|
| créé | `.claude/agents/documentaliste.md` | haiku : fiches `documentation-dev/`, étapes du README |
| créé | `.claude/agents/traducteur.md` | haiku : fichiers `translations/`, textes Twig → `|trans` |
| créé | `.claude/agents/dev-symfony.md` | sonnet : entités, migrations, contrôleurs, formulaires, CRUD, upload |
| créé | `.claude/agents/integrateur-twig.md` | sonnet : templates, composants Symfony UX, Stimulus, CSS |
| créé | `.claude/agents/testeur.md` | sonnet : tests PHPUnit |
| créé | `.claude/agents/architecte.md` | opus : conception et débogage difficile, lecture seule, rend un plan |
| créé | `.claude/agents/relecteur.md` | opus : relecture avant commit, lecture seule |
| créé | `.claude/rules/dispatch-agents.md` | tableau de répartition et enchaînement type, chargé automatiquement |

## Raisons

- Tâches simples et répétitives → haiku (rapide, peu coûteux).
- Développement courant dont la conception est claire → sonnet.
- Décisions structurantes, sécurité, relecture → opus.
- `architecte` et `relecteur` n'ont pas les outils Write/Edit : ils conseillent sans modifier.
- Chaque agent rappelle les règles du projet : commandes dans le conteneur `php`, pas de commit ni de branche, textes en français via les traductions.

## Agents utilisés

- aucun

## Commandes lancées

    # vérification des en-têtes (name, model, tools) des 7 agents : OK

## À faire / points d'attention

- Relancer Claude Code (ou `/agents`) pour que les nouveaux agents soient pris en compte.
- Ajuster les modèles à l'usage si un agent haiku se trompe trop souvent.
