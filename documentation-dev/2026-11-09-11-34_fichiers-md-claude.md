# Création des fichiers .md de fonctionnement de Claude

- **Date** : 2026-11-09 11:34
- **Branche** : feature/02-new-claude-files
- **Demande** : préparer les fichiers .md nécessaires au fonctionnement de Claude Code sur le projet

## Fichiers

| Action | Fichier | Rôle |
|--------|---------|------|
| créé | `documentation-dev/README.md` | explique la convention de nommage et le contenu des fiches |
| créé | `documentation-dev/_modele.md` | modèle à copier pour chaque fiche |
| créé | `documentation-dev/2026-11-09-11-34_fichiers-md-claude.md` | cette fiche |
| créé | `.claude/rules/conventions-symfony.md` | règles de code (langue, Symfony, Twig, médias) chargées automatiquement par Claude Code |
| créé | `.claude/skills/documenter/SKILL.md` | compétence `/documenter` pour rédiger une fiche en fin de tâche |
| modifié | `README.md` | suite de l'Etape 3 |

## Raisons

- `CLAUDE.md` impose de documenter chaque modification dans `documentation-dev/` : le dossier, sa convention et un modèle sont nécessaires.
- `CLAUDE.md` reste court (contexte du projet) ; les conventions de code détaillées vont dans `.claude/rules/`.
- La compétence `documenter` rend la rédaction des fiches systématique et homogène.

## Agents utilisés

- aucun

## Commandes lancées

    git branch --show-current
    git status --short

## À faire / points d'attention

- `compose.yaml` utilise encore PostgreSQL 16 alors que `CLAUDE.md` et `.env` prévoient MariaDB + PHPMyAdmin : à mettre à jour.
- `README.md` installe PHP 8.4 alors que `CLAUDE.md` indique PHP 8.5.
- Faute de frappe dans `CLAUDE.md` : `template.html.twwig` → `template.html.twig`.
