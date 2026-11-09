# Ajout de l'agent designer

- **Date** : 2026-11-09 12:12
- **Branche** : feature/02-new-claude-files
- **Demande** : ajouter un agent designer

## Fichiers

| Action | Fichier | Rôle |
|--------|---------|------|
| créé | `.claude/agents/designer.md` | opus : charte graphique, variables CSS, maquettes, relecture visuelle |
| modifié | `.claude/rules/dispatch-agents.md` | designer ajouté au tableau et en étape 2 de l'enchaînement type |

## Raisons

- L'identité visuelle est une décision structurante, qui conditionne tout le travail d'intégration : modèle **opus**, comme `architecte`.
- Séparation des rôles : le `designer` décide (tokens CSS dans `assets/styles/tokens.css`, charte dans `documentation-dev/charte-graphique.md`, maquettes dans `documentation-dev/maquettes/`) ; `integrateur-twig` (sonnet) réalise les templates et composants.
- Contrairement à `architecte`, il peut écrire des fichiers, mais seulement CSS, documentation de charte et maquettes.
- Exigences d'accessibilité (contraste WCAG AA, focus visible, zones cliquables 44 px) intégrées dès la conception.

## Agents utilisés

- aucun

## Commandes lancées

    # vérification de l'en-tête de designer.md : OK

## À faire / points d'attention

- `assets/styles/app.css` contient encore le style de démo (`background-color: skyblue`) : à remplacer lors du premier passage du designer.
- Relancer Claude Code (ou `/agents`) pour que l'agent soit pris en compte.
