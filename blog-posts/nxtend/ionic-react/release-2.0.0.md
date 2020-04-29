---
published: false
title: "Release @nxtend/ionic-react 2.0.0"
cover_image:
description: "Bugs have been fixed, dependencies have been updated, and even Ionic has made updates to their starter templates"
tags: ionic, react, nx, webdev
series:
canonical_url:
---

I have been hard at work on `@nxtend/ionic-react` since the initial relese, and I'm happy to announce that version 2.0.0 is now available. Bugs have been fixed, dependencies have been updated, and even Ionic has made updates to their starter templates.

## Features

- extend `@nrwl/react` schematics
- import `@testing-library/jest-dom` commands for unit tests
- upgrade `@testing-library/jest-dom` to 5.5.0
- upgrade `@testing-library/cypress` to 6.0.0
- upgrade `@testing-library/user-event` to 10.0.1
- honor `unitTestRunner` flag
- set `@nxtend/ionic-react` as the default collection if one is not set when generating an application
- honor `skipFormat` flag
- update Ionic starter template
  - [#1201](https://github.com/ionic-team/starters/pull/1201)
  - [#1202](https://github.com/ionic-team/starters/pull/1202)
  - [#1237](https://github.com/ionic-team/starters/pull/1237)

I originally used the same dependency versions that ship with Ionic, however, several of them were getting rather out of date. I decided to update all of the `@testing-library/*` dependencies and will continue to maintain those updates with future releases.

Ionic React ships with `@testing-library/jest-dom` configured, and while `@nxtend/ionic-react` shipped with the dependency, it was not actually being used in v1.0.0. This library will now be configured for all `@nxtend/ionic-react` applications going forward.

The Ionic team have made several minor revisions to their starter templates, and this has been reflected in this project. If you would like to incorporate these changes then feel free to look at the [migration guide](https://github.com/devinshoemaker/nxtend/blob/%40nxtend/ionic-react%402.0.0/libs/ionic-react/MIGRATION.md) provided.

I extended the `@nrwl/react` schematics so that all `generate` commands fallback onto that plugin. Essentially, even though `@nxtend/ionic-react` does not have a `component` schematic, you can still generate one with this plugin since `@nrwl/react` has one available. The plugin also now sets `@nxtend/ionic-react` as the default schematic if one is not yet set.

Due to the breaking changes in the `@testing-library/*` dependencies, extending the `@nrwl/react` schematics, as well as the changes to default schematics, it warranted a major release.

I have a number of features plannned for upcoming releases and I can't wait to share it with you all. Feel free to reach out to me on Twitter if you have questions or anything else!

# Resources

nxtend GitHub: https://github.com/devinshoemaker/nxtend<br>
NPM Package: https://www.npmjs.com/package/@nxtend/ionic-react<br>
Nx: https://nx.dev<br>
Ionic Framework: https://ionicframework.com
