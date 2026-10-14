---
title: "npm link"
source: "https://medium.com/@jophin.joseph88/npm-link-2f35c7e1ac33"
author:
  - "[[Jophin Joseph]]"
published: 2024-02-21
created: 2026-10-06
description: "npm link is the quintessential tool for developing and testing npm packages iteratively without having to continually rebuild."
tags:
  - "clippings"
---
`npm link` is the quintessential tool for developing and testing npm packages iteratively without having to continually rebuild. The package can be tested directly in the intended target code base so that you can steer clear of any unsavoury surprises post publish. I’ve been using it for a long time. Initially it was pretty straightforward. But as my codebase got complicated with tooling like nvm, Webpack etc, I started facing issues with getting it to work. This writeup is about what I’ve learned from my acquaintance with `npm link`.

## Use case

For this discussion consider the following use case.

I have a node app named **app** in *~/Documents/workspace/app* which uses a package **utils**. **utils** is already published to npm. I’m developing a new feature in **utils** that I would like to test in **app**. For this purpose, I have checked out the package in *~/Documents/workspace/utils*. **utils** package has *src/index.js* as it’s main file in **package.json**.

I’ll be creating a link to **utils** from **app** to test the new feature.

## Usage

Linking a package from another codebase is a 2 step process.

### Step 1

**Run** `**npm link**` **in the package that is to be tested.**

This will create a symbolic link from the package directory to the global *node\_modules* directory which is at *{prefix}/lib/node\_modules/\<package-name>*. It will also link any bins in the package to *{prefix}/bin/\<bin-name>*.

`<package-name>` here refers to the name of the package in *package.json* file and not the name of the directory in which the package code resides.

`{prefix}` here refers to the output of `npm prefix -g`. In my MacOS where node has been installed via homebrew, this is */usr/local*. So my global *node\_modules* are at */usr/local/lib/node\_modules*.

When I execute `npm link` in the **utils** directory, a symbolic link is created from */usr/local/lib/node\_modules/utils* to *~/Documents/workspace/utils*. When I go to my global node modules directory, this is the output of the `ls` command

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*0WOY-pdm6nP26nQMJ6M8zw.png)

utils package linked from global node\_modules to the package directory

### Step 2

**Run** `**npm link <package-name>**` **in the codebase where you want to test the package.**

As per the npm [documentation](https://docs.npmjs.com/cli/v8/commands/npm-link), this will create a symbolic link from *node\_modules/\<package-name>* within the codebase to the global *node\_modules* i.e. *{prefix}/lib/node\_modules/\<package-name>*. But I’ve noticed that this behaviour has changed for newer versions of npm(I think from 8+). For newer versions, the symbolic link is created from *node\_modules/\<package-name>* directly to the local package repository.

When I execute `npm link utils` in my **app** directory, a symbolic link is created from *~/Documents/workspace/app/node\_modules/utils* to the utils package location *~/Documents/workspace/utils* because I’m running on npm 8.11. The output of the `ls` command in the *node\_modules* directory of **app** shows this

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*ZXsw9YsbPBIZ4EUJSIxUcg.png)

Symbolic link from app/node\_modules to utils directory

I tried the same on npm 6.14.4. In that case, utils get linked to the global *node\_modules* as mentioned in the npm documentation i.e. */usr/local/lib/node\_modules/utils*.

## Usage with nvm

nvm allows switching between of different versions of node in the same machine. Even though multiple versions of node could be present, only 1 will be set as the current version. When nvm is in play, executing `npm link ` in a package creates a link to the current node version’s(set via `nvm use`) global *node\_modules*. Later when `npm link <package-name>` is executed in the target codebase, if the nvm current node version has changed, the link will not be created.

### Use case

In the initial use case, suppose **app** needs node 18 and **utils** need at least node 16 to work. So to link them the following needs to be done

1. Switch to node 18 using nvm
2. Run `npm link` in **utils**. This will link the package to the global *node\_modules* of node v18
3. Run `npm link utils` in **app**

Now suppose there is an **app\_1** that also uses **utils** but which only works on node 16. To link **app\_1** to **utils**, the following needs to be done

1. Switch to node 16 using nvm
2. Run `npm link` again in **utils** so that it also gets linked to the global *node\_modules* of node v16
3. Run `npm link utils` in **app\_1**

> Both the commands should be executed in the same version of node while using nvm. If the package needs to be linked to multiple apps running on different versions of node, it should be ensured that `npm link` has been run in the package for all those node versions, before running `npm link <package-name>` in the corresponding apps.

## Usage with Webpack

Linking creates some issues if the app from which the package is linked is bundled with Webpack.

### Issue with resolve.symlinks setting

