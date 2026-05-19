# WMSC Drupal test

Drupal Core tryout for WMSC web site project

## Windows dev environment

Use WSL2, Docker, and DDEV according to prescribed setup:

https://www.drupal.org/docs/develop/local-server-setup/windows-development-environment/installing-drupal-with-ddev-in-wsl2-on-windows/installing-docker-ddev-drupal-in-wsl2

### Commands

Start Docker containers: `ddev start`
Stop all Docker containers: `ddev poweroff`
Display a one-time login link in terminal: `ddev drush uli`
Launch project in Edge browser: `ddev launch`
Start with BrowserSync: `ddev browsersync`

- Add `:3000` to URL for hot syncing in browser.
