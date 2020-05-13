---
published: true
title: "Executing External Schematics in an Nx Plugin"
cover_image:
description: "Learn how to execute an external schematic from within an Nx Plugin"
tags: nx, schematics, monorepo, webdev
series:
canonical_url:
---

[Nx plugins](https://nx.dev/nx-community) make it easy to execute an existing schematic. Examples of this can be seen in many of the official Nx plugins. For instance, both the `@nrwl/react` and `@nrwl/angular` application schematics execute the `@nrwl/cypress:cypress-project` schematic. With this approach, you can leverage the many schematics that Nrwl and other developers have created.

## Implementation

First, we need to import the function that lets us achieve this:

```
import { externalSchematic } from '@angular-devkit/schematics';
```

Next, you can execute the external schematic:

```
return externalSchematic('@nrwl/react', 'application', {
  ...options,
  routing: true,
  unitTestRunner: 'none',
  skipWorkspaceJson: true
});
```

The first argument in this function is the library containing the schematic that you wish to execute. The second is the actual schematic that you wish to execute. Finally, the third argument is an object containing the schema options that you wish to pass to the schematic.

In the example above from my `@nxtend/ionic-react` plugin, I am executing the official `@nrwl/react:application` schematic, spreading the options passed into the schematic I am building, and overriding a few of those options. This kind of approach can be incredibly useful for extending existing schematics and then making tweaks to them.

One thing to note is that your user must have the library containing the external schematic added to their `package.json`. It's common practice to add this library for the user in your schematic if they don't have it already. You can read about how to do this in my other blog post, [Building an Nx Plugin to Add Dependencies to a Project](https://dev.to/devinshoemaker/building-an-nx-plugin-to-add-dependencies-to-a-project-29ih).

## Conclusion

The ability to execute external schematics adds a whole new level of reusability within your own Nx plugins as well as the community as a whole. There's no need to reinvent the wheel, Nx plugins allow you to leverage what the community has already built.

## References

[Nx Plugin Guide](https://nx.dev/react/plugins/nx-plugin/overview)<br>
[Authoring Schematics by Angular](https://angular.io/guide/schematics-authoring)<br>
[@nxtend/ionic-react](https://github.com/devinshoemaker/nxtend/tree/master/libs/ionic-react)
