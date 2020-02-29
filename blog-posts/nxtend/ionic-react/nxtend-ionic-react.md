---
published: false
title: "Developing Ionic React Apps in Nx with @nxtend/ionic-react"
cover_image:
description: "Using the Nx plugin @nxtend/ionic-react to develop Ionic React applications in an Nx workspace"
tags: ionic, react, nx, webdev
series:
canonical_url:
---

# Outline

- Introduction
- Background and Motivation
- Usage
- Future Development
  - Libraries
    - One of the next features that I will be working on is the ability to generate an Ionic React library.
  - Pages
    - The Ionic CLI offers a `page` schematic for Angular applications, so I intend to offer similar functionality for this plugin.
  - Starters
    - The Ionic CLI allows you to generate a new application with one of several starter templates. Over time, I intend to add support for each of these official templates.
  - Plugins
    - `@nxtend/ionic-react` is just the beginning. I have plans for entirely new Nx plugins that I will publish under the `@nxtend` scope, but you'll have to stay tuned for more information on that. 😁
- Conclusion
  - I have had an amazing time working with Nx and schematics and I can't wait to iterate on this project
  - If anyone finds an issue with the project, or has a suggestion, don't hesitate to reach out on GitHub.
- Resources

I am extremely excited to announce the release of my new [Nx](https://nx.dev) plugin `@nxtend/ionic-react`. With this plugin, it is easier than ever to develop [Ionic React](https://ionicframework.com/docs/react/your-first-app) applications in an Nx workspace.

# Background and Motivation

I have been a fan of both Ionic and Nx for a while now, so once both of these projects added React support, they seemed like a natural pair. However, when I attempted to convert an Nx React application, I quickly ran into issues. With the help of the community and the Nrwl team, we are now able to develop Ionic React applications in an Nx workspace. Over the last few weeks, I have been developing an Nx plugin to automate the generation of an Ionic React application, and I'm excited to finally share it.

# Usage

Adding the `@nxtend/ionic-react` plugin to your Nx workspace is trivial, and works just like any other Nx plugin.

If you use the Angular CLI, run:

```
ng add @nxtend/ionic-react
```

If you use the Nx CLI and Yarn, run:

```
yarn add --dev @nxtend/ionic-react
```

If you use the Nx CLI and NPM, run:

```
npm install --save-dev @nxtend/ionic-react
```

Now, create your Ionic React application.

```
nx generate @nxtend/react:application myApp
```

Nx will ask you some questions about the application, but you can customize it further by passing these options:

```
nx generate @nxtend/ionic-react:application [name] [options,...]

Options:
  --name                  The name of the application.
  --directory             The directory of the new application.
  --style                 The file extension to be used for style files. (default: css)
  --linter                The tool to use for running lint checks. (default: tslint)
  --skipFormat            Skip formatting files
  --skipWorkspaceJson     Skip updating workspace.json with default schematic options based on values provided to this app (e.g. babel, style)
  --unitTestRunner        Test runner to use for unit tests (default: jest)
  --e2eTestRunner         Test runner to use for end to end (e2e) tests (default: cypress)
  --tags                  Add tags to the application (used for linting)
  --pascalCaseFiles       Use pascal case component file name (e.g. App.tsx)
  --classComponent        Use class components instead of functional component
  --js                    Generate JavaScript files rather than TypeScript files
  --dryRun                undefined
  --help                  Show available options for project target.
```

# Resources

nxtend GitHub: https://github.com/devinshoemaker/nxtend<br>
NPM Package: https://www.npmjs.com/package/@nxtend/ionic-react<br>
Nx: https://nx.dev<br>
Ionic Framework: https://ionicframework.com<br>
Original GitHub Issue: https://github.com/nrwl/nx/issues/1931
