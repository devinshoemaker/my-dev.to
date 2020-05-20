---
published: true
title: "Extending Schematics in an Nx Plugin"
cover_image:
description: "Build an Nx Plugin that extends a different libraries schematics"
tags: nx, schematics, monorepo, webdev
series:
canonical_url:
---

[Nx Plugins](https://nx.dev/nx-community) allow you to develop custom schematics for an Nx workspace, but maybe you just want to extend an existing set of schematics with some slight tweaks. [Schematics](https://angular.io/guide/schematics-authoring) feature this out of the box and it can be a good addition to your Nx Plugin.

For example, if your organization uses React and has a standard set of changes that are always made to new applications, but otherwise use the `@nrwl/react` schematics, you could extend the `@nrwl/react` schematics and customize only the `application` schematic. Any schematics other than the ones that have been overridden will fall back to the library that you have extended from.

## Implementation

Add an `extends` property in your plugins `collection.json` that contains an array of libraries you are overriding schematics from. Here is an example from my `@nxtend/ionic-react` Nx Plugin that overrides `@nrwl/react`:

```
{
  "$schema": "../../node_modules/@angular-devkit/schematics/collection-schema.json",
  "name": "ionic-react",
  "version": "0.0.1",
  "extends": ["@nrwl/react"],
  "schematics": {
    "init": {
      "factory": "./src/schematics/init/schematic",
      "schema": "./src/schematics/init/schema.json",
      "description": "Initialize the @nxtend/ionic-react plugin",
      "aliases": ["ng-add"],
      "hidden": true
    },

    "application": {
      "factory": "./src/schematics/application/schematic",
      "schema": "./src/schematics/application/schema.json",
      "aliases": ["app"],
      "description": "Create an Ionic React application"
    }
  }
}
```

In the example above, I override both the `init` and `application` schematic, but otherwise, all other schematics will fall back to `@nrwl/react`. That means that `nx g @nxtend/ionic-react:component` will fall back to `@nrwl/react:component` since the `component` schematic was not overridden above.

You may have noticed that the field is an array. This means that you can extend multiple schematics schematics to provide a wide variety of fallback commands that fit your needs.

## References

[Nx Plugin Guide](https://nx.dev/react/plugins/nx-plugin/overview)<br>
[Authoring Schematics by Angular](https://angular.io/guide/schematics-authoring)<br>
[@nxtend/ionic-react](https://github.com/devinshoemaker/nxtend/tree/master/libs/ionic-react)
