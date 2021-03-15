# Typescript basics

### Functions
Function declaration:

```javascript
const foo = (input) => {
}
# For using types for the input we have to write
const foo2 = (a: string, b: int) => {
}
# For using types for input and output to secure functions do
const foo3 = (a: string, b:int): string => {
}
```

### Interfaces
These are like some type of structures for objects where we can give the blueprint for it. This blueprint then includes the attributes of said object(essentially we say object but it is our own datatypes) and the types of these attributes.

```typescript
# Interface is a protected word
# Pay attention to the code style we have big letter at start
interface User {
	name: string;
	age: number;
}
# use case
const user: User = {
	name: "Ramtin",
	age: 25,
}
# We can also have functions in our interfaces
interface User {
	name: string;
	age: number;
	getAge(): string # this is the return type
					 # this will then be used like following
}

# use case 2
const user: User = {
	name: "Ramtin",
	age: 25,
	getAge() {
	 return "25"; # note we have to return as string
	}
}
```
When using interfaces it is also common to put a big I before interface name to differentiate between interface and class. Or more commonly `UserInterface`

### Union
If we have a variable that can be either a number or a string or any combination of two types we can write is as such:
```Typescript
let pageName: string | number = 1;
```
The pipe in the middle there is the Union operator. And the equals 1 is the default value of the variable if nothing changes it.

The most common use case for the union operator is to check for null. Because when we are working with some data and we want to fetch it or we are waiting for a response etc then we dont want our program to crash so in those cases we write the following
```Typescript
let errorMessage: string | null = null; 
```
Unions can also be combined with Interface
```Typescript
interface UserInterface {
	name: string;
	surname: string;
}
let user: UserInterface | null = null;
```
Just make sure to not abuse unions with something like
```Typescript
let x = string | number | null | undefined | string[]
```

### Aliases
Aliases are there for giving names to types so that the code become more readable for example
```Typescript
type ID = string;
type Berry = BerryInterface;
type MaybeBerry = BerryInterface | null 
                  # Just to show that we can combine aliases too

interface UserInterface {
	id: ID; # programatically no change but easier to read
	name: string;
	surname: string;
}

let berries: Berry[] = ["Blueberry","Lingon berry"];
```
Notice capital letter at start for Aliases. 

### Classes in Typescript

```Typescript
Class User {
	firstName: string;
	age: number;
	
	constructor(firstName: string, age: number) {
	this.firstName = firstName;
	this.age = age;
	}
	
	getUser(): string {
	return this.firstName + " " + this.age as string;
	}
}

const user = new User("Ramtin", 25)
```

### Generics && Enums 
[[TODO]]

---
Status: #🌱 
tags:[[Javascript MOC]]-[[030 Software Development]]
date:2021-03-15


```Typescript
var s = "JavaScript syntax highlighting";
alert(s);
```