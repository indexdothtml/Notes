 ## What is Runtime Environment ?
 
 Runtime Environments are software which contains services, which manage resources while running other programs on it. (the programs for which the runtime environments are build for). Runtime Environments are build to execute other programs easily, without considering other problems like memory management, error handling etc. Different programming langagues have there own runtime environment like for JavaScript we have nodeJs, for Java we have Java Runtime Environment (JRE), for .Net programms we have .Net Common Language Runtime etc.

## Why .js extention ?

 There is no difference between text.txt and text.js file both contains text, but text.js file is special file, which contains some fixed words or some structure, it not contain any random words, all lines are some rules we call syntax.
The nodeJs - JavaScript Runtime environment is coded as to only understand .js extention file. 

## Variables without let, const and var

 In JavaScript you can create a variable without using let, const and var keyword, just by giving variable_name = value; in without strict mode file.
```
name = "Abhishek";
```
If you create variable without using var, let and const keyword then JavaScript engine in browser make that variable as a property of window object (It means it will make that variable in global scope) and in nodeJs runtime environment as a global scope.
```
function example() {
    x = 10; // Implicit global variable
}

example();
console.log(x); // 10
console.log(window.x); // 10 in a browser environment
``` 

But if you use strict mode in file like "use strict"; at beginning and you create a variable wihtout using let, const and var keyword then you will see "ReferenceError" that states variable not defined, after trying to run that file.

```
"use strict";
function example() {
    x = 10; // ReferenceError: x is not defined
}

example();
```

## What is "use strict"; ?

 "use strict"; is used in JavaScript file to make the interpreter or compiler follow new rules or latest JavaScript implementations.

Eliminates some JavaScript silent errors by changing them to throw errors: For example, assigning a value to an undeclared variable will throw an error in strict mode, while it would silently create a global variable in non-strict mode.

```
"use strict";
x = 3.14; // This will cause an error
```

Fixes mistakes that make it difficult for JavaScript engines to perform optimizations: Code in strict mode can sometimes run faster because it helps the engine perform optimizations more easily.

Prohibits some syntax likely to be defined in future versions of ECMAScript: For example, in strict mode, you cannot use with statements.

```
"use strict";
with (Math) { // This will cause an error
  x = cos(2);
}

Error:
Uncaught SyntaxError: Strict mode code may not include a with statement
```

Prevents the use of certain keywords as variable names: Strict mode reserves keywords that might be used in future versions of JavaScript, preventing them from being used as variable or function names.

```
"use strict";
var let = 1; // This will cause an error

Error:
Uncaught SyntaxError: Unexpected strict mode reserved word
```

Makes this behave more predictably: In strict mode, this remains undefined in functions that are called as standalone functions, rather than being coerced to the global object.

```
"use strict";
function test() {
  console.log(this); // undefined
}
test();
```

### Strict mode can be enabled for the entire script or for individual functions.

Entire Script

```
"use strict"; // at first line  
var x = 3.14;
```

Individual Function

```
function myFunction() {
  "use strict";
  var y = 3.14;
}
```

## Why null is object ?

There are primitive data types (the datatypes which pre-defined by JavaScript langauge) :
number, null, string, symbol, boolean, bigInt, undefined

and non primitive data types (the datatypes which are not pre-defined by JavaScript language) :
object

But if you notice null is primitive value but if you print 'typeof null' it will show type as object.

Why ? because 'Historical Reason'

The reason typeof null returns "object" is due to a bug in the original implementation of JavaScript.

JavaScript's types are represented by a tag, a fixed-length bit field.

The tag for objects was 0, and the tag for null was also 0 due to an error in the implementation.

This error was never corrected for backward compatibility reasons, as fixing it would potentially break existing code that relies on this behavior.

null is a primitive value: In the ECMAScript specification, null is classified as a primitive value, meaning it is not an object.

## Difference between undefined and null

1. 'undefined' is a default value for uninitialized variables and parameters. 'null' is explicitly assigned value by programmers to indicate no value.

2. 'undefined' is its own type. 'null' is an object (though this is considered a quirk in JavaScript).

3. 'typeof undefined' returns "undefined". 'typeof null' returns "object".

4. 'undefined == null' is 'true' because they are considered equal in value. 'undefined === null' is 'false' because they are different types.

In short; undefined is where no notion of the thing exists; it has no type, and it's never been referenced before in that scope; null is where the thing is known to exist, but it's not known what the value is.

## Javascript implicite type conversion

JavaScript automatically converts data types when operators are used with different types of operands. This behavior is known as implicit type conversion or coercion.

