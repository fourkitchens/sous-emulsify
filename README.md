# Sous Emulsify Drupal Recipe

A recipe that installs Emulsify dependencies and sets Emulsify as the default theme.

## Supported baseline

Use the supported Minimal baseline in the [platform guide](https://github.com/fourkitchens/sous-drupal-project/blob/main/docs/PLATFORM.md),
with the Emulsify theme and Emulsify Tools packages declared in `composer.json`. Sous Admin and Sous Content Types are optional.

## Theme and authorization ownership

This recipe installs the Emulsify base theme and Tools integration, then selects
the base theme as Drupal's default frontend theme. The starter generates the
site-specific custom theme and installs its locked Node tooling; application
asset builds belong to that generated site. This recipe does not create roles
or assign permissions. New Sous installations receive the `superuser`
administrator role from Sous Admin; standalone theme users manage authorization
in their site's configuration or chosen administration recipe.

Existing sites keep the role previously supplied here: it retains the same
machine ID, UUID, settings, and assigned accounts. Updating recipe source does
not remove active configuration. Keep that role in the site's complete export;
do not delete or recreate it during this ownership move. A site missing the role
can explicitly adopt Sous Admin's
[native missing-role migration](https://github.com/fourkitchens/sous-admin/tree/main/migrations/2026-10-superuser-role)
after reviewing the authorization decision. Package updates do not automatically
apply recipe configuration or migrations.

## Installing this Recipe

These examples select the current unreleased implementation on `dev-main`.
Run them in a configured consuming site, not in this recipe source checkout.
[Setup and recipe prerequisites](https://github.com/fourkitchens/sous-drupal-project/blob/main/docs/SETUP.md) define the required
repositories, installer paths, core unpacking plugin, and explicit root stability
exceptions. Use reviewed stable tags once the coordinated releases exist.

`ddev composer require fourkitchens/sous-emulsify:dev-main`

## Applying this Recipe

If you used the Sous Project as your starterkit:

- `ddev install-recipe fourkitchens/sous-emulsify`

Without the Sous DDEV command, use a configured consuming project and run from its root:

- `ddev drush recipe /var/www/html/web/recipes/sous-emulsify`
- `ddev drush cache:rebuild`

Use the [current native unpacking workflow](https://github.com/fourkitchens/sous-drupal-project/blob/main/docs/SETUP.md) before application.

## Development, integration, and releases

This repository is reusable recipe source, not a generated Drupal application.
Its Composer requirements and `recipe.yml` describe installation defaults; the
consuming project owns its runtime, complete configuration export, custom
theme, and application deployment. Requiring `dev-main` downloads remote source;
it does not test uncommitted sibling checkout changes.

Use the shared documentation instead of maintaining another setup procedure:

- [Supported runtime and package relationships](https://github.com/fourkitchens/sous-drupal-project/blob/main/docs/PLATFORM.md)
- [Fresh installation, contributor clones, restoration, and recovery](https://github.com/fourkitchens/sous-drupal-project/blob/main/docs/SETUP.md)
- [Sibling-source development and integration checks](https://github.com/fourkitchens/sous-drupal-project/blob/main/docs/INTEGRATION.md)
- [Configuration ownership and existing-site upgrades](https://github.com/fourkitchens/sous-drupal-project/blob/main/docs/MAINTENANCE.md)
- [Frontend development and production assets](https://github.com/fourkitchens/sous-drupal-project/blob/main/docs/BUILD_TOOLS.md)
- [Production deployment](https://github.com/fourkitchens/sous-drupal-project/blob/main/docs/DEPLOYMENT.md)
- [Coordinated releases and Conventional Commits](https://github.com/fourkitchens/sous-drupal-project/blob/main/docs/RELEASES.md)
- [Maintenance ownership and review cadence](https://github.com/fourkitchens/sous-drupal-project/blob/main/docs/OPERATIONS.md)

Recipe release tooling runs with the Node/npm versions pinned in `.nvmrc` and
`package.json`; Node is not required to execute a recipe in Drupal. The private
npm package publishes no browser assets or npm release. The thin workflow calls
the shared integration gate before the guarded GitHub publisher. Its central
workflow must be rolled out first; source configuration is not proof of a live
GitHub run or release. See the release guide for actual tag state, stable-tag
adoption, and explicit development exceptions.

Package updates do not automatically change configuration already applied to a
site. Preserve its complete export and adopt changes through reviewed native
configuration migrations and project-owned overrides. Do not routinely replay
the entire recipe on a customized site.

## License

Sous recipe source is licensed under [GPL-2.0-or-later](LICENSE). Dependencies
retain their own license terms; see the shared license policy in the platform
guide.
