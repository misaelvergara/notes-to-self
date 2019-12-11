NPM
------
Node Package Manager is a registry for third-party tools and a command line interface.
___
**`package.json`** is a file that contains metadata about your application.  This file should be created before adding any other npm packages.. This file provides basic information about your project. Such as its name, its version and etc. All node applications have by standard a `package.json` file.

> You should run `np init` to create a **`package.json`** before you add other node modules to your application.
> All your dependencies can be safely restored by running `npm i` inside your projects folder.
___
- **`npm list`** lists a project's dependencies.
- - **`--depth=0`** does not list a project's dependency dependencies.
___
- **`npm view <package_name> `** displays **Registry Info** of an npm package
> You can supply a `<package_property>`, such as `dependencies`, so as to display a specific property.
> 
Installing Packages
---
- **`npm i <package_name>@<package_version>`** installs specific version of a package.
- **`npm i <> --save-dev`** | **_`Development Dependencies`_** are packages that are only used during development, such as tools for running unit tests. These dependencies should not go to the production environment where the application will be deployed.
- **`npm un <package_name>`** uninstalls a specific package.
> Command line tools that are accessible out of NPM projects are called **Global Packages**, they are not tied to a specific folder or project. In order to install a package globally, the `-g` param should be declared in the `npm install` command.
> 
Updating Packages
---
Simply command Node to install an already installed package in order to get its latest updates.
- **`npm outdated`** shows a list of outdated packages of a project
- **`npm update`** updates outdated packages to newer minor versions or patches.
- **`npm i -g npm-check-updates`** installs **ncu**, a tool that makes it possible to update the dependencies of a project to major versions, a feature not natively supported by Node.
```bash
ncu
ncu -u
npm i
```
___

**`require`**  takes as argument a file name. E.g: `filename` First, it is interpreted as a core module, then it is interpreted as a file or folder. If it is a file `./filename`, node will try to look for `filename.js` in the current directory. Or else, if it is a folder, node will try to look for a file named `index.js` inside the `/filename` folder. On the condition that none of the above scenarios are valid, node will try to look for a module named `filename` inside `node_modules`.

Dependencies
-----
Installing a package from NPM also download all the dependencies that package needs in order to work. If two modules uses different versions of a dependency, one of these modules will download the specific version of that dependency and store it inside its folder.

_**`Semantic Versioning`**_ 
|Major|Minor|Patch| STATUS|
|-|-|-|-|
|1.|0.|0|app was launched|
|1.|0.|1|bug fixes|
|1.|1.|0|minor changes were added|
|2.|0.|0|major changes were implemented|
|
___
**`^`** the caret character indicates that a version should be kept. E.g:
`"package": "^3.12.7",` either the current version will be downloaded or a newer version as long as the major version is 3.

Publishing Packages
---
**`npm publish`** You need to be logged in with your NPM user account so as to publish your own package. It must provide an entry point for its functionality, which means, exporting its functions and data through an **`index.js`** file.
```js
module.exports.add = function (a, b) { return a + b ; };
```
**`npm version minor`** updates the version number of a package. Only then it will be possible to publish your changes to NPM.
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTIwODQ4MjE4LC0xOTA2NzkxNzgwLDEzND
czNDg4ODgsLTIwNTIyMzQ0OTcsNDUwNDE4MjIxLDE1NDM3MDQw
NDMsMTE1OTA3ODA2MCwtMTY5MjIxMDIwMSwxODI4MzE5MzExLD
M5MDc4OTI3NywxNzM4NDE3MDUwLC0xMTE4MzYwMDYzLDgwNTk5
NDA5LDE4NjA4NzE2MTQsNDc0MTUyMTEzLC0yMTI3Njc5OTEsLT
EzMzc5MjYwNDIsLTIwNDMzNjE2MTgsNTcwMjQxNTA1LDEwOTk0
OTE2OTFdfQ==
-->