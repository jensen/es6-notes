# ES6

In order for a language to take on new features, browsers need to build in support. There is a process for standardization of the language that we know as JavaScript. The goal is that a piece of code run once will run the same in all of the browsers that claim support. This isn't always the case, but things are better than they used to be.

There is a standard called ECMAScript that is based off of the original JavaScript design. In June 2015 the 6th version of ECMAScript was agreed upon. Browsers are still in the process of supporting the new features of ES6 in JavaScript.

## Quick History

Brendan Eich wrote JavaScript in 10 days, in May 1995. This was a result of the necessity of an interpreted language for the ever growing web. Netscape Navigator shipped with the first implementation of LiveScript in September which was later remnamed to JavaScript for the December release.

In 1996 JavaScript was submitted to Ecma International for standardization. Eight months later the first version of ECMAScript was released.

Between 1997 and 2005 JavaScript existed. New versions were released, browsers were implementing some of the features, and there was some drama between key figures in the commmunity around the direction of standardization. Wikipedia has an article on [JavaScript#Standardization](https://en.wikipedia.org/wiki/JavaScript#Standardization). 

In 2005 the open source community defined Ajax which lead to the development of jQuery. This was a huge milestone in the advancement of the web as a platform for applications. Four years later, at the end of 2009, ECMAScript 5 was released.

In June 2015 ES6 (ECMAScript 2015) was released. It seems like they are on a more steady release schedule falling on June of every year.

## Browser support

There are four major browsers in use today. Each of these browsers has it's own JavaScript engine.

```
+-------------+---------+-------------------+
| Corporation | Browser | JavaScript Engine |
+-------------+---------+-------------------+
| Mozilla     | Firefox | SpiderMonkey      |
| Google      | Chrome  | V8                |
| Microsoft   | Edge    | Chakra            |
| Apple       | Safari  | JavaScriptCore    |
+-------------+---------+-------------------+
```

The JavaScript engine is responsible for parsing the JavaScript source code and executing the code as fast as it can. You can see a ES6 feature compatibility table at [https://kangax.github.io/compat-table/es6/](https://kangax.github.io/compat-table/es6/).

> It is important to note that V8 is the same JavaScript engine that we find in NodeJS.

## Transpiling and Polyfills

We want to write code that follows a standard. We want our code act predictably. 

There are a few solutions currently in use today to make up for the lack of language/feature support in browsers. 

- We can write ES6 code and then **transpile** it to ES5 which is supported by modern browsers.
- A library that provides support for a feature that isn't supported by the browser yet is called a **polyfill**. A polyfill will check to see if the browser supports the feature it is meant to fill in for. If the browser doesn't support the feature then the polyfill will fill in to provide support.

> The json2.js library, which allowed reading and writing of the JSON data format, became so popular that JSON support was built in to browsers. The original library was then converted in to a polyfill.

## Features of ES5

### 'use strict'; (Strict Mode)

The `'use strict';` directive is a feature that has existed since ES5. It is important enough to make specific mention of before we move on to ES6. When defined at the top of a .js file the interpreter will handle the execution of the code contained in that file in a strict way.

Strict means, for example:

- Can no longer do variable assignment if the variable hasn't been defined with `var`. Without strict the variable would be created on the global scope.
- Usage of `eval` is restricted.
- The `with(){}` statement is no longer usable.

You can start a specific function with `'use strict';` and only exection within the function scope will be handled in a strict way.

It is up to you if you want to use this. If you come across it, it is important to understand why it is there.

- [Strict Mode - MDN Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)
- [Vaz's Notes on Strict Mode](https://gist.github.com/vaz/797a0e233e6ae75df5ecec2c27f4088a#file-1_use_strict-js)

## Features of ES6

### let, const, var

Up until ES6 we only had the function scoped `var`. With ES6 come two new ways to declare variables. If we would like to be more specific with our scoping of a variable we can use `let`. The `let` keyword declares a variable to be in scope only within the block it is declared.

Examples of a block:

```javascript
for(let i = 0; i < 10; i += 1) {
  // i is only available within for-loop
}

if(true) {
  let i = 0;
  // i is only available within if statement
}

let i = 0;
{
  let i = 1;
  // i is 1 inside this block statement
  // used very rarely
}
```

We can use `const` to specify that we want to prevent re-assignment of a variable. We can still modify the values inside an object or array, we simply cannot assign to the variable a different value.

```javascript
const obj = {
  changeable: 'unchanged'
}

console.log(obj);

obj = 'unchangeable'; // produces a TypeError

obj.changeable = 'changed';

console.log(obj);
```

The `var` keyword will live on, but you should be able to write new code using `let` and `const` primarily.

- [let - MDN Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
- [const - MDN Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
- [var - MDN Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)
- [Vaz's notes on let/const/var](https://gist.github.com/vaz/797a0e233e6ae75df5ecec2c27f4088a#file-4_let_and_const-js)

### for...of or for...in

The `for...of` statement is used to **interate** over **iterable** objects. The most common iterable objects would be `Array, String, Set and Map`. You can also create your own objects that are iterable. 

```javascript
const list = [1, 2, 3, 4];

for(const item of list) {
  console.log(item);
}
for(let item of list) {
  item += 1;
  console.log(item);
}
```

- [for...of - MDN Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)
- [Vaz's notes on for...of](https://gist.github.com/vaz/797a0e233e6ae75df5ecec2c27f4088a#file-3_for_of-js)

It is easy to confuse this with `for...in` which is used to interate through the properties of an object. The two will behave quite differently, for example you cannot call `for...of` on an object.

### Template Literals

With normal strings you tend to concatenate a lot of variables.

```javascript
const date = {
  dow: 'Tuesday',
  day: 14,
  month: 'February',
  year: 2017
};

console.log('The date today is ' + date.dow + ' ' + date.month + ' ' + date.day + ', ' + date.year);
```

> Don't actually do this with dates. Use a date formatter. Seriously.

If you use a template literal then the code becomes a bit more clear.

```javascript
console.log(`The date today is ${date.dow} ${date.month} ${date.day}, ${date.year}`);
```

You could include any JavaScript expression you want inside the braces.

```javascript
console.log(`100 * 200 = ${100 * 200}`);
```

- [Template Literals - MDN Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
- [Vaz's notes on Template Literals](https://gist.github.com/vaz/797a0e233e6ae75df5ecec2c27f4088a#file-5_string_interp-js)

### Arrow Functions

Standard anonymous function passed as an argument to the Array.prototype.map function.

```javascript
[1, 2, 3, 4].map(function(value) {
  return value * value;
});
```

We could use the short-hand arrow function instead.

```javascript
// in this case we remove the function keyword and add the arrow
[1, 2, 3, 4].map((value) => {
  return value * value;
});

// if there is a single parameter and a single expression within the function, we can omit the parenthesis and return keyword
[1, 2, 3, 4].map(value => value * value);
```

Other than syntactic sugar the major difference between regular function declarations and arrow functions is how they handle `this` context. Unlike a regular function declaration, an arrow function inherits `this` from the scope it is declared in.

Use the following guidelines for choosing which style to use. Thanks Vaz!

- Top level functions should use `function`.
- Functions meant to be invoked with a `this` context must use `function`.
- Functions defined and passed inline as arguments are good candidates for arrow functions.

Oh, and don't forget. Arrow functions are **always** anonymous.

- [Arrow Functions - MDN Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- [Vaz's notes on Arrow Functions](https://gist.github.com/vaz/797a0e233e6ae75df5ecec2c27f4088a#file-6_arrows-js)

## More ES6

We were only able to cover a few of the useful features of ES6. There are plenty more. A good place to check out a list is [http://es6-features.org/](http://es6-features.org/)

- Class Syntax
- Generators
- Promises
- Destructuring Assignment
- Modules
- Enhanced Object Properties
- Generators

## Bonus

There is a cool tool called Python Tutor. Even though it started as a way to visualize python code exectution, support for many more languages has been added. There is support for the visualization of your JavaScript code execution.

Eventually you shouldn't need the tutor to visualize the path your code is taking. Try to practice by getting some code you didn't write. Take a look and try and imagine how the code is being executed. You can verify by using the [Python Tutor](http://pythontutor.com/) site.

["Cool tools rule. Cool tools."](https://www.youtube.com/watch?v=nKHHDSpY06c)