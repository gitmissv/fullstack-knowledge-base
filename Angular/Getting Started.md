# Angular:  What is it?
- Versioning:
  - AngularJS (Angular1)
  - Angular 2 (2016)
  - Angular 4 (v3 was skipped)
  - v10, 11, 12, ...
  - Ignore all versions except V1 (AJS) vs 2+

## Angular CLI (command line interface)
Angular uses TypeScript (subest of JavaScript)

> Keep terminal open while working on Angular file. When finished, type Ctrl+C to quit; this will close out your localhost:4200.











-----------------------------------------------------------
...@LAPTOP... ~
> $ npm install -g npm@6

added 1 package in 20s

4 packages are looking for funding
  run `npm fund` for details

...@LAPTOP... ~
> $ npm install -g @angular/cli@latest

...@LAPTOP...\AppData\Roaming\npm\ng -> ...@LAPTOP...\AppData\Roaming\npm\node_modules\@angular\cli\bin\ng.js
+ @angular/cli@16.2.3
added 249 packages from 165 contributors in 37.399s


## Once Angular sucessfully completes, add your project
>   ng new [project name ... no brackets; no spaces]
>   <i>i.e.:  ng new my-first-project</i>
>   also add --no-strict (puts in non-strict mode; strict mode is special mode to create project; then optimizing; but start by non-strict mode first)
> full code:  ng new my-first-project --no-strict
 - Q: Wld you like to enable autocompletion....? 
   - A: Y
 - Q: Wld you like to share pseudonymous usage data...?
   - A: N
 - Q: Wld you like to add angular routing...?
   - A: N
 - Q: Which stylesheet format....?
   - A: CSS 

## Once successfully initialized, open your new file/directory
> i.e.:  cd my-first-project/

then run (to complete browser app bundle):  
> ng serve 
> > open file at **localhost:4200**



...@LAPTOP... /c/myWorkspace
$ ls
 CodeLabs_Fall2023/   'TypeScript Demo'/           my-first-project/   typescript-exercises/
'JavaScript Videos'/   fullstack-knowledge-base/   typeScript/

...@LAPTOP... /c/myWorkspace
$ cd my-first-project/

...@LAPTOP... /c/myWorkspace/my-first-project (master)
$ ng serve
√ Browser application bundle generation complete.

Initial Chunk Files   | Names         |  Raw Size
vendor.js             | vendor        |   2.03 MB |
polyfills.js          | polyfills     | 333.19 kB |
styles.css, styles.js | styles        | 230.46 kB |
main.js               | main          |  46.03 kB |
runtime.js            | runtime       |   6.53 kB |

                      | Initial Total |   2.63 MB

Build at: 2023-09-27T00:51:50.388Z - Hash: 79399e93d69a9c3b - Time: 26290ms

## Angular Live Development Server is listening on **localhost:4200**, open your browser on **http://localhost:4200/**


√ Compiled successfully.
