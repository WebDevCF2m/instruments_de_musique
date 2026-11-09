---
name: documenter
description: Rédige la fiche de documentation d'une modification dans documentation-dev/ (format YYYY-MM-DD-HH-MM_description-courte.md). À utiliser à la fin de chaque tâche qui crée, modifie ou supprime des fichiers du projet.
---

# Documenter une modification

1. Récupérer la date et l'heure : `date '+%Y-%m-%d-%H-%M'`, et la branche : `git branch --show-current`.
2. Lister les fichiers touchés : `git status --short` (ne garder que ceux modifiés pendant la tâche).
3. Créer `documentation-dev/<date>_<description-courte>.md` en suivant `documentation-dev/_modele.md` :
   - description courte en minuscules, avec tirets, sans accents ;
   - remplir date, branche, fichiers, raisons, agents utilisés (« aucun » si aucun sous-agent), commandes lancées.
4. Mettre à jour `.claude/MEMORY.md` (état d'avancement, prochaines étapes, décisions, pièges connus).
5. Ne pas créer de branche ni de commit : indiquer à l'utilisateur les fichiers à vérifier avant qu'il committe.
