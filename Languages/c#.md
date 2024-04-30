
## Basics

### Syntax

```csharp
// Single-line comments start with two forward slashes

/*
Multi-line comments start with forward slash and asterisk
and end with asterisk and forward slash
*/

// Declaring variables
int a = 5;
string b = "Hello";
bool c = true;

// Conditional statement
if (a > 5) {
    Console.WriteLine("Greater");
} else {
    Console.WriteLine("Less or equal");
}

// Looping structures
for (int i = 0; i < 10; i++) {
    Console.WriteLine(i);
}

while (a > 0) {
    Console.WriteLine(a);
    a--;
}

// Methods
void MyMethod() {
    Console.WriteLine("Called MyMethod");
}
```

### Data Types

- **int** - represents a 32-bit integer
- **long** - represents a 64-bit integer
- **float** - single precision floating point number
- **double** - double precision floating point number
- **bool** - Boolean
- **string** - sequence of characters

### Arrays

```csharp
// Declaring an array
int[] myArray = {1, 2, 3, 4, 5};

// Accessing array elements
Console.WriteLine(myArray[0]); // Outputs 1

// Iterating through an array
foreach (int i in myArray) {
    Console.WriteLine(i);
}
```

## Object-Oriented Programming

### Classes and Objects

```csharp
// Defining a class
public class Car {
    public string Make;
    public string Model;
    public int Year;

    // Constructor
    public Car(string make, string model, int year) {
        Make = make;
        Model = model;
        Year = year;
    }

    // Method
    public void DisplayInfo() {
        Console.WriteLine($"Make: {Make}, Model: {Model}, Year: {Year}");
    }
}

// Creating an object
Car myCar = new Car("Toyota", "Corolla", 2021);
myCar.DisplayInfo();
```

### Inheritance

```csharp
// Base class
public class Animal {
    public void Eat() {
        Console.WriteLine("Eating");
    }
}

// Derived class
public class Dog : Animal {
    public void Bark() {
        Console.WriteLine("Barking");
    }
}

Dog myDog = new Dog();
myDog.Eat(); // From Animal class
myDog.Bark();
```

## Advanced Features

### LINQ (Language Integrated Query)

```csharp
using System.Linq;

var numbers = new int[] { 1, 2, 3, 4, 5 };
var evenNumbers = from num in numbers
                  where num % 2 == 0
                  select num;

foreach (var num in evenNumbers) {
    Console.WriteLine(num);
}
```

### Exception Handling

```csharp
try {
    int[] myArray = new int[5];
    myArray[5] = 25; // This will throw an exception
} catch (IndexOutOfRangeException e) {
    Console.WriteLine("An exception occurred: " + e.Message);
} finally {
    Console.WriteLine("This block is executed regardless of the outcome.");
}
```

## Resources

- [Microsoft C# Documentation](https://docs.microsoft.com/en-us/dotnet/csharp/)
- [C# Corner](https://www.c-sharpcorner.com/)

