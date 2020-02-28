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
  - Generating application
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
  - nxtend GitHub and NPM links
  - Nx GitHub issue link
  - Ionic
  - Nx

I am extremely excited to announce the release of my new Nx plugin `@nxtend/ionic-react`. With this plugin, it is easier than ever to develop Ionic React applications in an Nx workspace.

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