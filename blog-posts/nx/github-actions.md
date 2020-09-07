---
published: true
title: "Running Nx Affected Commands in GitHub Actions"
cover_image:
description: "How to run Nx affected commands in a GitHub Action workflow"
tags: nx, devops, monorepo, webdev
series:
canonical_url:
---

[GitHub Actions](https://github.com/features/actions) is a powerful feature that allows developers to automate their CI/CD workflows directly in GitHub. It's pretty easy to get up and going with the [official Node.js workflow](https://help.github.com/en/actions/language-and-framework-guides/using-nodejs-with-github-actions#starting-with-the-nodejs-workflow-template) template, however, [Nx](https://nx.dev) can be a bit tricky to work with.

Nx has a powerful set of commands that allow you to [rebuild and retest](https://nx.dev/react/guides/ci/monorepo-affected#rebuilding-and-retesting-what-is-affected) what is affected by a change, but due to the way that GitHub Actions checks out a branch to execute a workflow, these will not work properly with the standard Node.js workflow.

The first thing to change from a standard Node.js workflow is the parameters passed into the `checkout` action:

```
- uses: actions/checkout@v2
  with:
    ref: ${{ github.event.pull_request.head.ref }}
    fetch-depth: 0
```

The `ref` command explicitly sets the commit to be checked out as the latest commit from the pull request that was initiated.

When `fetch-depth` is set to 0 then then the entire history of commits is fetched.

Next, we need to fetch origin master so that we have a base to run the affected commands against:

```
- run: git fetch --no-tags --prune --depth=5 origin master
```

Finally, you can begin running the affected commands:

```
# npm

npm run affected:build -- --base=origin/master

# Yarn

yarn affected:build --base=origin/master
```

Here is a full example borrowed from my [nxtend](https://github.com/devinshoeaker/nxtend) repo:

```
name: Nx Affected CI

on:
  push:
    branches: [master]
  pull_request:
    branches: [master]

jobs:
  build:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [12.x]

    steps:
      - uses: actions/checkout@v2
        with:
          fetch-depth: 0
      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v1
        with:
          node-version: ${{ matrix.node-version }}
      - run: git fetch --no-tags --prune --depth=5 origin master
      - run: yarn install --frozen-lockfile
      - run: yarn affected:build --base=origin/master
      - run: yarn affected:lint --base=origin/master
      - run: yarn affected:test --base=origin/master
      - run: yarn affected:e2e --base=origin/master
```

In order to use this, create the file `nx-affected.yml` in the directory `.github/workflows` in your repository.

# Conclusion

GitHub Actions are powerful and easy to add to your CI/CD pipeline. As your code scales with Nx, so should your testing.

Special thanks to [Plysepter on GitHub](https://github.com/nrwl/nx/issues/2170#issuecomment-607986124) for their suggestions that helped get this working.

## References

[GitHub Actions](https://github.com/features/actions)<br>
[Starting with the Node.js workflow template](https://help.github.com/en/actions/language-and-framework-guides/using-nodejs-with-github-actions#starting-with-the-nodejs-workflow-template)<br>
[Nx - Rebuilding and Retesting What is Affected](https://nx.dev/react/guides/ci/monorepo-affected#rebuilding-and-retesting-what-is-affected)<br>
[@nxtend](https://github.com/devinshoemaker/nxtend)
[Plysepter on GitHub](https://github.com/nrwl/nx/issues/2170#issuecomment-607986124)
