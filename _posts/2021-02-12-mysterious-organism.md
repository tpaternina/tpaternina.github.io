---
title: "The Mysterious Organism Project"
date: 2021-02-12
categories: journal codecademy javascript 
excerpt: A walkthrough of my favorite project on Codecademy so far.
---

Another week went by and as I was thinking about what to write about, it occurred to me to do a short walkthrough of the Codecademy project I have enjoyed the most so far.

It deals with object creation and a bit of iteration in JavaScript, and the theme is DNA sequences, something I'm rather familiar with 😏.

## Simulating _paequor_, a new micro-organism

A team of scientists has discovered a new micro-organism that lives in the bottom of the ocean. They have named it _Pila aequor_, but we will call it  _paequor_ for the sake of simplicity. 

The scientists have isolated paequor DNA and found its sequence. Put simply, DNA is a chain of 4 molecules that we represent with four letters: A, C, T, and G. Two strands of DNA interact by pairing G's with C's, and A's with T's, forming the famous DNA double helix (see figure below).

![DNA structure](/assets/images/Dna-base-flipping.svg)
<figcaption style="text-align: center;">A representation of the DNA double helix. On the left, each base is represented with a color and a letter: C for cytosine (blue), G for guanine (green), A for adenosine (yellow), and T for thymine (red). On the right, a representation of DNA double helix, where A pairs with T, and G pairs with C. I found this image on <a href="https://commons.wikimedia.org/wiki/File:Dna-base-flipping.svg">Wikipedia</a>, don't judge.</figcaption>

