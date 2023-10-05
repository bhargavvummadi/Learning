# OOP vs FP 
## Object Oriented Programming vs Functional Programming

- Scheme (functions ) prior and inspiration for JS
- Java (Object) inspiration for Js

- In JS we have multi paradigmed language , both FP and OOP  

```
// factory function make/create
function createElf(name, weapon) {
  //we can also have closures here to hide properties from being changed.
  return {
    name: name,
    weapon: weapon,
    atack() {
      return 'atack with ' + weapon
    }
  }
}
const sam = createElf('Sam', 'bow');
const peter = createElf('Peter', 'bow');

sam.atack()

In this example we are using functional programming except that every object has a atack() function in every object space
```
- Object.create() using prototypal inheritance creating link between objects and functionality

```
const elfFunctions = {
  attack: function() {
    return 'atack with ' + this.weapon
  }
}
function createElf(name, weapon) {
  //Object.create creates __proto__ link
  newElf = Object.create(elfFunctions)
  newElf.name = name;
  newElf.weapon = weapon
  return newElf
}


const sam = createElf('Sam', 'bow');
const peter = createElf('Peter', 'bow');
sam.attack()

```
  - Constructors

```
//Constructor Functions
function Elf(name, weapon) {
  this.name = name;
  this.weapon = weapon;
}

Elf.prototype.attack = function() { 
  return 'atack with ' + this.weapon
}
const sam = new Elf('Sam', 'bow');
const peter = new Elf('Peter', 'bow');
sam.attack()

```
- ES6 Classes blueprint of the object (these can be defined as psuedo classes as in the background or under the hood these are still prototypical inheritance)

```
class Elf {
  constructor(name, weapon) {
    this.name = name;
    this.weapon = weapon;
  }
  attack() {
    return 'atack with ' + this.weapon
  }
}

const fiona = new Elf('Fiona', 'ninja stars');
console.log(fiona instanceof Elf) // 
const ben = new Elf('Ben', 'bow');
fiona.attack()
```


- this in 4 ways

```
// new binding
function Person(name, age) {
  this.name = name;
  this.age =age;
  console.log(this);
}

const person1 = new Person('Xavier', 55)

//implicit binding
const person = {
  name: 'Karen',
  age: 40,
  hi() {
    console.log('hi' + this.name)
  }
}

person.hi()

//explicit binding
const person3 = {
  name: 'Karen',
  age: 40,
  hi: function() {
    console.log('hi' + this.setTimeout)
  }.bind(window)
}

person3.hi()

// arrow functions
const person4 = {
  name: 'Karen',
  age: 40,
  hi: function() {
    var inner = () => {
      console.log('hi ' + this.name)
    }
    return inner()
  }
}

person4.hi()

```

- Inheritance (Elf has prototypal chain with character)

```
class Character {
  constructor(name, weapon) {
    this.name = name;
    this.weapon = weapon;
  }
  attack() {
    return 'atack with ' + this.weapon
  }
}

class Elf extends Character { 
  constructor(name, weapon, type) {
    // console.log('what am i?', this); this gives an error
    super(name, weapon) 
    console.log('what am i?', this);
    this.type = type;
  }
}

class Ogre extends Character {
  constructor(name, weapon, color) {
    super(name, weapon);
    this.color = color;
  }
  makeFort() { // this is like extending our prototype.
    return 'strongest fort in the world made'
  }
}

const houseElf = new Elf('Dolby', 'cloth', 'house')
//houseElf.makeFort() // error
const shrek = new Ogre('Shrek', 'club', 'green')
shrek.makeFort()
```

- As of now we have private class field and private methods in JS
  
```
  ES2022: Private Class Fields + Methods
Good news! As of ES2022, we now have a feature that we are going to talk about in the next video: Private Class Field + Methods. Once you watch the next video, see if you can now officially use it in JavaScript by trying it on the latest version of the Chrome browser (inside the console tab). It should work!



class Employee {
    #name = "Test"; // private field
    setName(name) {
        this.#name = name;
    }
}
const emp = new Employee();
emp.#name = 'New'; // error
emp.setName('New'); // ok


class Employee {
    #name = "Test";
    constructor(name) {
        this.#setName(name) // ok
    }
    #setName(name) { // Private method
        this.#name = name;
    }
}
const emp = new Employee('New'); // ok
emp.#setName('New'); // error

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Private_class_fields
```
- 4 Pillars of JS
- Polymorphism (many forms, the ability to call same method on different objects and each object is responding different way )
- inheritance
- abstraction
- Encapsulation

```
class Character {
  constructor(name, weapon) {
    this.name = name;
    this.weapon = weapon;
  }
  attack() {
    return 'atack with ' + this.weapon
  }
}

class Elf extends Character { 
  constructor(name, weapon, type) {
    // console.log('what am i?', this); this gives an error
    super(name, weapon) 
    console.log('what am i?', this);
    this.type = type;
  }
  attack(cry) {
      return 'attack with' + cry;
  }
}

class Ogre extends Character {
  constructor(name, weapon, color) {
    super(name, weapon);
    this.color = color;
  }
  attack() {
      return 'arhhhh;
  }
  makeFort() { // this is like extending our prototype.
    return 'strongest fort in the world made'
  }
}

const houseElf = new Elf('Dolby', 'cloth', 'house')
houseElf.attack('weee');
//houseElf.makeFort() // error
const shrek = new Ogre('Shrek', 'club', 'green')
shrek.attack()

Basic Polymorphism example
```
  