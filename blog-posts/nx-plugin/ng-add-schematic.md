---
published: false
title: "Creating an ng add Schematic for an Nx Plugin"
cover_image:
description: "Learn how to build an Nx Plugin that supports `ng add`"
tags: nx, nxplugins, monorepo, webdev
series:
canonical_url:
---

[Nx community plugins](https://nx.dev/nx-community) are a powerful new technology by Nrwl that allows you to customize the functionality of Nx. If you have not yet watched Nrwl's official [Nx Plugin guide](https://nx.dev/react/plugins/nx-plugin/overview) then I highly recommend starting there.

You may be familiar with the `ng add` command from the Angular CLI. This allows you to easily add a dependency and add any necessary files or configurations with a single command. `@angular/material` is a great example of a library that utilizes this technology. Not only will `ng add @angular/material` update your `package.json` with the latest version of the library, but it will add the configurations you need and prompt you for additional customization. Since Nx relies heavily on Angular schematics, this functionality is fully supported in Nx Plugins.

## Angular CLI vs Nx CLI

When using an Nx workspace, you have the choice of using the [Angular CLI](https://cli.angular.io/) or the [Nx CLI](https://nx.dev/react/cli/overview). While the commands for both CLI's are very similar, there are some minor differences, and one of them is with the `ng add` command.

First of all, the Nx CLI does not automatically add the dependency to your `package.json`, so the user must do that themselves. Second, the command is slightly different and executes an `init` schematic. Under the hood, `ng add` schematics are named `init` with an `ng-add` alias to support the Angular CLI.

Angular CLI:

```
ng add @nxtend/ionic-react
```

Nx CLI:

```
// npm
npm install --dev --exact @nxtend/ionic-react

// yarn
yarn install --dev --exact @nxtend/ionic-react

nx g @nxtend/ionic-react:init
```

## Implementation

First, you'll want to edit `collection.json` and add a new schematic named `init` with an alias of `ng-add`:

```
"schematics": {
  "init": {
    "factory": "./src/schematics/init/schematic",
    "schema": "./src/schematics/init/schema.json",
    "description": "Initialize the @nxtend/ionic-react plugin",
    "aliases": ["ng-add"],
    "hidden": true
  }
}
```

Similar to other schematics, you can add flags and user prompts within the `schema.json` file defined above using the `properties` object: 

```
"properties": {
  "unitTestRunner": {
    "type": "string",
    "enum": ["karma", "jest", "none"],
    "description": "Test runner to use for unit tests",
    "default": "jest",
    "x-prompt": {
      "message": "Which Unit Test Runner would you like to use for the application?",
      "type": "list",
      "items": [
        {
          "value": "jest",
          "label": "Jest  [ https://jestjs.io ]"
        },
        {
          "value": "karma",
          "label": "Karma [ https://karma-runner.github.io ]"
        }
      ]
    }
  },
  "skipInstall": {
    "type": "boolean",
    "description": "Skip installing after adding @nrwl/workspace",
    "default": false
  }
}
```

I recommend viewing the [Authorizing Schematics](https://angular.io/guide/schematics-authoring) guide by Angular for more information on schematic prompts.

Finally, we can actually implement our schematic with the `schematic.ts` file. Some of the more common actions taken in an `init` schematic are adding dependencies and setting the schematic as the default collection. If you want to learn about adding dependencies in an Nx Plugin then check out my [previous blog post](https://dev.to/devinshoemaker/building-an-nx-plugin-to-add-dependencies-to-a-project-29ih).

Nx provides a function to add your schematic as the default collection if one does not currently exist. This can be easily demonstrated with the `@nrwl/angular` or `@nrwl/react` Nx Plugins. Essentially, if the `init` schematic for either of these plugins is executed and there is currently no default collection specified in the users `workspace.json` then that plugin will be set. This allows the user to execute commands without specifying that specific plugin.

```
// With @nrwl/react set as default collection
nx generate app myApp

// With @nrwl/react not set as default collection
nx generate @nrwl/react:app myApp
```

First, import `setDefaultCollection`:

```
import { setDefaultCollection } from '@nrwl/workspace/src/utils/rules/workspace';
```

Next, execute this function with your plugin name as the function parameter within your default functions chain:

```
export default function(): Rule {
  return chain([
    setDefaultCollection('@nxtend/ionic-react')
  ]);
}
```

## Testing

Testing your `init` schematic is similar to testing any other `schematic`. Here is a simple example taken from my `@nxtend/ionic-react` plugin:

```
import { Tree } from '@angular-devkit/schematics';
import { SchematicTestRunner } from '@angular-devkit/schematics/testing';
import { readJsonInTree } from '@nrwl/workspace';
import { createEmptyWorkspace } from '@nrwl/workspace/testing';
import { join } from 'path';

describe('init', () => {
  let appTree: Tree;

  const testRunner = new SchematicTestRunner(
    '@nxtend/ionic-react',
    join(__dirname, '../../../collection.json')
  );

  beforeEach(() => {
    appTree = createEmptyWorkspace(Tree.empty());
  });

  it('should set default collection', async () => {
    const result = await testRunner
      .runSchematicAsync('init', {}, appTree)
      .toPromise();
    const workspaceJson = readJsonInTree(result, 'workspace.json');

    expect(workspaceJson.cli.defaultCollection).toEqual('@nxtend/ionic-react');
  });
});
```

## Conclusion

Adding `init` schematics, also known as `ng add` schematics, are trivial thanks to the work done by the Nrwl team. As a bonus, consider executing your newly made `init` schematic within your `application` or other schematic. This ensures that your initilization process is executed whether the user initiated it or not.

## References

[Nx](https://nx.dev)<br>
[Nx Plugin Guide](https://nx.dev/react/plugins/nx-plugin/overview)<br>
[Building an Nx Plugin to Add Dependencies to a Project](https://dev.to/devinshoemaker/building-an-nx-plugin-to-add-dependencies-to-a-project-29ih)<br>
[Authoring Schematics by Angular](https://angular.io/guide/schematics-authoring)<br>
[@nxtend/ionic-react GitHub](https://github.com/devinshoemaker/nxtend/tree/master/libs/ionic-react)
