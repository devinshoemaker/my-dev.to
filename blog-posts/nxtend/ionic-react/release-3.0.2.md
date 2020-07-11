---
published: true
title: "@nxtend/ionic-react 3.0.2"
cover_image:
description:
tags: ionic, react, nx, webdev
series:
canonical_url: https://nxtend.dev/blog/ionic-react-3.0.2/
---

This is a minor update to fix a bug where the user was forced to manually install the `@nxtend/capacitor` plugin before generating an application with `@nxtend/ionic-react`.

## Bug Fixes

- properly initialize Capacitor plugin

The `@nxtend/capacitor` plugin was not being initialized properly with the `@nxtend/ionic-react:init` schematic. This resulted in an error being thrown if an Ionic React application was attempted to be generated if `@nxtend/capacitor` had not been added to the users workspace manually.

This change ensures that the `@nxtend/capacitor` plugin is added to the users `package.json` and is initialized before generating an application with Capacitor enabled.

Unit and e2e tests have also been added to ensure this functionality doesn't break in the future.

For information on upgrading the plugin, visit the [nxtend upgrades documentation](https://nxtend.dev/docs/nxtend/upgrades).
