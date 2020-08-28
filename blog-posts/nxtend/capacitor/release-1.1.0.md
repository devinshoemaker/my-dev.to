---
published: true
title: "Release @nxtend/capacitor 1.1.0"
cover_image:
description:
tags: ionic, capacitor, nx, webdev
series:
canonical_url: https://nxtend.dev/blog/capacitor-1.1.0
---

This release upgrades Capacitor dependencies to 2.4.0, and also makes it easier to add Capacitor plugins to a project. Previously, the user would have to add a Capacitor plugin dependency to both the root workspace `package.json`, but also the individual Capacitor projects `package.json`. Now, a `package.json` in the individual Capacitor project is no longer needed.

## Features

- upgrade Capacitor to 2.4.0
- copy package.json from workspace root for cap commands

<!--truncate-->

This update should be a good quality of life improvement for developers using the `@nxtend/capacitor` plugin. If you have any issues or feedback then feel free to file an issue on the offical [GitHub repository](https://github.com/nxtend-team/nxtend).

For information on upgrading the plugin, visit the [nxtend upgrades documentation](https://nxtend.dev/docs/nxtend/upgrades).
