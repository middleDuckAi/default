# Evolution CMS Default Preset

Minimal project-layer preset for Evolution CMS 3.5.x. It is meant to be the small bootstrap kit for a new site: controllers, Blade views, theme assets, and preset metadata only.

## What This Preset Contains

```text
core/custom/
  .gitignore
  composer.json
  config/
    cms/settings/ControllerNamespace.php
  packages/default/src/
    composer.json
    DefaultServiceProvider.php
    Controllers/
      BaseController.php
      HomeController.php
    Seeders/
      HomeTemplateSeeder.php
views/
  home.blade.php
  layouts/base.blade.php
  partials/header.blade.php
themes/default/
  css/app.css
.gitignore
```

Evolution core, manager files, runtime cache, database files, and local secrets stay outside this repository.

## Install Through Evo Installer

The preset should be installed by the Evolution CMS installer, not applied manually as a second step. The installer creates the target project first, then copies this preset as the project-layer bootstrap. The preset does not install Extras by default.

### TUI Install

Use TUI mode when you want the installer to ask for database, admin user, language, and optional Extras. This is the shortest default-preset install:

```bash
evo install /path/to/my-site \
  --branch=3.5.x \
  --preset=evolution-cms-presets/default
```

For a local preset checkout during preset development:

```bash
evo install /tmp/default-preset-check \
  --branch=3.5.x \
  --preset=/path/to/default-preset
```

Choose "No" on the Extras prompt when you want a clean default-project baseline.

### CLI Install

Use CLI mode when you want a fully non-interactive install:

```bash
evo install /path/to/my-site \
  --cli \
  --branch=3.5.x \
  --db-type=sqlite \
  --db-name=database.sqlite \
  --admin-username=admin \
  --admin-email=admin@example.com \
  --admin-password=change-me \
  --admin-directory=manager \
  --language=uk \
  --preset=evolution-cms-presets/default
```

For local installer development from an installer checkout:

```bash
cd /path/to/installer
go run ./cmd/evo install /path/to/my-site \
  --cli \
  --branch=3.5.x \
  --db-type=sqlite \
  --db-name=database.sqlite \
  --admin-username=admin \
  --admin-email=admin@example.com \
  --admin-password=change-me \
  --admin-directory=manager \
  --language=uk \
  --preset=evolution-cms-presets/default
```

`evolution-cms-presets/default` is the preset source. The target project can still be committed and pushed as its own repository.

For local preset development, point the installer at the preset checkout:

```bash
go run ./cmd/evo install /tmp/default-preset-check \
  --cli \
  --branch=3.5.x \
  --db-type=sqlite \
  --db-name=database.sqlite \
  --admin-username=admin \
  --admin-email=admin@example.com \
  --admin-password=change-me \
  --admin-directory=manager \
  --language=uk \
  --preset=/path/to/default-preset
```

Use `--preset=evolution-cms-presets/default@dev` when you want the installer to pull a development branch or tag from GitHub.

After install, the generated project `.gitignore` keeps Evolution core, manager, runtime cache, local SQLite databases, and IDE files out of the site repository. A fresh `git status` should show only the project layer: `core/custom`, `views`, `themes/default`, `robots.txt`, and `.gitignore`.

## Development Contract

- Put PHP site logic in `core/custom/packages/default/src/`.
- Put frontend templates in `views/`.
- Put theme assets in `themes/default/`.
- Keep the preset minimal; project-specific content belongs in the site repo that consumes it.
- `HomeTemplateSeeder` assigns the default site template alias to `home`, so Evolution can resolve `views/home.blade.php`.

## Next Site Step

Use this preset as the stable base, then create project-specific branches or repositories that replace `default` naming, add real content views, and grow controllers only when the site needs them.
