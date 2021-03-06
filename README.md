# ngMigration Assistant

ngMigration Assistant is an easy-to-use command line utility that scans an AngularJS application and recommends how to migrate to Angular. 

![ajs-app-dark-slow](https://user-images.githubusercontent.com/27384475/43745004-7f44ff54-9991-11e8-9c9b-acd0dda042cc.gif)

## Getting Started
### Installing
Whether you are using npm or yarn package manager, install ngma globally.
```
npm install -g ngma
```
```
yarn global add ngma
```

### Run the program

ngMigration Assistant will scan the current working directory or the input directory.
```
ngma <your_angularjs_app>
```

## App Composition

###  Class: analysisTool

Runs the analysis on the provided directory and returns a recommendation on which migration path to take to Angular. It looks at the complexity, source lines of code (sloc), antipatterns, AngularJS version, and preparation necessary for migration. It identifies the files that need to be modified and the specific changes that will prepare the app for upgrading. 

### Methods

* ```buildPathIgnoringGlobs()``` Builds a new filesystem by removing files matching the ignore globs using glob. Returns as an array of the new filesystem.
* ```getGlobsFromGitignore()``` Parses .gitignore file into an array of globs and appends default globs to the array. Filters out patterns starting with ! from the array because ! means to never ignore. Returns the globs to ignore.
* ```countLinesOfCode()``` ***asynchronous*** Counts sloc using node-sloc to traverse new filesystem returned by buildPathIgnoringGlobs(). Returns a promise that resolves to sloc.
* ```runAnalysis()``` Traverses through filtered filesystem returned by buildPathIgnoringGlobs() and calls testFile() to run the individual tests.
* ```runAntiPatternReport()``` ***asynchronous*** Creates the anti-pattern report and calculates the rewriteThreshold runRecommendation() uses. Each time an anti-pattern is found, general instructions and files needing corrections are appended to the preparation report. Returns a promise that resolves to the preparation report. 
* ```runRecommendation()``` ***asynchronous*** Recommendation algorithm that checks type of application (AngularJS, Angular, or hybrid), checks if sloc is under the rewriteThreshold, and checks if passes the ngUpgrade requirements. Returns a recommendation and preparation report. 

### Built With

* [node-glob](https://www.npmjs.com/package/glob)
* [parse-gitignore](https://www.npmjs.com/package/parse-gitignore)
* [node-sloc](https://www.npmjs.com/package/node-sloc)
* [readline-sync](https://www.npmjs.com/package/readline-sync)

## Authors

**Elana Olson** - [ellamaolson](https://github.com/ellamaolson)

## License 

Copyright Google Inc. All Rights Reserved. Use of this source code is governed by an MIT-style license that can be found in the LICENSE file at https://angular.io/license





