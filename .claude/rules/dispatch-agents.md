# Répartition du travail entre les agents

Les agents sont définis dans `.claude/agents/`. Le modèle suit la difficulté de la tâche.

| Difficulté | Modèle | Agent | Pour |
|------------|--------|-------|------|
| simple | haiku | `documentaliste` | fiches `documentation-dev/`, étapes du README |
| simple | haiku | `traducteur` | fichiers `translations/`, textes Twig → clés `|trans` |
| moyenne | sonnet | `dev-symfony` | entités, migrations, contrôleurs, formulaires, CRUD, upload |
| moyenne | sonnet | `integrateur-twig` | templates, composants UX, Stimulus, CSS |
| moyenne | sonnet | `testeur` | tests PHPUnit |
| difficile | opus | `architecte` | conception, modèle de données, sécurité, bugs difficiles (plan, sans modifier) |
| difficile | opus | `relecteur` | relecture avant commit (sans modifier) |

## Enchaînement type d'une fonctionnalité

1. `architecte` si la tâche est floue ou touche au modèle de données / à la sécurité.
2. `dev-symfony` puis `integrateur-twig` (en parallèle si les fichiers ne se recouvrent pas) ; `traducteur` pour les textes.
3. `testeur`.
4. `relecteur`.
5. `documentaliste` : fiche listant tous les agents utilisés.

## Règles

- Une petite tâche (quelques lignes, un fichier) se fait directement, sans agent.
- Donner à chaque agent un brief complet : objectif, fichiers concernés, décisions déjà prises (il ne voit pas la conversation).
- Aucun agent ne crée de branche ni ne committe.
