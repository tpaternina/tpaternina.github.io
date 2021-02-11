---
title: "The Mysterious Organism Project"
date: 2021-02-12 15:00:00
categories: journal codecademy javascript 
excerpt: A walkthrough of my favorite project on Codecademy so far.
---

Many days since I finished JS intro. favorite project/i enjoyed was mystery organism: biology, with dna sequences, doesn't hit far from home.

## Simulating a new micro-organism

P. aequor isa fictional org lives bottom ofthe ocean. Its entire genome is 15 base pair long for referece, human genome is over 3 billion base pairs jéjé). 

simply, dna is a chain of 4 letters: ACTG. These are called bases Codecademy provides two functions: one to provide a random base from the four, and another to generate a random strand of dna.

From here we have to simulate a P. aequor organism using a JS object. The idea is to make things easier for the researchers that disvcovered the organism to study it.

Simple b/c we only have two attr: the specimen number (to identify diff. orgs) and the DNA sequence. What will be more intresting is to add functionality to our little paequors.

### Add mutations

Sometimes, DNA mutates, this means its sequence is altered. Altough there are many types of mutations, we will only simulate point mutations (check), where a single base is replaced by another.

... (show example)

### Comparing two paequors

When working with DNa sequences we're often interested in comparing diff. sequences. although powerful algorithm exist to align and compare seq. we will only do a simple identity comparison. Comparing at position eah position, we want to count how many bases are identical. We'll express the identity as a percentage (100% two identical sequences, 0% completely different sequences).

### Genetically strong paequors

Not get too specific, but the higher the amount of G and C in a DNa, more stable the molecule is. In this exercise we consider that paeqors with high GC content are more likely to survive than their low-GC peers. Create a function to check whehter a paequor specimen is likely to survive:

1. Get the number of Gs and Cs in Na sequence
2. compute the fraction of GC over totl length
3. If this is above  threshold (here we consider 60%), paquor is likely to survive.

Initially, I printed both sequences, but became cluttering. With all the steps we wanted to print. I decided to ad a return statement besides the console log for a later step.

Now we can create two diff. specimens and find their percentage of identity. 

...

### Natural selection with a JS list

Select a collection of strong paequors using the likelsurvive function.


### Finding the two most similar paequors with a matrix

Matrices are very useful when you want to compare o make an operation with all possible pairs of elements from an array. 

## Conclusion