```
console.log("2" + 3) // output:- 23
console.log(2 + "3") // output:- 23
console.log(5.5 + "3") // output:- 5.53
```

If you use "+" operator in between two operands, in which one operand is type of string data type and another is type of number data type, then Javascript will implicitly convert number data type operand into string data type operand and later with "+" operator string concatination happens. 

### Why it not implicitly try to convert string into number while using "+" operator in between two operands?

The answer is, in javascript "+" opeartor is used for two different tasks, first for the addition of two numbers and second for concatinating two strings. So if you give one of the opearand as string type from given two opearands with "+" opeartor in between them, then it will do concatination instead of addition.
(My theory is, there are 100% chances to convert any data type into string data type but we can't garentee that Javascript will convert string data type into number, sometimes if we have "123ab" in string and if we try to convert this string to number data type it gives NaN i.e- Not a number and we can't to any math opeartion with this.)

### How Javascript evaluate expression.

Javascript read the expression with opeartor like (+ - * / %) from left to right.

for example :-
```
console.log(1 + 2 + 3 + "4") // output:- 64
console.log("1" + 2 + 3 + 4) // output:- 1234
```

In first example (1 + 2 + 3 + "4"), first from left to right 1 + 2 will be evaluated, that is 3 then with result 3 and next 3 will be added that is 3 + 3, it will be 6 and as we see next "4" is a string like 6 + "4", javascript think like we have to do concatination, it converts 6 into string data type and then perform concatination, so it becomes 64.

In second example ("1" + 2 + 3 + 4), first from left to right "1" + 2 will be evaluated, as we see "1" is a string data type, so javascript will convert next opearand also in string as we are using "+" opeartor in between both of them, so result will become "12" in stiring, which will be evaluated with next opearand 3 that is "12" + 3, as explained above, it again converted into string data type as we are using "+" opeartor and then concatination will happen. so it becomes "123" and last same, so final result will be "1234".

### In case of other opeartors than "+"
```
console.log(1 - 2 - 3 - "4" - "5") // -13

console.log("1" - "2" - 3 - 4 - 5) // -13

console.log("1" * "2" * 3 - 4 - 5) // -3
```

As other opeartors only have one usecase and not like "+" opeator which having two usecases. In that case if javascript faces such expression like shown in above example. Javascript try to convert string data types into number data type. If Javascript not able to convert some strings into number then output will show NaN.

### Implicite conversion with comparision opearators.

```
console.log("2" > 1) // output:- true
console.log(2 > "1") // output:- true
console.log(2 == "2") // output:- true
console.log(2 == "3") // output:- false
console.log(2 === "2") // output:- false
```

In above example, string opearand will be converted into number data type and then comparision happens.

"===" will do the type checking without converting the value, in above example both 2 having different data types, it will result as false.

```
console.log(null > 0) // output:- false
console.log(null == 0) // output:- false 
console.log(null >= 0) // output:- true
```

In above example, null will be converted to zero, when you use "greater than" comparision operator, note that null will be not converted to zero, if you use "equal to" opeartor because in Javascript both having different implimentations.

```
NOTE - Try to avoid comparing or doing arthimatics operations with different data type, try not to write confusing code
```

## Stack and Heap memory.

Main memory of your system is divided into two parts stack and heap memory.

When you declare a variable in Javascript it will store inside one of these memory part.

The variables which are stored in stack memory gives copy of the value and variable which are stored in heap memory gives reference of the value.

All primitive data types of Javascript are stored in stack memory part and all non-primitive data types are stored in heap memory part.

example -

The variables stored in stack memory gives copy of value when you assign it to other variable, that means original value will retain.

```
let myScore = 34;
let myNewScore = myScore; // It will copy value inside new variable.

myNewScore = 70; // changing value
console.log(myScore) // output:- 34
console.log(myNewScore) // output:- 70
```

But the variables stored in heap memory gives address (also calls reference) from memory of that value when you assign it to other variable, that means original value change if other variable also tries to change it.

```
let myDetails = {
  name: "Abhishek",
  score: 34
};

let myNewDetails = myDetails;

myNewDetails.score = 70; // Changing value

//Notice below that in both variables it is showing changed value, that means both variables are pointing to same address.
console.log(myDetails.score); // output:- 70
console.log(myNewDetails.score); // output:- 70
```

## Data type string

As we saw previously data types which are part of primitive data type, they are immutable that means original value never change when you assign it to another variable and change the value of that variable.

### There are two different types of creating string.

