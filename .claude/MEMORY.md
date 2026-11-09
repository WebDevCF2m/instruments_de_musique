# Mémoire partagée du projet

Chargée à chaque session via `CLAUDE.md` (`@.claude/MEMORY.md`), versionnée avec le projet.
Elle complète `CLAUDE.md` (contexte, stack, règles) sans le répéter : ici l'**état d'avancement**, les **décisions prises** et les **pièges connus**.

**Mise à jour** : à la fin de chaque tâche, en même temps que la fiche `documentation-dev/` (agent `documentaliste`). Rester court : le détail est dans les fiches et dans git.

---

## État d'avancement

*Dernière mise à jour : 2026-11-09 12:20, branche `feature/02-new-claude-files`*

### Où on s'est arrêté (session du 2026-11-09)

- Fin de session : conteneurs arrêtés (`docker compose down`), base conservée dans le volume `instruments_de_musique_database_data`.
- Branche `feature/02-new-claude-files` : dernier commit `64b5dae` (agent designer), en avance d'un commit sur `origin` (pas encore poussé).
- **Non commité** à la fin de la session : `.claude/MEMORY.md` (nouveau), `CLAUDE.md` (import de la mémoire), `README.md` (arrêt de Docker), `.claude/agents/documentaliste.md` et `.claude/skills/documenter/SKILL.md` (mise à jour de la mémoire), fiches `documentation-dev/2026-11-09-12-16_*` et `2026-11-09-12-19_*`.
- À vérifier au démarrage de la session suivante : `git status`, `/memory` (cette mémoire est chargée ?), `/agents` (8 agents présents ?).

### Pour reprendre

1. Démarrer Docker Desktop, puis `docker compose up -d` dans WSL.
2. Si les fichiers ci-dessus ont été commités : fusionner `feature/02-new-claude-files` dans `main`, puis créer la branche de l'étape suivante (ex. `feature/03-charte-graphique`). Claude ne crée ni branche ni commit.
3. Lancer la première « Prochaine étape » ci-dessous.

| Étape | Branche | État |
|-------|---------|------|
| 1. Installation Symfony 7.4 LTS webapp | `main` | fait |
| 2. Initialisation de Claude Code, `CLAUDE.md` | `feature/01-install-claude` | fait |
| 3. Fichiers Claude (`documentation-dev/`, règles, compétence, agents) | `feature/02-new-claude-files` | fait |
| 4. Docker : PHP 8.5, MariaDB, PHPMyAdmin, Mailpit | `feature/02-new-claude-files` | fait et testé |
| Charte graphique | — | à faire (agent `designer`) |
| Modèle de données (sections, instruments, médias, commentaires, utilisateurs) | — | à faire (agent `architecte`) |

Le code applicatif est encore vide : aucune entité, aucun contrôleur, aucune migration. `assets/styles/app.css` contient le style de démo (`skyblue`).

## Prochaines étapes envisagées

1. `designer` : charte graphique (`assets/styles/tokens.css`, `documentation-dev/charte-graphique.md`).
2. `architecte` : modèle de données et sécurité (utilisateurs, `ROLE_ADMIN`, validation des commentaires, upload photos/sons).
3. `base.html.twig` → `template.html.twig`, page d'accueil (historique de la famille des bois), traductions `fr`.

## Environnement

Démarrer Docker Desktop, puis dans WSL (`~/instruments_de_musique`) :

    docker compose up -d
    docker compose exec php php bin/console <commande>

| Service | Adresse | Détail |
|---------|---------|--------|
| Site (PHP 8.5 + Apache) | http://localhost:8000 | image `docker/php/Dockerfile` |
| PHPMyAdmin | http://localhost:8080 | serveur `database` |
| Mailpit | http://localhost:8025 | SMTP interne `mailer:1025` |
| MariaDB 10.11 | `127.0.0.1:3306` | base `app`, utilisateur `app` |

## Décisions prises

- Tout tourne dans Docker ; le conteneur `php` surcharge `DATABASE_URL` (hôte `database`) et `MAILER_DSN` (`smtp://mailer:1025`). Le `.env` (`127.0.0.1:3306`) reste valable depuis WSL.
- Ports fixes : 8000 (site), 8080 (PHPMyAdmin), 8025 (Mailpit), 3306 (MariaDB).
- `www-data` du conteneur a l'UID 1000 (utilisateur WSL) : pas de problème de droits sur `var/`.
- Pas de `symfony/apache-pack` : Apache utilise `FallbackResource /index.php`.
- Travail réparti entre 8 agents selon la difficulté (haiku / sonnet / opus) : voir `.claude/rules/dispatch-agents.md`.

## Pièges connus

- Docker Desktop doit être démarré, sinon `docker compose` échoue (`dockerDesktopLinuxEngine` introuvable).
- Le port 8000 est aussi celui de `symfony serve` : utiliser l'un ou l'autre.
- Les mails de l'application partent par Messenger (`async`) : rien n'arrive dans Mailpit sans `docker compose exec php php bin/console messenger:consume async`. `mailer:test` envoie directement.
- PHP 8.5 : OPcache est intégré, le paquet `php8.5-opcache` n'existe plus ; `php8.5-mysql` est nécessaire hors Docker.
- `config/packages/doctrine.yaml` garde une ligne `PostgreSQLPlatform: identity` héritée du squelette : sans effet sous MariaDB.

## Reprendre sur une autre machine

1. Installer WSL2 Ubuntu, Docker Desktop (intégration WSL activée), Claude Code (voir `README.md`).
2. `git clone https://github.com/WebDevCF2m/instruments_de_musique` dans WSL, puis se placer sur la dernière branche de travail.
3. `docker compose build && docker compose up -d`
4. `docker compose exec php composer install`
5. `docker compose exec php php bin/console doctrine:migrations:migrate --no-interaction` (dès qu'il y aura des migrations).
6. Lancer `claude` dans le dossier : `CLAUDE.md`, cette mémoire, les règles et les agents sont chargés automatiquement.
