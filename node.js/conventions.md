## Node.js Conventions

1. Use a `package.json` file
2. Leverage npm commands

#### 1. Use a `package.json` file

**Why?**

A `package.json` file allows you to provide meta information about your project that is useful
and oftentimes necessary for people and other programs to interact with what you've written. It 
gives you a way to keep track of your project's dependencies, version, license, repository, 
authors, contributors, and it provides you with a set of canonical commands used to run and 
test Node.js applications even if you know nothing about them.

**How?**

When starting a new Node.js project, the first thing you should do after creating your new 
project directory is run:

* `npm init`

Answer the prompts to the best of your ability.  Once you're done, you can view/edit the 
`package.json` file it generates.  You'll likely have to circle back to add in repository 
info and maybe update description fields, author fields over time.  However, do not manually 
edit your dependencies if it can be avoided.  It's prone to human error and there are convenient 
commands for doing that for you.

To add a project dependency, use:

* `npm install <package_name> --save`

The `--save` options tells npm to include the package in your `node_modules` director AND it
adds the package name and version to your `package.json`.

To add a project *development* dependency -- in other words, a package that you need as a 
developer of your project, but not a user of the project -- use the `--save-dev` flag like 
this:

* `npm install <package_name> --save-dev`

Your developer dependencies are kept within a separate object inside of `package.json` and it's 
good practice to make the distinction because when you `npm install` something, it will only 
include its dependencies and not its developer dependencies.  This leads to smaller package sizes
and faster downloads for your users.

**Example**

```
{
  "name": "tips-for-students",
  "version": "0.1.0",
  "description": "An example package.json for reference.",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+ssh://git@github.com/your-name/sample-project.git"
  },
  "keywords": [
    "CLI",
    "samples",
    "examples"
  ],
  "author": "Greg Considine <greg@greg-considine.com>",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/your-name/sample-project/issues"
  },
  "homepage": "https://github.com/your-name/sample-project#readme"
}
```

**Summary**

So by supplying some basic information, anyone who uses are projects knows where the official
repository is, who the author is, what the latest version is, where to get more info (README), 
where to file bugs/issues (GitHub), and what the project is licensed under.

**Notes**

* If you're using git, always create a `.gitignore` file and add `node_modules`.  Sometimes there 
are system-specific things that `npm` needs to do when running `npm install`, so your `node_modules`
might not necessarily work on another machine as-is.  Better to exclude `node_modules` and have 
users of your package use `npm` to install them on their machine.

* If you do clone a project that has a `package.json` use `npm install` with no additional arguments 
or options to install every dependency listed within the supplied `package.json`.

#### 2. Leverage npm commands

**Why?**

There are canonical approaches to starting and testing a Node.js application.  npm provides the 
ability to run scripts to do *something*.  There are a finite set of commands to leverage like 
`npm start`, `npm test` and so on, but you can also include custom commands that can be executed 
after particular events like `postinstall` and `pretest`.  Beyond that, you can even supply your 
own custom commands that can be executed by using `run` as in `npm run my-custom-script`.

This is considered good practice because if someone knows nothing about your project aside from 
what it's supposed to do (play Hangman, for example) they don't want to learn about your file 
structure or figure out which command to run to get things started.  They only need to type
`npm start` and they're off and running.

**How?**

These scripts are all added to the `"scripts"` object inside of your `package.json`.  The official
script properties can be found in the resource link below.  For now, I'm going to focus on `start`.

`start` is somewhat of an anomaly because you don't explicitly need to include `start` in the 
script block, if you have your entry file assigned to the `main` property in your `package.json`, 
then `npm start` will run `node <name_of_your_main_file>`

If starting requires particular arguments, flags, and options, you could overwrite the `start` 
script like this:

```
"scripts": {
  "start": "node lib/start.js arg1 arg2 --long-option -f"
}
```

#### Resources

* [Software licenses](https://spdx.org/licenses/)
* [npm scripts](https://docs.npmjs.com/misc/scripts)
* [.gitignore](https://git-scm.com/docs/gitignore)