1. With double quotes (""), single quotes ('') and string interpolation (backticks) (``)

       (" " or ' ' or ` `) this is primitive string.
       
       Creating string like this will process fast and takes less memory.

       Primitive string don't have there properties and methods as they are not objects. But when you try to access any string method, javascript encapsulate that string to an string object, so methods will be accessible.

       In this type of string creating, adding new properties and methods are not possible.

       If you try to create new method in primitive type of string will throw and error called.

       TypeError: Cannot create property '<your property name>' on string '<your string>'

2. With String class (new String())

       (new String("your string")) this is non-primitive way of creating string. The type of this string is object.

       Creating string like this will consume more memory than primitive way.

       The type of string created with String class is object, however, the value of the variable are immutable as defination of string states. But different from creating string with primitive, in this type of creating string, new properties and methods can be added.

       Example - How can you add your own function to you string.

       let myString = new String("This is new string");

       myString.helloWorld = function() {
         console.log("Hello World!");
       }

       console.log(s2.helloWorld()); // Hello World!

## Data type number

### Formula for generate random number between A and B.

```Math.floor(Math.random() * (maxNum - minNum + 1) + minNum)```

Explaination -

```Math.random()``` - This function will generate a random floating point number between 0 and 1.

```Math.random() * (maxNum - minNum + 1)``` - This will scale your random number genearation. Normally random function will generate random number between 0 and 1 but by calculating difference between given range and multiplying with random number it will cover all numbers between given range. This will not make sense until you add minNum into it, which will be next step.

```Math.random() * (maxNum - minNum + 1) + minNum``` - Now in this step the range shifting will happen, so in previous step it covers all numbers in between range but it was starting from 1 (not from 0 because we also added 1 into it to avoid it starting from 0) now with this step the min starting number will be given minNum so range shift happen from minNum to maxNum and now it will generate the random numbers in between minNum and maxNum.

```Math.floor(Math.random() * (maxNum - minNum + 1) + minNum)``` - Wrapping into Math.floor will only take the value before decimal without considering the value after decimal. Math.floor will not consider the value after decimal and will not round the value. ex - 4.9 will be 4 only. So here finally we are getting only integer random value.

## Data type Array

### Shallow Copy

A shallow copy of an object is a copy whose properties share the same references (point to the same underlying values) as those of the source object from which the copy was made. As a result, when you change either the source or the copy, you may also cause the other object to change too.

### Deep Copy

A deep copy of an object is a copy whose properties do not share the same references (point to the same underlying values) as those of the source object from which the copy was made. As a result, when you change either the source or the copy, you can be assured you're not causing the other object to change too.

```JavaScript array-copy operations create shallow copies. ```

Example which prove that Array copy creates shallow copies.

```
// original array.
const a1 = [32, 4, 3, 56, 1];

// creating the copy of original array.
const a1c = a1;

// changing the copy array.
a1c[0] = 23;

// the output shows that changing in copy array changed the original array as well.
console.log("copy array:", a1c); // copy array: (5) [23, 4, 3, 56, 1]
console.log("orig array:", a1); // orig array: (5) [23, 4, 3, 56, 1]
```

## Data type object

There are three different types you can create objects.

1. With object literal

        const myobj = {}; // empty object

2. With object class constructor
        
        const myobj = Object.create(null) // empty object with no properties.

3. With creating new Object of object class.

        const myobj = new Object(); // empty object


### Accessing object values

```
const sym = Symbol("This is unique");

function hw2() {
    return `hw2`;
}

function hw3() {
    return `hw3`;
}

const myobj = {
    "first name": "Abhishek",
    "last name": "Kshirsagar",
    "email": "abhi.kshirsagar@google.com",
    [sym]: "A1",
    [Symbol("This is also unique")]: "A2",
    "helloworld": function () {
        return `hello world`;
    },
    helloworld2: hw2,
    [hw3]: "hw bold"
}

// Method 1 - with [] (square brackets)
console.log(myobj["first name"]); // Abhishek
console.log(myobj["email"]); // abhi.kshirsagar@google.com

// Below syntax is used to access symbol, if you use symbol as a key in object.
console.log(myobj[sym]); // A1 

//Mthod 2 - with . (dot)
console.log(myobj.email); // abhi.kshirsagar@google.com

// If space is used in between keys or symbol is used as key then this method will not work, you have to use method 1 instead.

console.log(myobj."first name"); // Incorrect syntax
console.log(myobj.sym); // Incorrect syntax to access symbol, it will result as undefined if key not found in object.
```

### Creating symbol as a key of object.

