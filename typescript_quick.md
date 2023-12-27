
# TypeScript Cheat Sheet

## Installation and Setup

```bash
# Install TypeScript globally
npm install -g typescript

# Initialize a new TypeScript project
tsc --init
```

## Basic Types

```typescript
let isDone: boolean = false;
let age: number = 42;
let name: string = "Alice";

let list: number[] = [1, 2, 3];
let listGeneric: Array<number> = [1, 2, 3];

let tuple: [string, number] = ["hello", 10];

enum Color {Red, Green, Blue}
let c: Color = Color.Green;

let notSure: any = 4;
let notSureArray: any[] = [1, true, "free"];

let voidValue: void = undefined;

function warnUser(): void {
    console.log("This is a warning message");
}

let nullValue: null = null;
let undefinedValue: undefined = undefined;

let obj: object = {};
```

## Interfaces

```typescript
interface LabelledValue {
  label: string;
}

function printLabel(labelledObj: LabelledValue) {
  console.log(labelledObj.label);
}

let myObj = { size: 10, label: "Size 10 Object" };
printLabel(myObj);
```

## Classes

```typescript
class Greeter {
  greeting: string;
  
  constructor(message: string) {
    this.greeting = message;
  }

  greet() {
    return "Hello, " + this.greeting;
  }
}

let greeter = new Greeter("world");
```

## Functions

```typescript
function add(x: number, y: number): number {
  return x + y;
}

let myAdd = function(x: number, y: number): number { return x + y; };

let myAddTyped: (baseValue:number, increment:number) => number = 
  function(x, y) { return x + y; };
```

## Generics

```typescript
function identity<T>(arg: T): T {
  return arg;
}

let output = identity<string>("myString");

class GenericNumber<T> {
  zeroValue: T;
  add: (x: T, y: T) => T;
}
```

## Enum

```typescript
enum Color {Red = 1, Green, Blue}
let colorName: string = Color[2];

console.log(colorName);  // Displays 'Green'
```

## Type Assertions

```typescript
let someValue: any = "this is a string";
let strLength: number = (someValue as string).length;
```

## Advanced Types

### Union Types

```typescript
function padLeft(value: string, padding: string | number) {
  // ...
}
```

### Type Guards

```typescript
function isFish(pet: Fish | Bird): pet is Fish {
  return (pet as Fish).swim !== undefined;
}
```

### Type Aliases

```typescript
type NameOrNameArray = string | string[];

function createName(name: NameOrNameArray) {
  // ...
}
```

### Intersection Types

```typescript
interface ErrorHandling {
  success: boolean;
  error?: { message: string };
}

type ServerResponse = Response & ErrorHandling;
```

## Modules

```typescript
// Exporting
export interface SomeType { /* ... */ }
export class SomeClass { /* ... */ }

// Importing
import { SomeType, SomeClass } from "./someModule";
```

## Decorators

```typescript
function sealed(constructor: Function) {
  Object.seal(constructor);
  Object.seal(constructor.prototype);
}

@sealed
class BugReport {
  type = "report";
  title: string;

  constructor(t: string) {
    this.title = t;
  }
}
```

## tsconfig.json

- The `tsconfig.json` file specifies the root files and the compiler options required to compile the project.

