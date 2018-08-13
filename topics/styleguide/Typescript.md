# TypeScript styleguide

## Table of Contents

* [Naming](#naming)
    * [Variables and Functions](#variables-and-functions)
    * [Classes](#classes)
    * [Interfaces](#interfaces)
    * [Types](#types)
    * [Enums](#enums)
* [Decor](#decor)
    * [Quoutes](#quoutes)
    * [Spaces](#spaces)
* [Export and Import](#export-and-import)
* [Contructions](#contructions)
    * [Arrow functions](#arrow-functions)
* [File system structure](#file-system-structure)

## Naming

### Variables and Functions: 
* Use `camelCase` for variable and function names

    *Why?*: Conventional JavaScript

    ```ts
    /* Bad */

    let FooVar;

    function FooFunc() { }
    ```
    ```ts
    /* Good */

    let fooVar;

    function fooFunc() { }
    ```

### Classes 
* Use `PascalCase` for class names

    *Why?*: This is actually fairly conventional in standard JavaScript.

    ```ts
    /* Bad */

    class foo {

    }
    ```

    ```ts
    /* Good */

    class Foo { 

    }
    ```

* Use `camelCase` of class members and methods

    *Why?*: Naturally follows from variable and function naming convention.

    ```ts
    /* Bad */

    class Foo {
      public Bar: number;
      public Baz(): void { }
    }
    ```
    ```ts
    /* Good */

    class Foo {
      public bar: number;
      public baz(): void { }
    }
    ```
* Do not use `_` as a prefix for private properties.

    ```ts
    /* Bad */

    class Foo {
      private _bar: number;
      private _baz(): void { }
    }
    ```
    ```ts
    /* Good */

    class Foo {
      private bar: number;
      private baz(): void { }
    }
    ```

### Interfaces

* Use `PascalCase` for name.

    *Why?*: Similar to class

* Use `camelCase` for members.

    *Why?*: Similar to class

* **Don't** prefix with `I`

    *Why?*: Unconventional. `lib.d.ts` defines important interfaces without an `I` (e.g. Window, Document etc).

    ```ts
    /* Bad */

    interface IFoo {

    }
    ```
    ```ts
    /* Good */

    interface Foo {

    }
    ```

### Types

* Use `PascalCase` for name.

    *Why?*: Similar to class

* Use `camelCase` for members.

    *Why?*: Similar to class

### Enums

* Use `PascalCase` for enum names

    *Why?*: Similar to Class. Is a Type.

    ```ts
    /* Bad */

    enum status {

    }
    ```
    ```ts
    /* Good */

    enum Status {

    }
    ```

* Use `PascalCase` for enum member

    *Why?*: Convention followed by TypeScript team i.e. the language creators e.g `SyntaxKind.StringLiteral`. Also helps with translation (code generation) of other languages into TypeScript.

    ```ts
    /* Bad */

    enum Status {
        ready
    }
    ```
    ```ts
    /* Good */

    enum Status {
        Ready
    }
    ```
## Decor

### Quoutes 
* Prefer single quotes (`'`)

    *Why?*: More JS teams do it (e.g. [npm](https://github.com/npm/npm), [node](https://github.com/nodejs/node), [google/angular](https://github.com/angular/angular/), [facebook/react](https://github.com/facebook/react)). It's easier to type (no shift needed on most keyboards).

    ```ts
    /*Bad*/

    let foo = "foo";
    ```
    ```ts
    /*Good*/

    let foo = 'foo';
    ```

* When you can't use double quotes, try using back ticks (`).

    *Why?*: These generally represent the intent of complex enough strings.

    ```ts
    let foo = 5;
    let bar = `Can't add some number: ${foo}`
    ```

    The result will be `Can't add some number: 5`

### Spaces
* Use `2` spaces.

    *Why?*: More JS teams do it (e.g. [npm](https://github.com/npm/npm), [node](https://github.com/nodejs/node), [google/angular](https://github.com/angular/angular/), [facebook/react](https://github.com/facebook/react)). The TypeScript/VSCode teams use 4 spaces but are definitely the exception in the ecosystem.

    ```ts
    /*Bad*/

    class Foo {
        public bar: number;

        public baz(): void {}
    }
    ```   
    ```ts
    /*Good*/

    class Foo {
      public bar: number;

      public baz(): void {}
    }
    ```

## Export and Import

* Use `index.ts` file to export all stuff ouside of folder.

    *Why?*: It's convenient to import from folder name instead of full path to file

    ```ts
    /*src/services/data.service.ts*/

    export class DataService {}
    ```
    ```ts
    /*src/services/index.ts*/

    export * from './data.service';
    ```

    ---

    ```ts
    /*Bad*/

    import { DataService } from './src/services/data.service'
    ```
    ```ts
    /*Good*/

    import { DataService } from './src/services'
    ```

* Use relative path for import statement.
    TypeScript [--baseUrl](https://www.typescriptlang.org/docs/handbook/module-resolution.html#base-url)

    *Why?*: It's convenient to have import statements without long paths

    ```ts
    /*Bad*/

    import { DataService } from '../../../../services'
    ```
    ```ts
    /*Good*/

    import { DataService } from 'services'
    ```

## Contructions

### Arrow functions

* Use arrow functions instead of simple `function` wherever it possible.

    *Why?*: It doesn't lose context and easier to read.

    *Exeptional case*: Use `function` statement in case if it requires to have context.

    ```ts
    /*Bad*/

    ['London', 'New York'].forEach(function(cities){

    });

    function (x) { 
        return x + x;
    }
    ```
    ```ts
    /*Bad*/

    ['London', 'New York'].forEach((cities) => {

    });

    (x) => x + x
    ```
    ```ts
    /*Good*/
    
    ['London', 'New York'].forEach(cities => {

    });

    x => x + x
    ```
    ```ts
    /*Good*/
    
    ['London', 'New York'].forEach((cities, index) => {

    });

    (x, y) => x + Y
    <T>(x: T, y: T) => x === y
    ```

## File system structure

Actually it depends on project. (Node, Angular, React, Vue)