```
const mySym = Symbol("This is unique"); // OR
//const mySym = Symbol(); // You can give empty.

const myobj = {
  name: "Abhishek",
  location: "Pune",
  [mySym]: "This is symbol as a object key"
}

console.log(myobj[mySym]) // This is symbol as a object key

console.log(myobj)

// Output of above myobj object. Notice how symbol as a key looks like.

{name: 'Abhishek', location: 'Pune', Symbol(This is unique): 'This is symbol as a object key'}
location: "Pune"
name: "Abhishek"
Symbol(This is unique): "This is symbol as a object key"
[[Prototype]]: Object
```

Observe the above code, check how we have declared the symbol as a key and how we are accessing that down into a log function.

The advantage of creating symbol as a key is:

It will create a unique key, so less key conflict will happen in object, mostly if you are working with multiple libraries at a same time.

It will make keys as a private, so if anyone wants to print and loop through the keys, they will not able to do.

See, the below example in which the symbolic keys are not visible in output when you print all of the keys from object.

```
const sym = Symbol("This is unique");

function hw2() {
    return `hw2`;
}

function hw3() {
    return `hw3`;
}

const myobj = {
    "first name": "Abhishek",
    "last name": "Kshirsagar",
    "email": "abhi.kshirsagar@google.com",
    [sym]: "A1",
    [Symbol("This is also unique")]: "A2",
    "helloworld": function () {
        return `hello world`;
    },
    helloworld2: hw2,
    [hw3]: "hw bold"
}

console.log(Object.keys(myobj));

/*
output:

0: "first name"
1: "last name"
2: "email"
3: "helloworld"
4: "helloworld2"
5: "function hw3() {\r\n    return `hw3`;\r\n}"
length: 6
*/
```



### Some of the methods to declare function inside object.

```
function greet(name) {
    return `hey ${name}`;
}


const myobj2 = {
    "first name": "Abhishek",
    "last name": "Kshirsagar",
    "email": "abhi.kshirsagar@google.com",
    "greet_abhishek": greet("Abhishek"),
    "greet_JS": greet("JS"),
    "greet_Else": greet
    "helloworld": () => {
      return "Hello World!";
    }
}

console.log(myobj2.greet_JS); // hey JS
console.log(myobj2.greet_abhishek); // hey Abhishek
console.log(myobj2.greet_Else("JoJo")); // hey JoJo
console.log(myobj2.helloworld); // Hello World!
```

### Freezing object

You can modify object at any time and also object shares the same refernece, changing object copy will also change the original object.

To avoid changing object you can freeze object.

```
const obj = {
  prop1: 'value1',
  prop2: 'value2'
};

Object.freeze(obj);

obj.prop1 = 'new value'; // This will not change the value of prop1
obj.prop3 = 'value3'; // This will not add a new property to the object

console.log(obj); // { prop1: 'value1', prop2: 'value2' }
```

But Object.freeze will do the shallow freeze, means if any object contains nested object, it will only freeze outer object, and it will not freeze nested object.

To freeze nested object as well, you need to do manual freezing for each nested object.

```
const obj = {
  prop1: 'value1',
  nested: {
    prop2: 'value2'
  }
};

Object.freeze(obj);

obj.nested.prop2 = 'new value'; // This will change the value of prop2

console.log(obj); // { prop1: 'value1', nested: { prop2: 'new value' } }

// To deep freeze, you would need to freeze the nested object as well:
Object.freeze(obj.nested);
obj.nested.prop2 = 'another value'; // This will not change the value

console.log(obj); // { prop1: 'value1', nested: { prop2: 'new value' } }

```

### Merging two or more objects

There are mainly two methods, by using we can merge objects.

1. Using Object.assign()

        const o1 = {
            a: 1,
            b: 2,
            c: 3
        }
  
        const o2 = {
            d: 4
        }

        // Syntax: Object.assign(target, source)
        
        const o3 = Object.assign(o1, o2) 

        /*
        It will merge o2 into o1. That means it will modify the original object o1.
        */
        
        //OR
        // merge object without modifying original object by creating new empty object {} as a target into the syntax and merging source into it.
        
        const o4 = Object.assign({}, o1, o2);

        /* 
        Here {} empty breces acts as a target object and other objects o1 and o2 are source. So now it will merge everything into the new empty object instead of modifying existing object. 
        */

2. Using spread operator (...)


        const o1 = {
            a: 1,
            b: 2,
            c: 3
        }
  
        const o2 = {
            d: 4
        }

        //Syntax: {...o1, ...o2}

        const o3 = {...o1, ...o2}

        console.log(o3)

        /*
        It is garenteed creates a new object, without modifying the original objects, by spreading o1 and o2 into new empty object object {}.
        */

### How to check any perticular key is available in object or not.

