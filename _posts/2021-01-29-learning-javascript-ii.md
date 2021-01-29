---
title: "Learning JavaScript II: loops and objects"
date: 2021-01-23 15:00:00
categories: journal codecademy javascript python
excerpt: Discovering the different ways of iterating and representing objects.
---

While going through the basics felt relatively [breezy](% post_url 2021-01-22-learning-javascript %), things got gradually serious. The following sections consisted in concepts that I already knew, and others that I though I knew, but that I found harder to be familiarized with. 

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

## Javascript --dictionaries--