The DNA sequence of paequors is 15 base pair long. To have some perspective, human DNA is 3 billion base pair long, divided into 23 chromosomes. The shortest known DNA sequence is over 580 000 base pairs, and it belongs to the bacterium [_M. genitalium_](https://en.wikipedia.org/wiki/Mycoplasma_genitalium#Genome). This makes paequor's DNA sequence extra **extra** tiny, but it also makes our work much **much** easier.

ALthough it has a simple genome, paequors are hard to study because they live near hydrothermal vents in the bottom of the ocean. With the high pressure and the high temperatures, scientists said "we're not going down there" (okay, I made that up). So, our job is to make a program that allows scientists to simulate paequors and simplify their research.

Codecademy provides two functions to simulate paequor DNA. The first returns one base (remember, A, C, T, or G) at random. The second uses the first function to build an array of 15 random bases and return it as the DNA sequence of 1 paequor.

```javascript
// Returns a random DNA base
const returnRandBase = () => {
  const dnaBases = ['A', 'T', 'C', 'G'];
  return dnaBases[Math.floor(Math.random() * 4)];
};

// Returns a random single strand of DNA containing 15 bases
const mockUpStrand = () => {
  const newStrand = [];
  for (let i = 0; i < 15; i++) {
    newStrand.push(returnRandBase());
  }
  return newStrand;
};
```

From this starting point, our job is to build a JavaScript object that represents a paequor specimen. We will need only two attributes: the specimen number or ID, and its DNA sequence. To create several paequors with less lines of code, we will create a "factory", in other words, a function that returns paequor objects:

```javascript
function pAequorFactory(specimenNum, dna) {
  return {
    specimenNum,
    dna
  }
```

We will add functionality to our little paequors by writing methods inside the object returned by the ```pAqeuorFactory()``` function.

### Mutate the DNA

When a DNA sequence is modified, we say it _mutates_. Although many types of mutations exist in the real world, we will only simulate a mutation where one base is changed by another. This is what we call a _point mutation_ (sometimes it also means deleting or adding bases, but we will not consider those).

```javascript
mutate () {
  // select one base randomly
  const dnaIndex = Math.floor(Math.random() * 15);
  const base = this.dna[dnaIndex];

  // select one mutation randomly
  // we don't want the mutation to be the same as the target base
  let mutation;
  do {
    mutation = returnRandBase();
  } while (mutation === base);

  // mutate the selected DNA base
  this.dna[dnaIndex] = mutation;
  
}
```
<figcaption style="text-align: center;">Remember, this method is written inside our <code>factory()</code> function.</figcaption>

We can now create a paequor and mutate its DNA as much as we want:

```javascript
// Create a P. aequor specimen
const paequor1 = pAequorFactory(1, mockUpStrand());

// Print the original DNA sequence
console.log(`\nSimulate a mutation on specimen ${paequor1.specimenNum}:`)
console.log(`${paequor1.dna.join('')} (original)`)

// Mutate the DNA
paequor1.mutate()
console.log(`${paequor1.dna.join('')} (after mutation)`)
```

This would print, for example:
```
Simulate a mutation on specimen 1:
GCTCTCAAATGACTT (original)
GCTCTCAAATGGCTT (after mutation)
```
We can see that the last A in the original sequence was replaced by a G after mutating. If I ran this code again, I would probably obtain a different sequence and a different mutation. That's because we're using randomness to build the sequences, to select the mutated base, and to choose the base we want to replace it with.

### Comparing two paequors

When working with DNA, we're often interested in comparing different sequences. Although there are powerful algorithms to align and compare sequences, we will only do a simple identity comparison. To know the identity of two sequences, we count how many bases are identical and have the same position. The identity is expressed as a percentage, meaning that 100% identity means two sequences are identical, and 0% identity means they are completely different.

```javascript
// pass another paeqour object as argument
compareDNA (other) {
  // compare each position
  let identical = 0;
  for (let i = 0 ; i < this.dna.length ; i++) {
    const thisBase = this.dna[i];
    const otherBase= pAquor.dna[i];
    if (thisBase === otherBase) { identical++; }
  }

  // Show the two sequences
  console.log(`${this.dna}`);
  console.log(`${pAquor.dna}`);

  // compute percentage of identity (keep only two decimals)
  const identity = identical * 100 / this.dna.length;
  console.log(`Specimens ${this.specimenNum} and ${pAquor.specimenNum} have ${identity.toFixed(2)}% DNA in common.`);
  return identity;

}
```

I added a console log to print both sequences in case the scientist want to have a closer look at the two specimens. I also added a return statement because I will need it [later](#finding-the-two-most-similar-paequors-with-a-matrix). 

Now we can create another specimen, compare it to our first paequor and find the percentage of identity:

```javascript
// Compare DNA of two specimens
const paequor2 = pAequorFactory(2, mockUpStrand());
paequor1.compareDNA(paequor2);
```
This would print, for example:
```
G,G,A,C,G,T,C,G,A,A,C,C,A,C,G
A,A,T,T,A,G,A,C,A,G,T,A,C,A,G
Specimens 1 and 2 have 13.33% DNA in common.
```

### Genetically strong paequors

Paequors are more likely to survive if they have a high percentage of GC in their DNA. I don't want to go too much into detail, but due to the chemistry of DNA, the higher the amount of G and C, the more stable a DNA molecule is. In this exercise, I will consider _strong_ paequors as those who have a GC percentage above 60%. To determine whether a paequor is strong, we write the following method inside the ```factory()``` function:

```javascript
willLikelySurvive () {
  // compute the number of GC
  const gcCount = this.dna.filter(base => base === 'G' || base === 'C');
  // compute the percentage of GC
  const gcPerc = gcCount.length * 100 / this.dna.length;

  return (gcPerc >= 60);
}
```

### Natural selection with a JS array

The next exercise consists on creating a collection of 30 strong paequors. This would be similar to applying a treatment or changing an environmental condition that removes the least adapted organisms and favors the most resistant ones. 

To do this, we can simply create an array and progressively add paequors that are likely to survive (we will use our ```willLikelySurvive()``` function):

```javascript
const strongPaequor = [];

// We will use numGenerator as the specimen ID
// We start at 3 because we have already created 2 paequors.
let numGenerator = 3
while (strongPaequor.length < 30) {
  let paequor = pAequorFactory(numGenerator, mockUpStrand());
  if (paequor.willLikelySurvive()) {
    strongPaequor.push(paequor);
  }
  numGenerator++
}
```
To know which paequors live in our ```strong``` collection, I added an ```identify()``` method to the paequor object. It prints the paequor specimen ID and its DNA sequence:

```javascript
identify() {
  console.log(`Num. ${this.specimenNum}. Genome: ${this.dna.join('')}`)
}
```
<figcaption style="text-align: center;">"Genome" is the whole DNA sequence of an organism.</figcaption>

Now we can ask all the strong paequors to identify themselves:
```javascript
console.log(`List of strong P. aequor specimens:`);
strongPaequor.forEach(paequor => paequor.identify());
```
Which would print something like:
```
List of strong P. aequor specimens:
Num. 6. Genome: CACACGTTCAGGCGC
Num. 18. Genome: ACCTAGCCCACCACA
Num. 25. Genome: GATCCTCGTGGTGCC
Num. 27. Genome: CCCTGGCATGAAGCA
...
```

### Finding the two most similar paequors with a matrix

One last exercise was to find the pair of paequors that shared the highest DNA idendity. To do this I implemented a matrix, because it is very useful to compare, or to perform an operation on all the possible pairs of elements from an array. 

In this case, I wanted to compute the DNA identity between the _i<sup>th</sup>_ and the _j<sup>th</sup>_ paequors. Because I was going to perform 30 x 30 = 900 operations, I removed the part of the ```compare()``` method that logs the two sequences to the console (this declutters the console output a little).

```javascript
// identity matrix
let idMatrix = [];
for (let i = 0 ; i < strongPaequor.length ; i++){
  // The comparisons of paequor i against paequor j
  let matrixLine = [];
  let firstPaequor = strongPaequor[i];
  for (let j = 0 ; j < strongPaequor.length ; j++){
    if (i < j) {
      let secondPaequor = strongPaequor[j];
      matrixLine.push(firstPaequor.compareDNA(secondPaequor));
    } else {
      // ignore self comparison and inverse comparison
      matrixLine.push(0);
    }
  }
  idMatrix.push(matrixLine);
}
```
This creates a 30 x 30 matrix, in which the number in line _i_, and column _j_ corresponds to the DNA identity between paequor _i_ and paequor _j_. To find the most similar paequors, we need to find the index of the maximum value of DNA identity. 

Because I didn't <s>look for</s> find a function that returns the maximum value in a JavaScript list of lists, I did this in two steps. First, I flattened ```idMatrix``` using the ```reduce()``` method:

```javascript
// Flatten the identity matrix
const idMatrixFlat = idMatrix.reduce((acc, val) => acc.concat(val), []);
```
<figcaption style="text-align: center"><code>reduce()</code> iterates through the arrays of <code>idMatrix</code> and concatenates them to the growing array <code>acc</code>, which starts as an empty array.</figcaption>

Once the matrix was flat, I applied the ```max()``` method of the ```Math``` object. However, ```max()``` cannot receive the values inside an array, but as separate arguments. So, I unpacked the values inside ```idMatrixFlat``` using the three-dot notation:

```javascript
const maxId = Math.max(...idMatrixFlat);
```
Then, I used the ```findIndex()``` method to...find the index of the maximum identity value:
```javascript
const maxIndex = idMatrixFlat.findIndex(id => id === maxId);
```
Now we know where our maximum value is. But remember this is an index in a flattened matrix! We need to find the row and the column of the maximum value in the original matrix to find out who our most similar paequors are. To find the row, we just need to know how many times we need to multiply the length of the ```strongPaequor``` array to reach ```maxIndex``` (this is a simple division and a round-down). To find the column, we need to know how many positions we need to add to the closest multiple of ```strongPaequor.length```, which we can do with the ```%``` operator: 
```javascript
// Convert index to our matrix coordinates
// First find the row
const row = Math.floor(maxIndex / strongPaequor.length);
// Now find the column
const col = maxIndex % strongPaequor.length;
```
Now we can directly compare our most similar paequors using ```row``` and ```column``` as indexes:
```javascript
console.log(`\nThe most similar pair of specimens:`);
strongPaequor[row].compareDNA(strongPaequor[col]);
```
Which will print something like:
```
The most similar pair of specimens:
G,G,A,C,A,C,C,A,A,G,T,G,G,T,G
T,G,G,C,A,C,G,A,A,G,G,G,G,G,T
Specimens 30 and 92 have 60.00% DNA in common.
```

## Conclusion

I had a lot of fun doing this exercise, probably because there was some biology in it. It was also interesting to solve the problem using a matrix, because I am very much used to manipulate them with Python, but I don't even know if there are libraries for matrix manipulation in JavaScript.

This was a somewhat technical post, so I'm sorry if it was a bit boring. I just wanted to go over a project that I really enjoyed, and record my thought process for each exercise.

Until next time!