In some of my apps, when bundling an app that has a linked package, I’ve faced an issue with Webpack not being able to resolve imports from the linked module. This is most probably because of the `resolve.symlinks` settings in the Webpack config. This boolean is ***true*** by default which means that packages will be resolved to their real path and not their symlinked location. So if this issue pops up, set `resolve.symlinks` to ***false*** in your webpack config and the issue should be resolved.

## Get Jophin Joseph’s stories in your inbox

Join Medium for free to get updates from this writer.

In the use case that we have been following, `resolve.symlinks` with value

- ***true*** will result in **utils** being resolved to *../utils/src/index.js*
- ***false*** will result in **utils** being resolved to *./node\_modules/utils/src/index.js*

I’ve not been able to pinpoint exactly when this difference in resolution becomes an issue. I have some codebases where linked modules work perfectly without having to set `resolve.symlinks`. I also have some others where the dev build fails without setting it to false. The Webpack documentation for this property is also a bit ambiguous in it’s wording — *Note that this* ***may*** *cause module resolution to fail when using tools that symlink packages*

> To be on the safe side, always set `resolve.symlinks` to **false** in your Webpack config for development builds

### Issue while linking React packages

Suppose you are developing a package that has a React component which you would like to link and test in your app. The Webpack build will go through fine. But when you load the application in the browser, you might see you app crashing with an error logged — *You might have more than one copy of React in the same app*.

When a React component is published to npm, the `react` pacakage has to be added as a peer dependency in order to ensure that the it does not get bundled along with the component. If marked as a peer dependency, when the component is used in another React app, it will pick up `react` from that app’s *node\_modules*.

So if you face this issue,

1. Ensure is that your `react` has been added to **peerDependencies** and not to **dependencies** in the component’s **package.json**.
2. `react` should also be marked as an external dependency in the component’s bundler(`externals` for Webpack and `external` for Rollup). This will prevent them from being added to the output bundle.
3. Ideally the above 2 should resolve the issue. But in case you are still facing issues, create an alias for `react` in the app’s development Webpack config and resolve it to the app’s react version as shown below
```cs
// webpack.config.js
resolve: {
  alias: {
    react: path.resolve('./node_modules/react'),
}
```

> 1\. Ensure `react` is not packaged along with the component build.
> 
> 2\. Explicitly resolve `react` to the app’s react version in webpack config if the issue is still not resolved.

### TypeScript

TypeScript has an option `preserveSymlinks`. As per the [documentation](https://www.typescriptlang.org/tsconfig#preserveSymlinks), it exhibits the opposite effect of `resolve.symlinks` in Webpack. But I never had to tweak this option for any of my apps. I checked the effect of `preserveSymlinks` in 2 cases

1. A project with TS enabled and bundled with Webpack
2. A NodeJS project with TS enabled and transpiled using `tsc`

In both cases, the file generated with `preserveSymlinks: true` was identical to the file generated with `preserveSymlinks: false`. So I have not been able to track the utility of this option.

## NodeJS

NodeJS also has 2 options related to linking

1. [— preserve-symlinks](https://nodejs.org/api/cli.html#--preserve-symlinks)
2. [— preserve-symlinks-main](https://nodejs.org/api/cli.html#--preserve-symlinks-main)

There are detailed explanations in the NodeJS documentation related to these options. But I never had to use these in any of my apps to get linking to work.

## Other linking woes

The link command will always resolve the entire dependency tree, like `npm install`. Suppose you delete *node\_modules* and issue `npm install A`, you will notice that the whole list of dependencies in *package.json* are installed along with A. Similarly, when you run `npm link A`, npm will link package A + install all the other dependencies in *package.json*.

There are some linking issues I’ve noticed in relation to this behaviour of `npm link`.

### Linking multiple packages

Suppose you have a codebase in which package A is linked. Now you need to link another package B to the same codebase. When you issue `npm link B` now, you will notice that A is not linked anymore. This is because `npm link B` is telling npm to link package B + install all other dependencies in *package.json*. When npm does this, link created to package A is overwritten with the downloaded version of A from the registry. If the version of A mentioned in *package.json* is not found in the regsitry, linking fails with a 404 in the terminal for package A. So to link both A and B to the codebase, execute `npm link A B`.

> If multiple packages are to be linked to the a codebase, issue a single link command with all the packages to be linked in that single command — `npm link p1 p2 p3..`. Issuing multiple link commands for each package will link only the last package.

### Installing other packages

Suppose you have a codebase in which package A is linked. When you install a new package, you will notice that link to A is lost. This is because `npm install` has resolved the whole tree again and has installed A from the registry thereby overwriting the link. In case the version of A mentioned in *package.json* was not present in the registry, `npm install` would have failed with a 404. To resolve this issue, after every npm install, re-link all the packages that have to be linked.

> `npm install` command will overwrite existing links. After every `npm install`, `npm link` should be issued again to create the links that were lost