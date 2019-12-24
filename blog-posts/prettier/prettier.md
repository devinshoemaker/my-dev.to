---
published: false
title: "How to Configure Prettier to Automate Code Formatting"
cover_image:
description: "Using VSCode extensions and pre-commit hooks to automate code formatting with Prettier"
tags: prettier, codestyle, javascript, webdev
series:
canonical_url:
---

Code formatting is not a new concept, but based on my experience with professional software development, it's a problem that many companies and projects still struggle with. [Prettier](https://prettier.io) is a tool that attempts to simplify and automate the process of keeping code formatting consistent within a project.

# What is Code Formatting?

Code formatting, also known as code styling, style formatting, programming style, is what I like to consider the grammar of software development. Quality grammar can make a written body of work more appealing to read, and easier to digest, and code formatting can do the same for a project's source code. Well placed tabs, brackets, and newlines can make it much easier for a developer to read and understand code. Perhaps more importantly, consistent formatting across a collaborative codebase can make the development experience less frustrating as the developer knows what to expect of their own contributions.

# Why Prettier?

Prettier describes itself as an opinionated code formatter. In this case, "opinionated" means that Prettier has a prescribed way of formatting code, with only a handful of options that you can configure. I have used code formatting tools that have well over 100 options, while Prettier only has about 16. I have also been on teams in the past that attempted to adopt code formatting guidelines, but the endless debates over which options were better prevented us from ever making a final decision.

# Prettier Playground

The Prettier team offers a useful tool on their website called [Prettier Playground](https://prettier.io/playground/). This allows you to experiment with JavaScript and see how Prettier would format the code in real-time, and if you find a set of options that you prefer, then you can copy the proper config to your clipboard.

# Configuration File

To customize the Prettier configuration, you can add a `.prettierrc` to the root of your project. You can add single configurations to this file, such as `{ "singleQuote": true }`, or you can paste the configuration from Prettier Playground. If you don't provide a config file, then Prettier will use the default [Prettier options](https://prettier.io/docs/en/options.html).

# VSCode Extension

The easiest way to get started using Prettier is to install the Prettier VSCode extension by Esben Petersen. To manually format a single file, simply use the `Format Document` shortcut (on macOS the default is shift+option+f). If you would like to automatically format a document when you save then you can open the VSCode settings and enable the `Format On Save` option. You can also enable the VSCode setting `Prettier: Require Config` to avoid formatting files in projects that do not use Prettier.

# Pre-commit Hook

The VSCode extension is a convenient way to experiment with Prettier, but it can be difficult to enforce on teams. You can automate code formatting using a couple of dependencies and a modification to your `package.json`.

```
npm install --save-dev prettier husky pretty-quick

or

yarn add --dev prettier huskey prett-quick
```

- `prettier` is the main CLI that will be formatting the code
- `husky` enables hooks into several different steps of the Git commit lifecyle
- `pretty-quick` runs Prettier on staged or changed files

Once these dependencies are installed, add this to your `package.json`.

```
"husky": {
  "hooks": {
    "pre-commit": "pretty-quick --staged --pattern 'src/**/*.{js,jsx,ts,tsx,json,css,scss,md,html}'"
  }
}
```

This will automatically run Prettier against your staged files that are within the `src/` folder that match one of the extensions js, jsx, ts, tsx, json, css, scss, md, or html. I think that this is a well-rounded solution for most projects, but if you would like to change the files that get formatted, you can adjust the `--pattern` parameter by following the [minipatch](https://github.com/isaacs/minimatch) pattern.

# Resources

Prettier: https://prettier.io<br/>
Playground: https://prettier.io/playground/<br/>
CLI: https://prettier.io/docs/en/cli.html<br/>
Configuration: https://prettier.io/docs/en/configuration.html<br/>
Ignoring files: https://prettier.io/docs/en/ignore.html<br/>
Pre-commit hooks: https://prettier.io/docs/en/precommit.html
