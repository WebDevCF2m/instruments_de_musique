# Instruments de musique

Lien vers github du projet : https://github.com/WebDevCF2m/instruments_de_musique

## Raccourcis

[Raccourcis](RACCOURCIS.md)

#### Installation sous WSL2 de Windows 11 du projet instruments de musique:

Ouvrir Powershell et l'ouvrir (ou l'installer) ou n'importe quelle console

    wsl

    sudo apt update

    # PHP 8.5
    sudo apt install php8.5-common php8.5-{bcmath,bz2,curl,gd,gmp,intl,mbstring,mysql,readline,xml,zip}

    # node.js 22.22
    sudo apt install nodejs

    wget https://get.symfony.com/cli/installer -O - | bash
    # puis
    mv /home/VOTRE_LOGIN/.symfony5/bin/symfony /usr/local/bin/symfony

    npm install -g --allow-scripts=@anthropic-ai/claude-code @anthropic-ai/claude-code

    cd /home/VOTRE_LOGIN/

    symfony check:requirement

    # Modifier si nécessaire

    symfony new instruments_de_musique --version=lts --webapp
    # ou cloner le répertoire

    cd instruments_de_musique

## Etape 2 Initialisation de claude 

branche : feature/01-install-claude

    claude update
    claude

Suivre le serveur, puis dans Claude

    /init

Modification de `CLAUDE.md`pour donner `contexte` à notre projet

## Etape 3    

branche : feature/02-new-claude-files

    claude
    
Création des fichiers `.md` utilisés par Claude Code :

- `documentation-dev/` : journal des modifications faites par Claude (voir son `README.md` et le modèle `_modele.md`)
- `.claude/rules/conventions-symfony.md` : conventions de code chargées automatiquement
- `.claude/skills/documenter/SKILL.md` : commande `/documenter` pour rédiger une fiche en fin de tâche

## Etape 4 Docker : PHP 8.5, MariaDB, PHPMyAdmin, Mailpit

branche : feature/02-new-claude-files

Démarrer Docker Desktop, puis dans WSL :

    docker compose build
    docker compose up -d

    # commandes Symfony dans le conteneur PHP
    docker compose exec php php bin/console about

- site : http://localhost:8000
- PHPMyAdmin : http://localhost:8080
- Mailpit : http://localhost:8025
