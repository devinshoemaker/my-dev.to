---
published: true
title: 'Release @nxtend/ionic-react 3.1.0'
cover_image:
description:
tags: ionic, react, nx, webdev
series:
canonical_url: https://nxtend.dev/blog/ionic-react-3.1.0/
---

This is a pretty typical maintenance release with a few package updates. The most notable change is `@testing-library/cypress` which introduces some breaking changes which you can read about below, or in the [release notes](https://github.com/testing-library/cypress-testing-library/releases/tag/v7.0.0).

# Features

- update `@nxtend/capacitor` to 1.1.0
- update Ionic to 5.3.2
- update Ionicons to 5.1.2
- update `@testing-library/cypress` to 7.0.0
- update `@testing-library/jest-dom` to 5.11.4
- update `@testing-library/user-event` to 12.1.5

# BREAKING CHANGES

- `@testing-library/cypress`
  - `get` and `query` queries (which have been deprecated) have now been removed. Use `find` queries only.
  - **TS**: TypeScript type definitions have been brought into this module and no longer needs to be referenced from DefinitelyTyped

For information on upgrading the plugin, visit the [nxtend upgrades documentation](https://nxtend.dev/docs/nxtend/upgrades).
