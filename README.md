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

## Get Started

There are a few ways to get started with Drupal:

1. [User Guide:](https://www.drupal.org/docs/user_guide/en/index.html) Includes installing, administering, site building, and maintaining the content of a Drupal website.
2. [Create Content:](https://wmsc-drupal.ddev.site/node/add) Want to get right to work? Start adding content. **Note:** the information on this page will go away once you add content to your site. Read on and bookmark resources of interest.
3. [Extend Drupal:](https://www.drupal.org/docs/extending-drupal) Drupal’s core software can be extended and customized in remarkable ways. Install additional functionality and change the look of your site using addons contributed by our community.