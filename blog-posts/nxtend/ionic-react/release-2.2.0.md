---
published: false
title: "@nxtend/ionic-react 2.2.0"
cover_image:
description:
tags: ionic, react, nx, webdev
series:
canonical_url:
---

(This has been cross-posted from the official [nxtend](https://nxtend.dev) website)

It's been a while since the last `@nxtend/ionic-react` release, and as always, there is a lot in the works. Going forward, I plan to release more frequently and in smaller iterations.

## Bug Fixes

- fix pascal case generate App unit test
- fix generating global styles for Emotion

## Features

- upgrade Ionic to 5.2.2
- add `--disableSanitizer` flag to application schematic to disable the [Ionic sanitizer](https://ionicframework.com/docs/techniques/security#sanitizing-user-input)

The Ionic framework has a built-in input sanitizer, however, they recently added the ability to disable this feature entirely. The `--disableSanitizer` flag for the `application` schematic will disable this feature when generating the initial app.

I have upgraded the Ionic dependencies to `^5.2.2` in order to make user upgrades easier. I plan to continue to update dependencies with each release, but now users can upgrade compatible versions with their Node package manager.

## How to Upgrade

The `@nxtend/ionic-react` plugin releases with migrations for each release. The recommended way to upgrade is with the Nx or Angular CLI depending on how your project is configured. Where possible, nxtend will keep your relevant dependencies and configs updated.

Nx CLI:

```
nx migrate @nxtend/ionic-react

# yarn project
yarn

# npm project
npm install

nx migrate --run-migrations migrations.json

# yarn project
yarn

# npm project
npm install
```

Angular CLI.

```
ng update @nxtend/ionic-react
```
