---
published: true
title: "Building an Nx Plugin to Add Dependencies to a Project"
cover_image:
description: "Learn how to build an Nx Plugin that adds dependencies to a project"
tags: nx, schematics, monorepo, webdev
series:
canonical_url:
---

[Nx community plugins](https://nx.dev/nx-community) are a powerful new technology by Nrwl that allows you to customize the functionality of Nx. If you have not yet watched Nrwl's official [Nx Plugin guide](https://nx.dev/react/plugins/nx-plugin/overview) then I highly recommend starting there.

When building an Nx Plugin you may want to add dependencies when a schematic is executed. Perhaps you need to add dependencies during an `ng add` command, or maybe you only want to add dependencies when a particular flag is passed into a schematic (such as whether routing will be enabled or not). Adding dependencies with an Nx Plugin is very easy using the `@nrwl/workspace` library provided by Nrwl.

# Implementation

First, add the `addDepsToPackageJson` library:

```
import { addDepsToPackageJson } from '@nrwl/workspace';
```

Next, create a new function that returns the `addDepsToPackageJson` function. This function accepts two arguments; a `dependencies` and `devDependencies` object to merge with the users `package.json`:

```
function addDependencies(): Rule {
  return addDepsToPackageJson(
    {
      '@ionic/react': ionicReactVersion,
      ionicons: ioniconsVersion
    },
    {
      '@nxtend/ionic-react': nxtendVersion,
      '@testing-library/user-event': testingLibraryUserEventVersion,
      '@testing-library/jest-dom': testingLibraryJestDomVersion
    }
  );
}
```

In the example above, I am setting the library versions based on variables in a separate `versions.ts` file. This allows me to easily view and maintain what dependency versions my plugin is importing.

Finally, just execute this function in you schematic default function chain:

```
export default function(): Rule {
  return chain([
    addDependencies()
  ]);
}
```

# Testing

Adding a unit test for this is trivial. Here is an example from my `@nxtend/ionic-react` plugin:

```
describe('init', () => {
  let appTree: Tree;

  const testRunner = new SchematicTestRunner(
    '@nxtend/ionic-react',
    join(__dirname, '../../../collection.json')
  );

  beforeEach(() => {
    appTree = createEmptyWorkspace(Tree.empty());
  });

  it('should add Ionic React dependencies', async () => {
    const result = await testRunner
      .runSchematicAsync('init', {}, appTree)
      .toPromise();
    const packageJson = readJsonInTree(result, 'package.json');
    expect(packageJson.dependencies['@ionic/react']).toBeDefined();
    expect(packageJson.dependencies['ionicons']).toBeDefined();
    expect(packageJson.dependencies['react']).toBeDefined();
    expect(packageJson.dependencies['react-dom']).toBeDefined();
    expect(packageJson.devDependencies['@nrwl/react']).toBeDefined();
    expect(packageJson.devDependencies['@nxtend/ionic-react']).toBeDefined();
    expect(
      packageJson.devDependencies['@testing-library/user-event']
    ).toBeDefined();
    expect(
      packageJson.devDependencies['@testing-library/jest-dom']
    ).toBeDefined();
  });
});
```

In this test we create a new workspace, execute the `init` schematic that executes the `addDepsToPackageJson` method, and then asserts that these dependencies are present in the `package.json`.

# Conclusion

Nx Plugins are an exciting new technology with a lot of potential. Adding dependencies to a project with Nx Plugins is fairly simple, but feel free to check out my [`@nxtend/ionic-react`](https://github.com/devinshoemaker/nxtend/tree/master/libs/ionic-react) Nx Plugin for more examples.

# Resources

[Nx](https://nx.dev)<br>
[Nx Plugin Guide](https://nx.dev/react/plugins/nx-plugin/overview)<br>
[@nxtend/ionic-react GitHub](https://github.com/devinshoemaker/nxtend/tree/master/libs/ionic-react)