To check whether the perticular given key is available or not before we use that key to print the value. We use the object method called hasOwnProperty().

        const o1 = {
          a: 1,
          b: 2,
          c: 3
        }

        console.log(o1.hasOwnProperty('a')) // true

        /*
        Because key named 'a' is present in object thats the reason it will print true.
        */

        console.log(o1.hasOwnProperty('car')) // false

        /*
        Because key named 'car' is not present in object thats the reason it will print false.
        */        

        //adding 'car' key into the object

        o1.car = "BMW";

        console.log(o1.hasOwnProperty('car')) // true


### Destructuring object

Instead of accessing properties of object multiple times with objectName.propertyName, it is possible to take property only which you want and call it directly with its name or it is possible to change the name of property as well if it is very long string. Destructuring is also used to take only property which you need.

```
const course = {
  courseName: "Javascript",
  coursePrice: 999,
  courseInstructorName: "Abhishek Kshirsagar"
}

//Instead of 
console.log(course.courseInstructorName) //Abhishek Kshirsagar

//Destructuring can be used
const {courseInstructorName} = course

console.log(courseInstructorName) //Abhishek Kshirsagar

//Or if the property name is big.
const {courseInstructorName:Instructor} = course

console.log(Instructor) //Abhishek Kshirsagar
```

## Functions

There are mainly two ways to define a function. Function declaration and Function expression.

### Function declaration -

Creating function defination with function keyword.

```
function myFunction() {
  return "Hello World!";
}

console.log(myFunction()) // Hello World!
```

### Function expression -

creating function defination with function keyword or without function keyword like in arrow function and initializing the return value to variable.

```
let var1 = function () {
  return "Hello World!";
}

console.log(var1()) // Hello World!
```

#### Types of function expression -

##### Named function expression -

This type of function will be useful in the case of recursion, the name of the function is used only inside the function itself.
```
let var1 = function myFunc() {
  return "Hello World!";
}

console.log(var1());
```

##### Anonymous function expression

```
let var1 = function () {
  return "Hello World!";
}

console.log(var1());
```

##### Arrow function expression

```
let var1 = () => {
  return "Hello World!";
}

console.log(var1());
```

##### Immediate Invoked Function Expression.

```
(function () {
  return "Hello World!";
})();
```

### Generator function

In JavaScript, a generator function is a special type of function that can pause its execution and later resume from where it left off. This is achieved using the function* syntax and the yield keyword. Generators provide a powerful way to work with asynchronous code, iterate over sequences, and handle complex control flows.

```
//Note: Generator functions do not have arrow function counterparts.

//Note: function and * are separate tokens, so they can be separated by whitespace or line terminators.

function* generator(i) {
  yield i;
  yield i + 10;
}

const gen = generator(10);

console.log(gen.next().value);
// Expected output: 10

console.log(gen.next().value);
// Expected output: 20

```

```
function* simpleGenerator() {
  console.log('Generator started');
  yield 1;
  console.log('Generator resumed');
  yield 2;
  console.log('Generator resumed again');
  yield 3;
  console.log('Generator finished');
}

const gen = simpleGenerator();

console.log(gen.next().value); // Output: "Generator started" and 1
console.log(gen.next().value); // Output: "Generator resumed" and 2
console.log(gen.next().value); // Output: "Generator resumed again" and 3
console.log(gen.next().value); // Output: "Generator finished" and undefined
```

1. function* Syntax: The function* keyword is used to define a generator function.

2. yield Keyword: Inside the generator function, the yield keyword is used to pause the function execution and return a value.

3. next() Method: The generator object has a next() method, which resumes the function execution from where it was paused and returns an object with value and done properties. The value property holds the yielded value, and the done property is a boolean indicating whether the generator function has completed execution.

Use case -
```
function* countGenerator() {
  let count = 0;
  while (count < 5) {
    yield count++;
  }
}

for (const value of countGenerator()) {
  console.log(value); // Output: 0, 1, 2, 3, 4
}
```

## Hoisting

Hoisting is javascript's default behaviour to move declaration to the top of function's current scope or global scope if not in function.

### Variable hoisting

```
console.log(myScore) // undefined
var myScore = 45;
```

#### Why above result is undefined.

In Javascript the variable with uninitialized will have default value undefined (that means it is uninitialized).

In case of hoisting in javascript, it will move only declaration not initialized value.

For example if we visualize above statement it will look like below.

```
var myScore; // myScore is hoisted, only declaration moved to the top of current scope.

//So above declaration is not initilized with value, so default value will be undefined, therefore below result is undefined.

console.log(myScore) // undefined

var myScore = 45;

console.log(myScore) // 45
```

