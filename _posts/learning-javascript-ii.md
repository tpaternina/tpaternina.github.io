---
title: "Learning JavaScript II: loops and objects"
date: 2021-01-29 15:00:00
categories: journal codecademy javascript python
excerpt: Reviewing basic looping and learning to represent objects.
---

While going through the basics felt relatively [breezy]({% post_url 2021-01-22-learning-javascript %}){:target="_blank"}, things got gradually serious. The following sections consisted in concepts that I already knew, and others that I though I knew, but that I found harder to be familiarized with. 

## Looping around

The first loops that I reviewed were _for loops_. The syntax was not foreign to me, as it felt almost identical to Java for loops:

```javascript
let myArray = ['a', 'b', 'c', 'd']
for (let index=0 ; index < myArray.length ; index++) {
	console.log(index, myArray[index]);
	// prints the index and the element of myArray at the position of `index`
};
/** the whole loop prints:
 * 0 'a' 
 * 1 'b'
 * 2 'c'
 * 3 'd'
 */
```

In this example, we initialize our counter (`index = 0`), define the condition that will stop the loop, and define how to change our counter at the end of each iteration. In this example, the index of arrays are 0-based (the first element is at position 0), so the last element is indexed at `myArray.length - 1`. At each iteration, we print the value of `index`, then pick the element in myArray at the `index` position and print it. Then, we increase the value of `index` by 1. Once the value of our counter reaches the number of elements in the array, the condition `index < myArray.length` is no longer true, so the script breaks out of the loop. 

In principle, there was nothing new to me here. Yet, I would later find out how important it is to use the `let` statement when initializing the counter, but that's a post for another day.

As there was not much novelty with loops, I will be talking about JavaScript objects for the rest of the post. And yes, there was a lot more novelty there for me.

## JavaScript <s>dictionaries</s> objects

As an object-oriented programming language, JavaScript allows us to create abstract models of objects to represent real world objects. Objects have both properties and methods. For example, we can create a `car` object and list several properties such as maximum speed, model, year, mileage, color, current speed, oil level, gas level, etc. A method, on the other hand, is a function inside an object. They allow us to change property values and to model the actions an object performs. So, for our `car` object we can imagine writing methods such as `accelerate()`, `changeColor()`, `refuel()`, etc.

How do we write objects in JavaScript then? Well, it's up to you. So far, I have distinguished 3 different ways of writing objects: literal notation, Object constructor notation, and constructor notation.

### Literal notation

Why did I get so many Python vibes when I learned about JavaScript objects? They share some similarities indeed. Using the literal notation in JavaScript, we write object properties as key-value pairs inside curly braces. This is the same principle as Python dictionaries. However, i Python keys can be values of any type (strings, booleans, integers), while in JavaScript keys can only be strings (or symbols).

```
# A `car` dictionary in Python
car = {'brand': 'Fiat', 'year': 1990, 'color': 'white'}

// The same `car` as an object in JavaSript
let car = {
	brand: 'Fiat',
	year: 1990,
	color: 'white'
}
```
For this reason, we don't need to write object properties inside quotes in JavaScript objects (unlike Python). To access or modify the values of a particular property, we use square brackets, just like we would access the value at a particular index of an array:

```javascript
console.log(car['year']);
// prints `1990`

car['color'] = 'red';
// changes the value of the `color` property to `white`
```
Notice how we specify the property as a string when using the bracket syntax. Unlike Python dictionaries, JavaScript lets us access properties with the dot notation as well (notice how we don't need to write the property inside quotation marks):

```javascript
console.log(car.year);
// prints 1990

car.color = 'red'
// also changes the value of the `color` property
```
What happens if you want to add new properties or functionalities to an object you already created? JavaScript has your back. You can always add new properties or methods with the bracket syntax or the dot notation:

```javascript
car.speed = 70
// Adds a new property `speed` and initializes its value to `70`
```
Because we can modify objects after creating them (we can say objects are _mutable_), we can use the following syntax to create whole objects altogether.

### The Object() constructor syntax

As I mentioned before, JavaScript is an object-oriented programming (OOP) language. OOP is based on the definition of _classes_, which maybe I'll talk about more when I reach that part of the JavaScript course 😉. Briefly, classes define the blueprint of properties and methods that a particular group of objects will share. For instance, all humans have a name, an age, a skin color, a place of birth, etc. But the actual values of these properties vary from one person to the next. We can thus say that all humans are part of the `Human` class, and that each individual human is an _instance_ of this class.

What does this have to do with objects? Well, all JavaScript objects are instances of the _Object_ class. Class instances are created with a special function that we call a constructor (by convention, these functions begin with a capital letter). So, we can use the `Object()` constructor to create new empty objects using the following syntax:

```javascript
let car = new Object();
```

Notice the `new` statement before the `Object()` constructor. Once this empty object is created, we can add the properties we want using bracket syntax or dot notation:
```javascript
car.year  = 1990;
car.color = 'white';
car['registration date'] = '15/11/1990';
car.speed = 70;
```
Like literal notation, the `Object()` constructor syntax allows us to create and modify an individual object. But what if we want to create several objects that share the same properties?

### The constructor notation

I must admit that this notation gave me a <i>déjà-vu</i> of writing Java classes. However, writing JavaScript notations feels like a more concise, short way of writing object classes (think of [Dr. Evil and Mini-Me](https://bit.ly/3t6lWME)). 

The advantage of this notation is that we only need to write the properties of the object we want to create once. The particular values of these properties can be specified at the moment of calling the constructor, or after the object is created:
```javascript
function Car(color, year, brand) {
	this.color = color;
	this.year = year;
	this.brand = brand
}

// create first car
let myCar = new Car('white', 1990, 'Fiat');

// create another car
let friendCar = new Car('black', 2018, 'Renault');

console.log(`My car is a ${myCar.brand}. My friend's car is a ${friendCar.brand}`);
// Prints `My car is a Fiat. My friend's car is a Renault`
```
Notice how we call the `Car()` constructor with the `new` statement. In this example, the arguments of the constructor correspond to the values we want to assign to the properties of the new object.

Another thing worth noting is the `this` object. In the context of an object, `this` refers to the object itself. So, `this.color` refers to the `color`property of the `Car` object in our example. This is important because there is a difference between the scope of an object's properties, and the variables and functions defined outside of the object.

#### Object factories: functions that return objects

When talking about ways of creating objects, I cannot skip the functions that return objects, as they are a valid option as well. They differ from constructor functions as they use the `return` statement, and do not require the `new` statement when they are called.

As with object constructors, with these functions we only need to write the properties of our objects once, and it is possible to specify their value when creating each individual object:

```javascript
function createCar(color, year, brand) {
	return {
		color: color,
		year: year,
		brand: brand
	};
}

// create first car
let myCar = createCar('white', 1990, 'Fiat');

// create another car
let momCar = createCar('gray', 2009, 'Ford');

console.log(`My car is ${myCar.color}, and my mom's car is ${momCar.color}.`)
// Prints `My car is white, and my mom's car is gray.`

```
Notice how we don't need to use the `this` object when declaring the objects properties. Something that I find quite practical with this syntax, is _shorthand declaration_. This allows us to define properties using the name of the functions arguments without typing the same words:

```javascript
function createCar(color, year, brand) {
	return {
		color,
		year,
		brand
	};
}
```
I will take any chance I have to type less if JavaScript gives me that option!

## Adding functionality to our objects with methods

So far, I have given examples where our objects only have _properties_ or characteristics, but as I mentioned before, we can add some functionality to our objects with _methods_. Put simply, methods are functions inside objects, and we can use them to change properties or to model the actions of an object:
```javascript
let car = {
	brand: 'Fiat',
	color: 'white',
	year: 1990,
	speed: 0,

	// increases the speed of the car by `increment`
	accelerate: function(increment) {
		this.speed += increment;
	},
	// stops the car by setting the speed to 0
	stop: function() {
		this.speed = 0;
	}
}
```

When we define methods that use or modify the object's properties we need to tell JavaScript that we refer to the properties inside the object. This is where the `this` statement is important. If we don't write `this.speed` to access the speed of the `car` object, JavaScript is going to look for a global variable named `speed` and use it instead. Skipping the `this` keyword can have undesirable effects. If we haven't defined a global variable that has the same name as the property we want to access, the script is going to throw an error message. But if such a variable exists elsewhere in the code, things can get really messy, as the method points to the global variable and not the property we want to change:
```javascript
// My favorite color (a global variable)
let color = 'red';

// Add a method to the `car` object that intends to change its color 
car.paint = function(newColor) {
	color = newColor;
}

// Try the method
car.paint('blue');

console.log(car.color);
// Prints 'white' because the method changes the `color` variable defined outside of the object

console.log(color);
// Prints 'blue'
```
So, the right way to write the `paint()` method would be:
```javascript
car.paint = function(newColor){
	this.color = newColor;
}
```
Now that that is clear, let's take a look now at how we can write methods. In the examples above I have used function assignment, and if you thought JavaScript was going to offer just one way of doing things, [you are wrong]({% post_url 2021-01-22-learning-javascript %}/#the-variants-of-functions){:target="_blank"}. 

In the previous post, I pointed at how many different ways there are to write a function in JavaScript. Well, turns out that methods are not spared from this. Besides function assignment, we can define methods with a totally different syntax:
```javascript
let car = {
	color: 'white',
	speed: 70,

	paint (newColor) {
		this.color = newColor;
	},
	stop () {
		this.speed = 0;
	}
}
```
We can write the name of the function followed by a pair of parentheses (with or without a blank space between the name and the parentheses). If our function takes arguments, we write them inside the parentheses (as you can see in the `paint()` function above).

If you're thinking you can use any of the ways to write functions to write methods, **you are wrong again**. While testing the examples of this post on the node command line, I noticed the function declaration and the arrow function were not working as I expected. While function declaration throws a syntax error, arrow functions are allowed inside objects. Yet, we need to be careful when using arrow functions as methods. 

```javascript
let color = 'red';

let car = {
	color: 'white'
} 

car.paint = (newColor) => { this.color = newColor; };

// Try to change the car color with the paint method
car.paint('blue');

// Car color hasn't changed
console.log(car.color);

// But global `color` did
console.log(color);
```
What happened? Why did the global `color` variable changed instead of the `car` color property? I found he answer to this on [Stack Overflow](https://stackoverflow.com/questions/31095710/methods-in-es6-objects-using-arrow-functions):
```javascript
// Whatever `this` is here...
var chopper = {
    owner: 'Zed',
    getOwner: () => {
        return this.owner;    // ...is what `this` is here.
    }
}; 
```
Which means that arrow functions understand `this` as the global object rather than our `car` object. This is also mentioned in the <abbr title="Mozilla Developer Network">MDN</abbr> documentation:

<blockquote cite="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions">
	An <strong>arrow function expression</strong> is a compact alternative to a traditional function expression, but is limited and can't be used in all situations.<br /><br />
	<strong>Differences & Limitations:</strong>
	<ul>
	 <li>Does not have its own bindings to this or super, and should not be used as methods.</li>
	</ul>
</blockquote>

Basically, it's better if we avoid arrow function expressions inside objects.

## Conclusion

Wow, that was a long post. I wanted to summarize what I learned in this second part of the course as best as I could. I realized that I had to go a bit into detail in order to be clear, and so I ended up writing a lot more than what I expected.

There are many things about the basics of JavaScript that I can talk about, such as iterators, object getters and setters, string formatting, array methods, and many others that I can't think about right now. 

As I write this post, I realize that I'm summarizing the knowledge I get from the courses, while consulting the resources that I have at hand. Although that is valuable to me as a learner, I don't want to write a full-stack development course. My purpose is to record my impressions and my experience throughout this journey. Although I have tried to do that with the two last posts, I think from now on I will focus more on my experience than on the technical aspects of what I am learning.

I hope the post was still helpful to you. If you want to dig deeper, you can find the resources I used below. If you have a question about something that I explained but wasn't clear, you can contact me on LinkedIn or GitHub.

See you next time!

## Sources

* [Codecademy JavaScript course.](https://www.codecademy.com/learn/introduction-to-javascript){:target="_blank"}
* [JavaScript & jQuery](http://javascriptbook.com/){:target="_blank"} by Jon Duckett.
* [MDN reference pages](https://developer.mozilla.org/en-US/docs/Web/JavaScript){:target="_blank"}: a very comprehensive documentation about the JavaScript language, with tutorials and examples. A great advantage: it's translated into multiple languages!
