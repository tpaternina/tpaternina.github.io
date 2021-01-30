---
title: "Learning JavaScript I: variables and functions"
date: 2021-01-22 15:00:00
categories: journal codecademy JavaScript python
excerpt: Comparing the first steps in JavaScript to my knowledge in Python.
---

A website is built with 3 basic ingredients: HTML for the content, CSS for the style, and JavaScript for interactivity. My journey towards web development starts with JavaScript. In this post I am going to summarize my experience learning the basics of JavaScript.

## I have been down this road

Before I dive in, I need to give full disclosure. As I mentioned in [my first post]({% post_url 2021-01-04-starting_my_next_adventure %}), I went to graduate school to learn bioinformatics, and thus get closer to computer science. This means I am not new to coding. I first learned to implement algorithms with Python. I got introduced to Object Oriented Programming (OOP) with Java. Then, I learned statistics and machine learning with R. During my PhD, I developed my command line skills with bash, and analyzed my data with Python (thank you Pandas, Seaborn, and scikit-learn). 

I don't mean to brag about my skills, but to be clear about my perspective. My experience here is going to be different from someone who just started to learn to code, or from someone that has been coding in C++ for years and has decided to learn web development. I am not a newbie, but I have tons to learn!

With that in mind, let's talk about the basics of JavaScript. 

## (Re)starting from scratch

I started the Codecademy free version of the JavaScript course back in November. Before taking a big pause to help my family move houses, I went through around 40% of the modules. Luckily, when I subscribed to the Pro version of Codecademy, my JavaScript progress was taken into account for the Full-stack developer career path. So, technically, I didn't need to go through the JavaScript modules I had completed. 

But that would have been too easy.

Because I had made a big pause, I decided to go through the basics *again*, to fully grasp the characteristics of the language. This included variable declaration, data types, functions, and conditional statements.

Spoilers: it wasn't thrilling. 

## The variants of variables

Getting familiarized with the syntax of JavaScript is not too hard when you have had some experience with Java. Now,to be clear, they are not the same *at all*. But they do share some similarities in how we declare and modify variables:

```javascript
let emptyVariable;
let variable =  0;
variable += 2;
const message = 'You rise with the Moon, I rise with the Sun.';
```

As a python-head, I was not used to declare variables with the keywords `let` and `const`, nor to end my lines with semicolons. Also, knowing some Java, I noticed that declaring the variable type is not necessary (which is known as [weak typing](https://en.wikipedia.org/wiki/Strong_and_weak_typing)). So, the `let/const` keywords lets you know that the following code is a variable...or does it?

Before answering that question, let's take a quick look at the difference between `let` and `const`. While `let` defines variables that can be changed (this is useful if we want to update values as or code runs), the value of `const` variable cannot be changed after we initialize it:

```javascript
let myAge = 28;
// Oh, it's my birthday
myAge = 29;

// I was born on this year, it does not change
const birthYear = 1992;
birthYear = 1993;
// Throws TypeError
```

That seems simple, straightforward. However, the value inside a variable can change if the data type is *mutable*, independently of whether it was declared with `let` or `const`. An example of mutable data type is the Array object. We can modify the values within the array, add or delete elements. However, if the array was stored in a `const` variable, we cannot reassign the value:

```javascript
const list = ['Katara', 'Zuko', 'Aang', 'Sokka'];

// We can add another element to the array
list.push('Toph');

// But we cannot assign a different value to `list`
list = ['Azula', 'Mai', 'Ty Lee']; 
// Throws TypeError
```
It is worth noting that variables cannot be re-declared, either with `let` or `const` variables. So, if you want to change the value inside a function, you can assign the new value to a `let` variable, *without* using the `let` statement:
```javascript
let myAge = 23;

// This throws a SyntaxError
let myAge = 28;

// This works
myAge = 28;
```

So, every time we use the `const` and `let` keywords we assign values to variables, right? Well...

## The variants of functions

While Python functions are written with the keyword `def`, there are many ways to write functions with JavaScript. One of them is *function assignment*, where we write a function and assign its "value" to a variable:

```javascript
const hello = function(user) {
  return `Hello ${user}!`;
};
```

In this example the variable `hello` points to the function that takes the argument `user` and returns the string `Hello {user}`, where `user` is replaced with the value of the argument. Later, we would write the name of the variable `hello` with parentheses to call our function:

```javascript
console.log(hello('Momo'));
// prints 'Hello Momo!' to the console
```

Although I was not familiar with this logic, it's not too different than writing a function in Python and assign it to a variable (which can also be done in JavaScript, by the way):

```python
def hello(user):
  return 'Hello {}!'.format(user)

greet = hello

print(hello('Momo'))
# Prints 'Hello Momo!'

print(greet('Momo'))
# Prints 'Hello Momo!'
```

After all, the names of the variables that we create are pointers to the place in memory where the values are stored. 

If you are looking for another way to write functions, JavaScript has your back. Function declaration uses the `function` statement instead of assigning an anonymous function to a variable:

```javascript
function hello(user) {
  return `Hello ${user}!`;
}
```
According to the Codecademy material, the main difference between function declaration and function assignment is the order of execution when the script runs. Function declarations run before variable declarations, so whe can declare a function *after* writing code that calls that function:

```javascript
console.log(hello('Momo'));

function hello(user) {
  return `Hello ${user}!`;
};
```

On the other hand, we cannot call a function before writing it if we decide to use function assignment:

```javascript
console.log(hello('Momo'));
// Throws a Reference error because hello() has not been defined yet

const hello = function(user) {
  return `Hello ${user}!`;
};

```

So, the choice depends on how you want your code to be read. Personally, I think that defining functions prior to calling them, regardless of how I write them, provides more clarity to my scripts.

### This is not over: arrow functions

For the developers of JavaScript, it wasn't enough to create two different ways of writing functions. They realized that they had to type too many characters to define functions, so they came up with *arrow functions*. 

```javascript
// A function with no arguments (we don't need the return statement)
const greet = () => 'Hello user!';

// A function with one argument
const greeUser = user => `Hello ${user}`;

/** With curly braces, we can write multi-line functions
But we need the return statement (don't repeat my mistakes)
*/
const greetUserMultiline = user => {
	const string = `Hello ${user}!`;
	return string; 
};

// A function with two arguments
const greetUsers = (user1, user2) => `Hello ${user1} and ${user2}!`;
```

Arrow functions [have several limitations](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions). For the moment, all I know is that arrow functions don't need with the `function` statement. I am currently using arrow functions only when doing function assignment or when I need an anonymous function (for instance, to iterate through an array).

Coming from the Python universe, I felt surprised (and at times *overwhelmed*) with the number of function variants in JavaScript. In Python I only used the `fun` statement for named functions, and the `lambda` statement for anonymous functions. In JavaScript, three variations, each with specific syntax (which varied also for arrow functions depending on the number of arguments and lines of code), felt like a lot. But I guess it's just a matter of habit and knowing in which context each of them should be used.

## Closing remarks

Although getting used to writing functions and declaring variables required some time, I must admit that I advanced quickly through the quizzes and projects of these sections. Indeed, JavaScript has a syntax that I wasn't familiar wit. But as is usual with programming courses, the introductory sections covered basic programming concepts that I was already aware of.

I was wrong to think the following sections would be as breezy. In the following post I will be talking about how I dealt with Objects, and I will be ranting about functions again.

Thank you for reading, and see you next time!