#### Hoisting with var only follow functional scope.

If variable with var keyword is defined globally, then hoisting will happen on top of the global scope.

```
//Hoisting on top of global scope
var myScope; // This is visualization of hoisting, no need to declare this line in code, it happens automatically.

console.log(myScope) // undefined

var myScope = 45;

console.log(myScope) // 45
```

If variable with var keyword is defined in function scope then hoisting will happen on top of the function scope.

```
console.log(myScope) // Refference error: variable not defined.

function myFunc() {
  //Hoisting on top of functional scope
  var myScope; // This is visualization of hoisting, no need to declare this line in code, it happens automatically.

  console.log(myScope) // undefined

  var myScope = 45;

  console.log(myScope) // 45
}

myFunc();

console.log(myScope) // Refference error: variable not defined.
```

Note: Hoisting like functional scope with var keyword will not happen with block scope, because var does not follow the block scope.

```
//Hoisting on top of global scope
  var myScope; // This is visualization of hoisting, no need to declare this line in code, it happens automatically.

console.log(myScope) // undefined

if(true) {

  console.log(myScope) // undefined

  var myScope = 45;

  console.log(myScope) // 45
}

console.log(myScope) // 45
```

### Function hoisting

With function declaration, function can be accessed before it is declared, because javascript will move all function decalration to the top of the js file.

```
myFunc() // "Hello World"

function myFunc() {
  console.log("Hello World")
}
```

#### Function expression can't be hoisted.

The below function calls will give the type error called myFunc1 or myFunc2 or myFunc3 is not a function.

```
myFunc1()
myFunc2()
myFunc3()

var myFunc1 = function () {
  console.log("Hello World!");
}

var myFunc2 = function helloWorld() {
  console.log("Hello World!");
}

var myFunc3 = () => {
  console.log("Hello World!");
}
```

The below function calls will give the reference error called myFunc1 or myFunc2 or myFunc3 cannot access before initialization.

```
myFunc1()
myFunc2()
myFunc3()

let myFunc1 = function () {
  console.log("Hello World!");
}

let myFunc2 = function helloWorld() {
  console.log("Hello World!");
}

let myFunc3 = () => {
  console.log("Hello World!");
}
```

###### Why different error while defining variable with different keyword.

1) why variable defined with var shows the type error called "variable name" is not a function.

    The answer is var default nature is it will always hoist to the global scope and in the case of hoisting only declaration will hoist not initilization.

    So, when function expresson with var keyword accessed before initialization, only declaration moved to the top not initilization. Because variable became function later after initilizing function to it, so before that it is normal variable only.

    The error "variable name" is not a function is causing because we are trying to run the function by using paranthesis () but Javascript dosn't know that it is a function and what it will do before initialization. (because only declaration is moved top not initialization)

    ```
    //Hoisting visualization
    var myFunc1; // undefined

    // Because we are using paranthesis ()
    myFunc1() // myFunc1 is not a function

    // Without paranthesis
    console.log(myFunc) // undefined

    var myFunc1 = function () {
      console.log("Hello World!");
    }

    myFunc1() // Hello World!

    console.log(myFunc1) // Function
    ```

2) Variable defined with let and const.

    The variable defined with let and const also hoist on the top of the block scope, but we cannot access it before of Temporary Dead Zone.

    It means we only access the variable after the declaration.

    Let and Const will not hoist on the top of the global scope everytime like var, instead it will hoist on block scope, but still we cant access it before initilzation.

    ```
    //Hoisting visualization
    var myFunc1; // undefined

    // Because we are using paranthesis ()
    myFunc1() // cannot access myFunc1 before initialization

    // Without paranthesis
    console.log(myFunc) // cannot access myFunc1 before initialization

    let myFunc1 = function () {
      console.log("Hello World!");
    }

    myFunc1() // Hello World!

    console.log(myFunc1) // Function
    ```

## this keyword

this keyword in Javascript will give the current context of the object.

The global object is different from environment to environment, like in browser it will return Window object but in nodejs environment it will return {} empty object.

Browser -

```
console.log(this)

/*
output -
Window {window: Window, self: Window, document: document, name: '', location: Location, …}
*/
```

NodeJs -

```
console.log(this)

/*
output -
{}
*/
```

The this keyword is used to refer the current object and current object context.

For example - You have object of user which contains its username and also function which show welcome message with username. At this point you need to access what is username in object property, here your function also in same object.

```
const user = {
  username: "AbhiK",
  welcome: function () {
    console.log(`Welcome ${this.username}`);
  }
}

user.welcome(); // Welcome AbhiK

// If we change username

user.username = "Sam";

user.welcome(); // Welcome Sam
```

