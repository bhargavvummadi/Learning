### CLousers
### Prototypal Inheritance
### High Order Functions
### Functions vs Objects
### Scheme + Java

- Functions are Objects
- function written inside in a class or object as method
```
function a(){
    return 2;
}
a(); //a.call();

const obj = {
    //method
    sum: function(){
        return 3;
    }
}

const newFunc = new Function('varb','return varb');
newFunc(4); //op is 4

```

- functions can be passed around just like objects for data
- functions are First call citizens in JS because of all its usage like objs, variables and methods etc.
- they can be assign to varaibles and objects.
- Passed as arguments to other functions.
```
var stuff = function() {}

function a(fn)
{
    fn();
}

a(function(){console.log('hey ther!')})

function b()
{
    return function c() {
        console.log('bye!');
    }
}
const k = b();
k(); //'bye!' or we can also use two closed brackets like b()()
```
- Careful while using functions inside the loops. Always declare outside the loops

- High Order Functions: A function that can take a function as argument or return function as result 

```
function letAdamLogin() {
    let array = [];
    for (;et i=0;i<10000;i++)
    {
        array.push(i);
    }
    return 'Access Granted to Adam';
}

letAdamLogin() //takes sometime to process the result what happens when we have multiple users or employees

function letEvaLogin() {
    let array = [];
    for (;et i=0;i<10000;i++)
    {
        array.push(i);
    }
    return 'Access Granted to Eva';
}



Now let's create a generic function

function letUserLogin(user) {
    let array = [];
    for (;et i=0;i<10000;i++)
    {
        array.push(i);
    }
    return 'Access Granted to ' + user;
}

letUserLogin('Adam'); //more flexobility and kept dry code


HOF

function aUTHENICATE(verify) {
    let array = [];
    for (;et i=0;i<verify;i++)
    {
        array.push(i);
    }
    return true;
}

function letPerson(person,fn) {
    if (person.level === 'admin')
    {
        fn(500000);
    }
    else if(person.level === 'user')
    {
        fn(10000000);
    }
    return 'Access Granted to' + person.name;
}

letPerson({level:'admin', name:'Sally'}, aUTHENICATE);


Another HOF example

const multiplyBy = (n1) => (n2) => n1*n2;

multiplyBy(2)(4); //8

const multiplyByTwo = multiplyBy(2);
multiplyByTwo(4); //8

const multiplyByFour = multiplyBy(4);
multiplyByTwo(4); //16



```

## Two Pillers of JS Closuers and Prototypes

- Closuers: functions + lexical scope

```
function a(){
    let grandpa = 'grandpa';
    return function b() {
        let father = 'father';
        return function c() {
            let son = 'son';
            return ` ${grandpa} > ${father} > ${son} `;
        }
    }
}

a()()(); //returns grandpa > father > son
JS engine is here keeping the father and grandpa variables in a closuer box because they are being referenced inside the function c, if b() has any other varibale it is being garbage collected as it is not referenced.

```
```
function callMeMaybe() {
    setTimeout(()=> console.log(callMe),4000);
    const callMe = 'Hi there!';
}

because setTimeout() is webAPI function and it is a callback it is pushed back to event queue and waits until the stack is empty, by that time function is executed and a closure is created for callMeMaybe() function as callMe is referenced here.

```

- Closuers and memory efficiency

```
//Memory efficient

function heavyDuty(index) {
    const bA = new Array(7000).fill('happyface');
    console.log('created');
    return bA[index];
}

heavyDuty(453);
heavyDuty(433);
heavyDuty(783);

const closuerdHeavyDuty = heavyDutyWithClosuer();

closuerdHeavyDuty(785);
closuerdHeavyDuty(787);
closuerdHeavyDuty(789);

function heavyDutyWithClosuer() {
    const bA = new Array(7000).fill('happyface'); //this line is in closuer box
    console.log('created with closer'); //this line is in closuer box
    return function(index) { 
    return bA[index]; // this is repeated called and referenced
    }
}

ouptut:
created
created
created
created with closer
happyface

// Encapsulation 

const makeNuclearButton = () => {
    let timeWithoutDestruction = 0;
    const pastTime = () => timeWithoutDestruction++;
    const totalPeaceTime = () => timeWithoutDestruction;
    const launch = () => {
        timeWithoutDestruction = -1;
        return 'boom'
        };
    setInterval(passTime,1000) // call this function (passTime here) every  1 sec
    return {
        launch: launch,
        totalPeaceTime: totalPeaceTime
    }
}

const ohno = makeNuclearButton();
ohno.totalPeaceTime()
output in images:

Now, if I decide not to give access to launch function I simpy remove it in return

return {
        totalPeaceTime: totalPeaceTime
    }
Principle of least privileage - don't wanna give access to your api by everybody
This hides the usage of launch by anybody usage the makeNuclearButton also we only give setInterval to increment time not giving user power to increase the counter.
```

