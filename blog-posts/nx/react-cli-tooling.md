---
published: true
title: "Nx Brings High-Quality CLI Tooling to React"
cover_image:
description: "Nx Brings High-Quality CLI Tooling to React"
tags: nx, react, monorepo, webdev
series:
canonical_url:
---

I have been a fan of both Angular and React for a while now. I think both options have their strenghths and weaknesses, but one of the things that I (and many others) like most about Angular is its CLI. If you've never used Angular, then you probably don't know what you're missing. And if you've used Angular in the past then you likely miss the power that the CLI offers. While Nx offers many benefits beyond this, one of my favorite features is that it brings the power of the Angular CLI to React and other frameworks through plugins.

For those unfamiliar with the Angular CLI, it can:

- Generate new applications
- Generate new components and other pieces of code in a consistent manner with [schematics](https://angular.io/guide/schematics-authoring)
- Unify serve, test, lint, etc., commands with [builders](https://angular.io/guide/cli-builder)
- Update dependencies and files with migrations
- Be extended with third-party libraries that integrate with the CLI

The Nx CLI uses the same technology and helps bring these features to any framework supported by first or third-party plugins. Here are a few things that you can generate with the standard [`@nrwl/react`](https://nx.dev/react/plugins/react/overview) plugin for Nx:

- Application
- Component
- Library
- Redux slice
- Storybook configuration

While these things may seem trivial, the reduced copy and paste can go a long way, and defaults for these commands can be set in the Nx `workspace.json`.

Nx was originally developed for Angular, but over time it has embraced React and other frameworks in an agnostic way and I highly recommend React developers look at this technology for their next project. If you're interested in learning more then I suggest following the official [Nx React tutorial](https://nx.dev/react/tutorial/01-create-application).

An important thing to note is that Nx is not a framework and does not intend to be one. In fact, Nx currently supports both create-react-app style applications with the `@nrwl/react` plugin, as well as Next.js and Gatsby with `@nrwl/next` and `@nrwl/gatsby` respectively.
