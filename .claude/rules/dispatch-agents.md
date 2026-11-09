# Répartition du travail entre les agents

Les agents sont définis dans `.claude/agents/`. Le modèle suit la difficulté de la tâche.

| Difficulté | Modèle | Agent | Pour |
|------------|--------|-------|------|
| simple | haiku | `documentaliste` | fiches `documentation-dev/`, étapes du README |
| simple | haiku | `traducteur` | fichiers `translations/`, textes Twig → clés `|trans` |
| moyenne | sonnet | `dev-symfony` | entités, migrations, contrôleurs, formulaires, CRUD, upload |
| moyenne | sonnet | `integrateur-twig` | templates, composants UX, Stimulus, CSS |
| moyenne | sonnet | `testeur` | tests PHPUnit |
| difficile | opus | `designer` | charte graphique, variables CSS, maquettes, relecture visuelle |
| difficile | opus | `architecte` | conception, modèle de données, sécurité, bugs difficiles (plan, sans modifier) |
| difficile | opus | `relecteur` | relecture avant commit (sans modifier) |

## Enchaînement type d'une fonctionnalité

1. `architecte` si la tâche est floue ou touche au modèle de données / à la sécurité.
2. `designer` si la fonctionnalité ajoute une page ou un composant visuel (maquette + variables CSS).
3. `dev-symfony` puis `integrateur-twig` (en parallèle si les fichiers ne se recouvrent pas) ; `traducteur` pour les textes.
4. `testeur`.
5. `relecteur`.
6. `documentaliste` : fiche listant tous les agents utilisés.

## Règles

- Une petite tâche (quelques lignes, un fichier) se fait directement, sans agent.
- Donner à chaque agent un brief complet : objectif, fichiers concernés, décisions déjà prises (il ne voit pas la conversation).
- Aucun agent ne crée de branche ni ne committe.
