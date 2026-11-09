# Mémoire partagée du projet

- **Date** : 2026-11-09 12:16
- **Branche** : feature/02-new-claude-files
- **Demande** : créer une mémoire partagée `.claude/MEMORY.md` pour reprendre le projet dans une autre session ou sur une autre machine

## Fichiers

| Action | Fichier | Rôle |
|--------|---------|------|
| créé | `.claude/MEMORY.md` | état d'avancement, prochaines étapes, environnement, décisions, pièges connus, reprise sur une autre machine |
| modifié | `CLAUDE.md` | section « Mémoire partagée » avec l'import `@.claude/MEMORY.md` |
| modifié | `.claude/agents/documentaliste.md` | met à jour la mémoire en fin de tâche (autorisé à modifier `.claude/MEMORY.md`) |
| modifié | `.claude/skills/documenter/SKILL.md` | étape « mettre à jour `.claude/MEMORY.md` » |

## Raisons

- Claude Code ne lit pas `.claude/MEMORY.md` tout seul : l'import `@.claude/MEMORY.md` dans `CLAUDE.md` le charge à chaque session.
- La mémoire automatique de Claude Code reste sur le poste (`~/.claude/projects/...`) ; ce fichier, lui, est versionné et suit le projet sur GitHub.
- `CLAUDE.md` garde le contexte stable (projet, stack, règles) ; `MEMORY.md` contient ce qui évolue (avancement, décisions, pièges).
- La mise à jour est rattachée à la fiche de documentation pour ne pas être oubliée.

## Agents utilisés

- aucun

## Commandes lancées

    git branch -a ; git log --oneline -5   # pour l'état d'avancement

## À faire / points d'attention

- Committer `.claude/MEMORY.md` et `CLAUDE.md` pour que la mémoire soit disponible sur les autres machines.
- Vérifier au prochain lancement avec `/memory` que `.claude/MEMORY.md` apparaît bien dans les fichiers chargés.
