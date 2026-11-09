# Port fixe pour l'interface web de Mailpit

- **Date** : 2026-11-09 12:02
- **Branche** : feature/02-new-claude-files
- **Demande** : fixer le port de Mailpit à 8025

## Fichiers

| Action | Fichier | Rôle |
|--------|---------|------|
| modifié | `compose.override.yaml` | service `mailer` : port `"8025"` (aléatoire) → `"8025:8025"` |
| modifié | `README.md` | Etape 4 : lien direct http://localhost:8025 |

## Raisons

- Le port de l'interface Mailpit changeait à chaque redémarrage ; une adresse fixe est plus simple, comme PHPMyAdmin sur 8080.
- Le port SMTP 1025 reste aléatoire côté hôte : le conteneur PHP envoie les mails via `smtp://mailer:1025` à l'intérieur du réseau Docker.

## Agents utilisés

- aucun

## Commandes lancées

    docker compose up -d mailer                 # conteneur recréé
    curl http://localhost:8025/                 # HTTP 200

## À faire / points d'attention

- Le port 8025 ne doit pas être déjà utilisé sur la machine.