```
- Another exercise of closure

const ar =[1,2,3,4];

for(var i=0;i<ar.length;i++)
{
    setTimeout(function(){
        console.log('index at' + i);
    },3000);

}
output:
index at 4
index at 4
index at 4
index at 4

To fix this we just use let inplace of var becuase let in block scopic;
or we can use closure

for(var i=0;i<ar.length;i++)
{
    //using immidealtily invoked function
    (function(closueri){
    setTimeout(function(){
        console.log('index at' + closueri);
    },3000)
    })(i)

}

```

## Prototypal Inheritance (getting function and methods from a different object)

- Object{} 
-   | '  '    |
-  /  '       '  \
-  Array[]   Function()
```
array.__proto__ (we will get up the chain )
array.__proto__.__proto__ (we will get object as go to root of array[] which is object)
```

```
- Another example what is prototypal inheritance why we use it instead of bind() which is simply borrowing a method from a different object.

let dragon = {
    name:'tanya',
    fire:true,
    fight() {
        return 5;
    },
    sing() {
        if(this.fire) {
            return `I am ${this.name}, the breather of fire`;
        }
    }
}

let lizard = {
    name: 'kiki',
    fight() {
        return 1;
    }
}

const kikifire = dragon.sing.bind(lizard);
console.log(kikifire); //return undefined as lizard has no fire property which is checked in if inside the sing function.

Now if we try to use sing() for lizard using we will undefined output because .

Now we can extend or inherit all the properties and functions from a different object, here lizard want to inherit all the props and functions from dragon.

lizard.__proto__ = dragon;
dragon.isPrototypeOf(lizard); // returns true if lizard inherits from dragon
lizard.sing(); //I am kiki, the breather of fire
lizard.fire; //true
lizard.fight(); //1

for (let prop in lizard) {
    if (lizard.hasOwnProperty(prop)) {
        console.log(prop); // name, fight
    }
    console.log(prop); //name, fire, fight, sing
}

we shouldn't manually assign prototypl inheritance, it will literally slows down the js code.

why we shouldn't use __proto__ in JS
ChatGPT
The __proto__ property in JavaScript is considered deprecated and not recommended for several reasons:

Non-standard: The __proto__ property is not a part of the official ECMAScript specification (though it was historically supported by many JavaScript engines). Instead, it is a legacy feature that was never standardized.

Non-portable: Because it is not standardized, using __proto__ can result in code that is not portable across different JavaScript environments and engines. It may work in one browser or environment but not in others.

Object.setPrototypeOf and Object.getPrototypeOf: Modern JavaScript provides alternative methods for working with object prototypes in a standardized way. You can use Object.setPrototypeOf() to set the prototype of an object and Object.getPrototypeOf() to retrieve the prototype. These methods are more consistent and reliable than __proto__.

Performance: Accessing the __proto__ property can be slower than using the standardized methods like Object.setPrototypeOf() and Object.getPrototypeOf(). Modern JavaScript engines are optimized for the latter, making them more efficient.

Readability and Maintainability: Using __proto__ can make code less readable and harder to maintain because it relies on a non-standard and less common syntax. Code that follows standardized practices is typically easier for other developers to understand.

Potential Security Risks: In some cases, using __proto__ can introduce security vulnerabilities, such as prototype pollution attacks. It's safer to stick to standardized methods for working with object prototypes.

Another prototype and __proto__ which lives within the prototype obj liok image

//Every Prototype chain links to a prototype object{}
function multiplyBy5(num) {
  return num*5
}

multiplyBy5.__proto__
Function.prototype
multiplyBy5.__proto__.__proto__
Object.prototype
multiplyBy5.__proto__.__proto__.__proto__
typeof Object
typeof {}
```

- We should use Object.create(obj) to inherit from obj

```
  // Create our own prototypes:
let human = {mortal: true}
let socrates = Object.create(human);
socrates.age = 70;
human.isPrototypeOf(socrates); // true

Only functions have the prototype property and Object is a function and the Object.property is the final object in the chain.
```
```
Exercise of Prototypal Inheritance

//Array.map() => to print '🗺'
Array.prototype.map = function()  { // what happens with arrow function here?
  arr = [];
  for (let i = 0; i < this.length; i++) {
    arr.push((this[i]+'🗺'));
  }
  return arr;
}
console.log([1,2,3].map())

//Date object => to have method .yesterday() which shows you yesterday's day in 'YYYY-MM-DD' format.
Date.prototype.lastYear = function(){
  return this.getFullYear() - 1;
}

new Date('1900-10-10').lastYear()
// don't worry if you didn't get this... we will expand on this later.

How would you be able to create your own .bind() method using call or apply.

Hint:
Function.prototype.bind = function(whoIsCallingMe){
  const self = this;
  return function(){
    return self.apply(whoIsCallingMe, arguments);
  };
}
```


  





