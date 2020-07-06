---
published: true
title: "Build Cross-Platform Applications in a Monorepo with Nx, Ionic, and Capacitor"
cover_image:
description: "Build cross-plaform applications in an Nx monorepo workspace using Ionic and Capacitor Nx community plugins"
tags: ionic, capacitor, nx, webdev
series:
canonical_url:
---

# Background and Motivation

A few months ago I released an Ionic React plugin for Nx. While I really enjoy using Ionic for its comprehensive component library, the project is not nearly as complete without Capacitor.

Capacitor is developed by the Ionic team but it does not require an Ionic project. Capacitor is framework agnostic and should work with any app in an Nx workspace. If you would like to learn more about Capacitor then I suggest you check out the [official documentation](https://capacitor.ionicframework.com/docs/).

`@nxtend/ionic-react` enabled developers to create web apps that _looked_ native, `@nxtend/capacitor` enables developers to compile their web apps to a native platform such as iOS and Android.

# Usage

While the officially Capacitor CLI does not work well with an Nx workspace, I have tried to match the functionality with the plugin as much as possible.

The `@nxtend/capacitor` plugin will be added to your workspace and a Capacitor project will be automatically generated with a new `@nxtend/ionic-react` application. However, you can add Capacitor to an existing project.

## Add Capacitor to Existing Project

First, you need to initialize the `@nxtend/capacitor` plugin:

```
# Angular CLI
ng add @nxtend/capacitor
```

```
# Nx CLI

# npm
npm install --save-dev --exact @nxtend/capacitor

# yarn
yarn add --save-dev --exact @nxtend/capacitor

nx generate @nxtend/capacitor:init
```

Once the plugin has been added to your Nx workspace you can generate a Capacitor project from an existing frontend project:

```
nx generate @nxtend/capacitor:capacitor-project {Capacitor project name} --project {frontend project name}

nx generate @nxtend/capacitor:capacitor-project mobile-app-cap --project mobile-app
```

## Add Native Platforms

Now that a Capacitor project has been added to your Nx workspace you can begin adding support for native platforms. Currently, Capacitor supports Android and iOS with Electron support being in beta.

```
nx run {Capacitor project name}:add {native platform}

nx run mobile-app-cap:add android
```

## Sync Native Platform

Running the sync command will update the native platform dependencies and copy a build of your frontend project to the Capacitor project:

```
nx run {Capacitor project name}:sync {native platform}

nx run mobile-app-cap:sync android
```

## Open Native Platform

Finally, you can open the native platform:

```
nx run {Capacitor project name}:open {native platform}

nx run mobile-app-cap:open android
```

# Conclusion

The `@nxtend/capacitor` plugin enables any project in an Nx workspace to be compiled to a native platform. Combined with `@nxtend/ionic-react` you can create high-quality cross-platform applications in an Nx monorepo.

I highly recommend looking at the [official Capacitor documentation](https://capacitor.ionicframework.com/docs/) for more information.

# Resources

[Ionic Framework](https://ionicframework.com/docs)
[Capacitor](https://capacitor.ionicframework.com/docs/)
[@nxtend/ionic-react](https://github.com/devinshoemaker/nxtend/tree/master/libs/ionic-react)
[@nxtend/capacitor](https://github.com/devinshoemaker/nxtend/tree/master/libs/capacitor)
