# TypeScript Intro
TypeScript is an extension  of(or powerful addition to) JavaScript - it adds static typing to JS (whereas JS is dynamic type).

# Install typeScript into VS Project
Open Terminal and run:  npm init -y 
>   this will give empty json pkg file 
 
- ?? **Do you need this each time?**  
     >  A:  YES - run npm init -y; then install typescript; then compile.
- **WHY? | WHY NOT?** 
     >  A:  Creates the json pkg needed to run code in typescript.

**then run:**    npm install typescript -D
>    -D generates the devDependencies file

###IF DOWLOADING SOMEONE ELSE'S CODE --ALWAYS-- RUN npm install (i.e.:  code fr/ github)

## TypeScript does NOT run in the browser

Must compile TS before running - this will help spot problems within your code.

**to compile, run:**  npx tsc [<i>your file name here - no brackets</i>]
>   >  i.e.:  npx tsc with-typescript.ts
     (This will compile on the ts file that should be compiled.  Otherwise, it will attempt to run on all files in full program)

- ?? **Why does output change TS to 'Var'?** 
     >   A:  compiling turns code into pre-ES6; 
- ??  **Do you leave as is, or change?**
     >   A:  you can change it in the TS config file, but not a big deal!
- ??  **WHY?**

> >     ?? **What are the extra files compiling creates?**
> >     ??    **How to understand what compling is doing?**
> ONCE COMPILED:  you can run node [your js file ... no brackets] which is same as console.log w/i the terminal


# TypeScript BASICS
### // * Primitives:  number, string, boolean
>    > number and string must be lowercase!


### // ! More complex types:  arrays, objects

> without adding a type, the default is 'any'
>
> for object types, you can set object within {} in order to define what can be added within the {}; anything outside of what is defined within {} will throw an error.
>  > i.e.:  let person {
>  > >        name: string;
>  > >        age: number;
>  > >        ID: number;
>  >   }
> 
> any other data someone tries to pass that is not defined here, will be null/error.
> 
>    type inference & union:  TS will 'infer' what type is being used/needed (i.e.:  courses = 'TypeScript for Beginners' is a string, but you do not need to say it's a string - it's inferred)
>   Union is when you combine one or more types, use pipe after the colon to specify one or more >>> use the 'pipe' ( | ) for union type 
> (i.e.:  Person: string | number)

Aliases:  use 'type' to assign an 'alias' that can be defined and used at other places within your code.
>> i.e.:  type Person = { name: string; age: number}
>> then let person: Person;



### // ? Function types, parameters
**Generics**:  flexible.  Use <> with 'T' (i.e. <T>) to help define any type - that can be used and inferred with your code.  Creates flexibility and type safety.

**Classes and Interfaces**: 

**Classes** in typeScript can be defined within the Constructor and made public or private. 
> Example:  class Student {
>    constructor(public firstName: string, public lastName: string, public age: number, private courses: string[]) {}
>
>    enroll(courseName: string) {
>        this.courses.push(courseName);
>    }
>
>    listCourses() {
>        return this.courses.slice();
>    }
>}
A class can define the 'infrastructure' needed for data. What data and types of data are needed.

**Interface**
1. feature only exists in typeScript (not JS).
2. object type definitions (interface)
3. Helps define the structure and forces us to utilize said structure.
4. Create a structure that includes a method that does not return any value (i.e.:  greet: () => void;)
5. Can use Interfaces to define object types; they can be an alternative to defining object types.
>   > can force us to add certain features to a class in order to utilize the class appropriately
> (i.e.:  class Instructor implements Human {
>   this structure must include what is defined in the interface 'Human'
> })

***TS will show red 'squiggly' lines when code is wrong***

#Configuring the TypeScript Compiler

---CLASS NOTES---
npm = node package manager
npm install typescript -D
> 'D' generates the devDependencies
> **If downloading someone else's code (i.e. from GitHub), **ALWAYS** run npm install**

npx = node package execution
> node main.js = same as console.log within terminal

Type vs Interface:
-type ______ **=** {
     _______
}
-interface ______ {
     _______
}

NOTE:  node mudules do not uploade to github
> use .gitignore
>
> add node_modules



----------------------------------------------------
from **typescriptlang.org** (https://www.typescriptlang.org/download):
## TypeScript in Your Project
Having TypeScript set up on a per-project basis lets you have many projects with many different versions of TypeScript, this keeps each project working consistently.

### via npm
TypeScript is available as a package on the npm registry available as "typescript".

You will need a copy of Node.js as an environment to run the package. Then you use a dependency manager like npm, yarn or pnpm to download TypeScript into your project.

> npm install typescript         --save-dev

All of these dependency managers support lockfiles, ensuring that everyone on your team is using the same version of the language. You can then run the TypeScript compiler using one of the following commands:

> npx tsc

### with Visual Studio
For most project types, you can get TypeScript as a package in Nuget for your MSBuild projects, for example an ASP.NET Core app.

When using Nuget, you can install TypeScript through Visual Studio using:

> The Manage NuGet Packages window (which you can get to by right-clicking on a project node)
The Nuget Package Manager Console (found in Tools > NuGet Package Manager > Package Manager Console) and then running:
Install-Package Microsoft.TypeScript.MSBuild

> For project types which don't support Nuget, you can use the TypeScript Visual Studio extension. You can install the extension using Extensions > Manage Extensions in Visual Studio.


**Visit typescriptlang.org Website to learn more**
