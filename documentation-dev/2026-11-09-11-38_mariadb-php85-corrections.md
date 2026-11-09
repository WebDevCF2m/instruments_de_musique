# Passage à MariaDB + PHPMyAdmin, PHP 8.5, correction CLAUDE.md

- **Date** : 2026-11-09 11:38
- **Branche** : feature/02-new-claude-files
- **Demande** : corriger les 3 incohérences relevées dans la fiche `2026-11-09-11-34_fichiers-md-claude.md`

## Fichiers

| Action | Fichier | Rôle |
|--------|---------|------|
| modifié | `compose.yaml` | service `database` : PostgreSQL 16 → MariaDB 10.11 (même version que `serverVersion` dans `.env`) |
| modifié | `compose.override.yaml` | port 3306 exposé en `3306:3306` + service `phpmyadmin` sur http://localhost:8080 |
| modifié | `README.md` | installation PHP 8.4 → 8.5 ; paquet `mysql` ajouté, `opcache` retiré (intégré à PHP 8.5, plus de paquet séparé) |
| modifié | `CLAUDE.md` | faute de frappe `template.html.twwig` → `template.html.twig` |

## Raisons

- `CLAUDE.md` et `.env` prévoyaient MariaDB + PHPMyAdmin, mais Docker lançait PostgreSQL.
- Le port 3306 est fixe pour que le `DATABASE_URL` de `.env` (`127.0.0.1:3306`) fonctionne aussi avec `php bin/console`.
- PHP 8.5.4 est la version installée dans WSL ; `pdo_mysql` est nécessaire pour MariaDB.

## Agents utilisés

- aucun

## Commandes lancées

    docker compose config --quiet   # validation des fichiers compose : OK
    php -v ; php -m                  # PHP 8.5.4, pdo_mysql et OPcache présents

## À faire / points d'attention

- Si un conteneur PostgreSQL existe déjà : `docker compose down -v` (supprime l'ancien volume) puis `docker compose up -d`.
- Le port 3306 ne doit pas être déjà pris par un MySQL/MariaDB local.
- `config/packages/doctrine.yaml` garde une ligne `PostgreSQLPlatform: identity` : sans effet sous MariaDB, elle peut rester.
