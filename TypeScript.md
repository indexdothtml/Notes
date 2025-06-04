# Why TypeScript

As JavaScript project grows large and complex, it is hard to maintain and we may can face more runtime error in production.
JavaScript was developed to write some small scripts for static websites to give it some dynamic feel, as popularity of JavaScript is growing new features which are exist in other programming languages are added into JavaScript like classes, modules etc.
JavaScript is loosly typed or its dynamically typed feature can give runtime error in larger projects and it will hard to maintain for developers.
TypeScript helps into this to add strict type declaration into code, to allow developers to assign types to variables, functions, classes etc. Which can help to minimize error in runtime in production and give the error at compile time while developing.

# How TypeScript works in simple.

TypeScript files are defined with .ts extension.

1. Write the code in TypeScript.
2. Use tsc compiler to compile TypeScript code if any error present it will show at the time of development only. `tsc file-name.ts`
3. If compilation successfull then tsc compiler will generate JavaScript file for that same code, excluding all TypeScript specific code and just pure JavaScript. Then will use that JavaScript file to run into browser for our application or to run into node environment if you are creating any node application.

# TypeScript Datatypes

1. number - Used to store number e.g - 1 or 13 or -1 or 0 etc.

```ts
let num: number;
num = 13;
```

2. string - Used to store string e.g - "Hello World!" or "12" or "" etc.

```ts
let str: string;
str = "Hello World!";
```

3. boolean - Used to store true or false, boolean values e.g true or false

```ts
let isValid: boolean;
isValid = true;
```

4. null - Used to indicate that variable stores nothing, null value

```ts
let data: null | Data; // Pipe symbol is used to declare union of data types.
data = null;
```

5. Array - Used to define array of elements.

```ts
let numArray: number[];
let strArray: string[];
let numStrArray: (number | string)[];

numArray = [1, 3, 4, 5, -3, 0];
strArray = ["Hello", "", "34"];
numStrArray = [1.3, -5, "45", "Hello", 7];
```

6. Objects - Used to define objects.

```ts
let bike: { model: string; make: string; cc: number; isAvailable: boolean }; // Fix way of defining objects if you know already what values object is going to store.

bike = { model: "Ronin", make: "TVS", cc: 225, isAvailable: true };

let userData: Record<string, string | boolean | number>; // If you don't know in advance what will be the structure of an object but you know what types of values it can store.

userData = { name: "Abhishek", lastName: "Kshirsagar", isAdmin: true, age: 24 };

//Another way of defining object if you don't know the structure in advance.

let userData2: { [key: string]: string | number | boolean };

userData2 = {
  name: "Abhishek",
  lastName: "Kshirsagar",
  isAdmin: true,
  age: 24,
};
```
