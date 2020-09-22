---
published: true
title: "Change Nx Default Affected Branch to Main"
cover_image:
description:
tags: nx, devops, monorepo, webdev
series:
canonical_url:
---

The Nx [affected commands](https://nx.dev/react/guides/ci/monorepo-affected#rebuilding-and-retesting-what-is-affected) are a powerful way to scale monorepos by only rebuilding and retested the apps and libraries that could be affected by a particular change. This is accomplished by comparing hashes of the files modified in the current branch compared to the base branch which defaults to `master`. It's easy to pass in a different branch as a parameter with `--base`, however, you can also change this default in the workspace [`nx.json`](https://nx.dev/react/workspace/configuration#nx-json).

First, make sure that you have created the new base branch. In this example, we will be using `main` as our base branch.

Next, edit the workspace `nx.json`. If you do not have the `affected` property then you will need to add that first, and then you can customize the base branch.

```
{
  "npmScope": "nxtend",
  "affected": {
    "defaultBase": "main"
  },
  ...
}
```

Lastly, this feature is only available in Nx 9.5 or higher. If you are currently on a version of Nx lower than this then I recommend upgrading to the latest version of Nx, or at least the latest version of Nx 9.

**Upgrade to latest version:**

```
nx migrate latest
```

**Upgrade to Nx 9.7:**

```
nx migrate @nrwl/workspace@9.7.0
```
