
## Basic Syntax and Data Types

```javascript
// Comments
// Single line comment
/* Multi-line
   comment */

// Variables
let x = 5;       // Integer (mutable)
const PI = 3.14; // Constant (immutable)
let name = "Alice";  // String
let isValid = true;  // Boolean

// Basic Operations
let sum = x + PI;
let difference = x - PI;
let product = x * PI;
let quotient = x / PI;
let remainder = x % PI;
let power = x ** 2;

// Template Literals
let greeting = `Hello, ${name}!`;

// Arrays
let numbers = [1, 2, 3, 4, 5];
numbers.push(6);  // Add to end
let first = numbers[0];  // Access element
let last = numbers[numbers.length - 1];  // Last element
let sliced = numbers.slice(2, 4);  // Slice array

// Objects
let person = { name: "Alice", age: 25 };
person.name;  // Access value
person.age = 26;  // Change value
person.gender = "Female";  // Add key-value pair
```

## Control Structures

```javascript
// If-Else
if (x > PI) {
    console.log("x is greater");
} else if (x < PI) {
    console.log("PI is greater");
} else {
    console.log("x and PI are equal");
}

// Loops
for (let i = 0; i < 5; i++) {
    console.log(i);
}

numbers.forEach(function(num) {
    console.log(num);
});

let i = 0;
while (i < 5) {
    console.log(i);
    i++;
}
```

## Functions

```javascript
function greet(name) {
    return `Hello, ${name}!`;
}

console.log(greet("Alice"));

// Arrow Functions
const square = x => x * x;
console.log(square(4));
```

## Array Methods

```javascript
// Map
const squares = numbers.map(x => x * x);

// Filter
const evens = numbers.filter(x => x % 2 === 0);

// Reduce
const sum = numbers.reduce((acc, x) => acc + x, 0);
```

## Error Handling

```javascript
try {
    const result = x / 0;
} catch (error) {
    console.log("An error occurred:", error.message);
} finally {
    console.log("This always executes");
}
```

## Modules and Imports

```javascript
// Exporting a module
export const add = (a, b) => a + b;

// Importing a module
import { add } from './math.js';
```

## Classes and Objects

```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    greet() {
        return `Hello, my name is ${this.name}`;
    }
}

const alice = new Person("Alice", 25);
console.log(alice.greet());
```

## Destructuring and Spread

```javascript
// Object Destructuring
const { name, age } = person;

// Array Destructuring
const [firstNum, secondNum, ...rest] = numbers;

// Spread Operator
const newArray = [...numbers, 7, 8, 9];
```

## Promises and Async/Await

```javascript
// Promises
const getData = new Promise((resolve, reject) => {
    // Asynchronous operation
});

// Async/Await
async function fetchData() {
    try {
        const data = await getData;
    } catch (error) {
        console.error("Error fetching data:", error);
    }
}
```