### What is the output of this inside object.

If we take above example and add console.log(this) in function. We will get current object in which this is called. Here this has only object scope. Thats why we are able to access username with this like this.username inside function.

```
const user = {
  username: "AbhiK",
  welcome: function () {
    console.log(`Welcome ${this.username}`);
    console.log(this)
  }
}

user.welcome(); // Welcome AbhiK
/*
{username: 'AbhiK', welcome: ƒ}
username: "AbhiK"
welcome: ƒ ()
[[Prototype]]: Object
*/

// If we change username

user.username = "Sam";

user.welcome(); // Welcome Sam
/*
{username: 'Sam', welcome: ƒ}
username: "Sam"
welcome: ƒ ()
[[Prototype]]: Object
*/
```

### Don't call this inside arrow function

Remember if you are using this inside function to call object properties, use only normal function defination with function keyword (named or anonymous) but don't use arrow function.

this inside arrow function will give {} empty object if you are in nodejs environment or Window object if you are in browser, this inside arrow function will not show current object context.

Same if we consider above example but with arrow function.


Browser -

```
const user = {
  username: "AbhiK",
  welcome: () => {
    console.log(`Welcome ${this.username}`);
    console.log(this)
  }
}

user.welcome(); // Welcome undefined
/*
Window {window: Window, self: Window, document: document, name: '', location: Location, …}
*/

// If we change username

user.username = "Sam";

user.welcome(); // Welcome undefined
/*
Window {window: Window, self: Window, document: document, name: '', location: Location, …}
*/
```

NodeJs -

```
const user = {
  username: "AbhiK",
  welcome: () => {
    console.log(`Welcome ${this.username}`);
    console.log(this)
  }
}

user.welcome(); // Welcome undefined
/*
{}
*/

// If we change username

user.username = "Sam";

user.welcome(); // Welcome undefined
/*
{}
*/
```

## Nullish Coalescing Operator (??)

The nullish coalescing (??) operator is a logical operator that returns its right-hand side operand when its left-hand side operand is null or undefined, and otherwise returns its left-hand side operand.

```
const foo = null ?? 'default string';
console.log(foo);
// Expected output: "default string"

const baz = 0 ?? 42;
console.log(baz);
// Expected output: 0
```

## How JavaScript execute the code.

1) When you run JavaScript file with browser using script tag or with node js environment. In both the way Javascript files are provided to Javascript engine like V8 engine of chorme or spidermonkey engine of firefox etc.

2) Javascript file parse the syntax with syntax parser. It converts the Javascript code into syntax that Javascript engine can understand.

3) Parsed code then interpreted one by one and executed and also hot code paths (code that frequently called) are compiled into the machine code, this is called just in time compilation because it is happening at runtime.

### What is execution context

https://www.freecodecamp.org/news/execution-context-how-javascript-works-behind-the-scenes/


## About Switch case

In Switch case if given case matches it will execute the code inside matched case also it will execute all the cases below execept default case if break not present.

```
const expr = 'Papayas';
switch (expr) {
  case 'Oranges':
    console.log('Oranges are $0.59 a pound.');
    break;
  case 'Mangoes':
  case 'Papayas':
    console.log('Mangoes and papayas are $2.79 a pound.');
    // Expected output: "Mangoes and papayas are $2.79 a pound."
    break;
  default:
    console.log(`Sorry, we are out of ${expr}.`);
}

```

## Document Object Model

The document or website is represented as a tree like stucture and each node is an object.

### Difference between innerHTML, innerText and textContent

```
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DOM</title>
</head>
<body>
    <h1>Document Object Model</h1>
    <p id="freeText"><i>here you can enter anything</i> <span style="display: none;">this is hidden part</span></p>
</body>
<script>
    const freeText = document.getElementById("freeText");
    console.log(freeText.innerHTML); // <i>here you can enter anything</i> <span style="display: none;">this is hidden part</span>

    console.log(freeText.innerText); // here you can enter anything 

    console.log(freeText.textContent); // here you can enter anything this is hidden part
</script>
</html>
```

## Event Object Properties

### Timestamp

The timeStamp read-only property of the Event interface returns the time (in milliseconds) at which the event was created.

### preventDefault

It helps to disable the default behaviour of element. Like in anchor tag redirection will stop, in text input with keypress event it stops taking input from keyboard.

### target

The read-only target property of the Event interface is a reference to the object onto which the event was dispatched.

### clientX and clientY

The clientX read-only property of the MouseEvent interface provides the horizontal and verticle coordinate within the application's viewport at which the event occurred (as opposed to the coordinate within the page).

