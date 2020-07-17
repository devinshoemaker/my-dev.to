---
published: true
title: '@nxtend/ionic-react 3.0.3'
cover_image:
description:
tags: ionic, react, nx, webdev
series:
canonical_url: https://nxtend.dev/blog/ionic-react-3.0.3/
---

This version of the `@nxtend/ionic-react` plugin includes a few quality of life improvements regarding dependency management.

## Bug Fixes

- add `@nrwl/react` version based on the users Nx version
- don't unnecessarily add `@nxtend/ionic-react` dependency in `init` schematic
- add `@nxtend/capacitor` 1.0.0 instead of `*`

Previously, `@nxtend/ionic-react` would add the latest version of `@nrwl/react` to the users `package.json` which could cause issues if the user was using an older version of Nx. Now, the plugin will look at the users local version of Nx and will install the same version of `@nrwl/react`.

An update has also been made that avoids adding `@nxtend/ionic-react` unnecessarily when using `ng add`.

Finally, the plugin will install version 1.0.0 of `@nxtend/capacitor` instead of version `*`.

For information on upgrading the plugin, visit the [nxtend upgrades documentation](https://nxtend.dev/docs/nxtend/upgrades).
