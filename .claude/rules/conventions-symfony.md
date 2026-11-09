# Conventions de code du projet

Complète `CLAUDE.md` (chargé automatiquement par Claude Code).

## Langue

- Textes visibles par l'utilisateur : en français, via `translations/` (fichiers `messages+intl-icu.fr.yaml`), jamais en dur dans les templates une fois la traduction mise en place.
- Noms de classes, propriétés, méthodes et routes : en anglais (convention Symfony). Commentaires : en français.

## Symfony

- Générer avec le maker-bundle (`php bin/console make:entity`, `make:controller`, `make:form`, `make:crud`…) puis adapter, plutôt qu'écrire de zéro.
- Toute modification d'entité → `make:migration` puis relire la migration avant `doctrine:migrations:migrate`.
- Routes par attributs `#[Route]`, avec un nom explicite (`app_instrument_show`…).
- Zone d'administration sous le préfixe `/admin`, protégée par `ROLE_ADMIN`.
- Commentaires des utilisateurs : enregistrés non publiés, visibles seulement après validation par un administrateur.

## Templates Twig

- `base.html.twig` → `template.html.twig` (mise en page commune) → templates des pages.
- Composants réutilisables avec Symfony UX (Twig Components / Live Components) plutôt que des `include` complexes.
- Pas de Node.js : dépendances JS via `php bin/console importmap:require <paquet>`.

## Médias

- Photos et extraits sonores des instruments : fichiers uploadés hors de `src/`, avec validation du type MIME et de la taille.

## Commandes

- Les commandes PHP / Symfony / Docker se lancent dans WSL (Ubuntu), pas dans PowerShell.