### offsetTop and offsetLeft

The HTMLElement.offsetLeft read-only property returns the number of pixels that the upper left corner of the current element is offset to the left within the HTMLElement.offsetParent node.

The HTMLElement.offsetTop read-only property returns the distance from the outer border of the current element (including its margin) to the top padding edge of the offsetParent, the closest positioned ancestor element. 


### screenX and screenY

The screenX read-only property of the MouseEvent interface provides the horizontal and verticle coordinate (offset) of the mouse pointer in screen coordinates.

## Event propagation

Event propagation happens when element is inside another element and both of the element having same event type.

In event propagation triggering of event on one element causes triggering of event on other element too. For example if any event triggers on child element will trigger same event on parent as well or vise versa.

### Event capturing

This is the first phase in the event propagation process. When an event is triggered, it starts from the root of the DOM tree and then moves down towards the target element. By default, event handlers are not executed in this phase.

Event capturing can be enabled by passing 'true' as third parameter 

```js
document.addEventListener("click", function() {}, true)
```

### Event Bubbling

After targeting, the event traces back its path and moves back up to the root of the DOM. It is in this phase that the event handlers execute. JavaScript executes the associated event handlers in order as the event moves up the DOM tree.

Default propagation style is bubbling, it can be achived by passing false as a third parameter.

```js
document.addEventListener("click", function() {}, false)
```

## How async tasks work in JavaScript

Js is syncronized programming langague, it has only one thread to process so it cannot work on multiple lines of code at a same time.

But js can perform asyncronize execution, with the help of execution environment call, task queue etc.

When async operation comes like setTimeout, setInterval, any event etc. then web API cal or Node API call will go, it is different execution environment and setTimeout, setInterval or any event is not a part of core Js it is part of API which works with Js engine creates one environment.

After call go to API it register call-back for that call. Then after completing decided operation it will send it to execution again back to call-stack of js engine.

For-ex: If setTimeout calls and it will execute after 2 second then call go to API until that time Js will execute other code after that line.

After call reached to API it will register a call-back for that, and after 2 seconds completes it will send the code to task queue, task queue will immedieatly add everything back to callstack of js engine. Js engine pick up one by one and execute.

Task queue is added because there might be so many async tasks waiting to be exicuted, there is no other special calculation task queue will do, it just immedieatly add everything back to call-stack of js engine.

Later in this environment one more queue is added which has priority high than task queue, which will also add tasks to call-stack, it is used by fetch api

## xmlHttpRequest - Before the use of fetch

fetch came in es6 update of js but before that developers are using xmlHttpRequest API/class to make API request.

It has some readyStates which will change per different action takes place on any perticular request.


Value | State | Description
------|-------|------------
0     | UNSENT | Client has been created. open() not called yet.
1 | OPENED | open() has been called.
2 | HEADERS_RECEIVED | send() has been called, and headers and status are available.
3 | LOADING | Downloading; responseText holds partial data.
4 | DONE | The operation is complete.

```js
const req = new xmlHttpRequest();
//open(method, url, isAsyncReq, user, pass)
req.open("get", reqURL); // readyState 1

then send(null) // default body is null

req.send() // readyState 2

//then listen for onload event so after page loads we can get the data using responseText

req.addEventListener("onload", () => {
 if(req.readyState === req.DONE){ // it will check readyState 4 or not
   const data = JSON.parse(req.responseText) // it will give response in string format so required to parse in json
 } 
})
```

## Promise

Promise can be made with creating new object instance of 'Promise' class with call back function as a parameter, and call back function as well required two parameter called resolve, reject you can give any name but first parameter will return success result if promise is successful and second will return error if promise fails.

```js
// below creation of fake network request can explain how promise will be written

let promiseOne = new Promise((resolve, reject) => {

 setTimeout(() => {
  let error = false;
 
 if(!error) {
  resolve({username:"abhishek", password:"123"})
 }
 else {
  reject("something went wrong")
 }
 }, 1000)
 
})

//resolve will be connected to then() and reject will be connected to catch()

//resolve will return data to then() and then() will accept it as argument likewise happens to catch(), reject will return error and catch() will accept it as argument.

promiseOne.then((response)=> {
 console.log(response)
}).catch((error) => {
 console.log(error)
})
```

chaining of then can be possible like then().then()...catch().finally(),

first then() will return data which will go to second then() and so on.. after first then() executes then only second then() executes and so on. so if we are parsing data to .json() so no need of await keyword here likewise we use in async await format.

finally will always executes.

promise can be made without storing into variable as well.

new Promise().then().then()...catch().finally()

