---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - node_js
  - JavaScript
  - programming
note type: Informational Note
---
Links:
- npm web site: [click](https://www.npmjs.com/)
- lodash documentation: [click](https://lodash.com/)

It is a **Node Package Manager** 
- Its a *global* package, that means it can be used from any folder and doesn't depend on any specific project  

- I have installed npm with the exact version (8.14.0) with the command `npm i -g npm@8.14.0`, this command can be used for every version of npm
- I created an folder for npm demo with `mkdir npm-demo` command and navigated there
- I initiated npm `npm init` in order to create a module folder and json package files
	- These JSON files are keeping information about the project (author, keywords, git repository, etc.)
- Then, I installed *lodash* module for npm with `npm i lodash`
	- it changed "dependencies" in *package.json* and added a folder lodash with its .js files

To use this module we need to use a `const _ = require("lodash")` method.
	`require()` method:
		./ is used if the file that being imported is in the same folder 
		../ is used if the file is in parent folder
		without these things -> the file is a folder and is located in modules folder 

*Example*:
```JavaScript
const _ = require("lodash"); // importing lodash

const result = _.includes([1, 2, 3], 2); // using lodash method
console.log(result); // true
```

# Semantic Versioning 
It is what versions mean.
For example in **package.json** we have a line `dependencies{ "lodash" : "^4.17.21"}`
The number is what we call *SemVer* and it consists of:
- `4` - major version (updates with new grand features)
- `17` - minor version (updates with new features)
- `21` - patch (updates with fixing bugs)

If we have a project we can use syntax like that: `lodash : ^4.x` this `^4.x` means that everybody can use this code on the major version 4 of lodash and any minor existing version.

`~7.4.x` - means that we are interested in any version as long as the major version is 7 and minor is 4

If we want to see every dependencies versions, there is no need of entering **package.json**, we can do so with this command:
- `npm ls`

# Commands 
- `npm i -g @npm8.14.0` - install the exact 8.14.0 version of npm (can be used with any npm module)
- `mkdir dirName` - create a direction with name(dirName) 
- `npm i lodash` - install lodash module
	-  Can also install many modules at the same time:
		`npm i lodash@4.11.1, mongoose@6.9.1`
- `npm un packageName` or `npm uninstall packageName` - uninstalls package  
- `npm ls` - watch all npm dependencies from **package.json** 
	- `npm ls mongoose` - reveals mongoose current installed version
- `npm view mongoose` - watch mongoose module information
	- we can any particular property of the module with: `npm view moduleName property`
	- Example: `npm view mongoose dependencies` - will reveal mongoose's dependencies
	- `npm view mongoose versions` - used to reveal all the versions module ever had
- `npm outdated` - reveals all the obsolete modules 
	- `npm update` - updates the obsolete modules, though *only patch and minor version*
- `npm i -g npm-check-updates` - install npm-check-updates modules
	- we have a new command tool: `npm-check-updates` - advanced version checker 
		- when running upper command, can use `ncu -u` to update all the obsolete modules 
		- then need to run `npm install` to install new versions
- `npm i jshint --save-dev` - installs jshint and adds it as a development dependency (modules needed only on development stage, such as tests, static code analysis, etc.)  
- `-g` refers to *global* package
	- if we want to install any package globally, we need to run:
	- `npm i -g packageName@packageVersion` command
	- `npm -g outdated` - reveals all outdates global packages
