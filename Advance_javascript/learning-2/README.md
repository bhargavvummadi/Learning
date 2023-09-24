- Execution Context
- - Gloabal Execution context 
- - global object and this and hoisting (creation phase)
- - running your code (execution phase)
- Lexical environment (scope of the function or object local or global)
- Hoisting is the behavior of moving the variables or function declarations to the top of their resp environment during compilation phase.
- variables (when 'var' is used) are partially hoisted and functions are fully hoisted
``` code
    console.log(teddy);
    console.log(sing());
    var teddy = 'bear';
    function sing() {
        console.log('testing lalala');
    }

    output:
    undefined
    testing lalala

```
- functions can be declared or expressed like following
```
//function expression other one is declaration which is observed while creation phase
const fnc1 = ()=>{
    console.log()
}

```
- arguments keyword should be avoided because it's an object and can be converted to array and used again if we want to perform any operations. Instead we can use spread operator which gives a array of args like (...args)
- variable environment in execution context like block scope in other programming languages.
- Scope chain links variables and functions which are in global lexical environment. Just like accessing variables that are defined globally.
- In JS lexical scope (available data + variable where the functions are defined) determines our available variables. Not where the function is called (dynamic scope).
- Weird JS
- - lekage of global variable and use of **use strict** 
``` 
function weird() {
    h = 50;
    return h;
}
weird(); //without using use strict in the header it returns 50 because JS creates global h for you and creates confusion.
```
- function scope vs block scope let and const are block scoped
- global variables are bad and can cause crashes (IIFE Imediate Invocation of Function Expressions)
- IIFE creats local scopes and reduces the global access of variables and in return helps to speed boost the code in example of jquery passed to anonymous function argument which is invoked automatically.
- **this** keyword in JS is the object that the function is a property of
```
obj.somefunc(this) //here this is again the obj which has all the properties here it is somefunc

//1, gives methods access to their object
//2, execute same code for multiple objects

function impPerson() {
    console.log(this.name + "!");
}
const name = "suny";

const obj1 = {
    name: "Rob",
    impPerson:impPerson
}
const obj2 = {
    name: "Baki",
    impPerson:impPerson
}
obj1.impPerson();
obj2.impPerson();

this - hey Execution context who called me!!
this - also not lexically scoped which means not where function is written only where function is called from which we can say it is dynamically scoped.
We can make it lexical and work properly by using ()=>{} functions from ES6. before we used bind or raised var self = this assignment and called functions like this , obj.someFunc()().
```
- call() vs apply() vs bind()
- All functions use call() underneath the hood , for example
```
 function a(){}
 a() --> a.call() (real deal)

 const wizard = {
     name: "marlin",
     health: 100,
     heal(power) {
         return this.health += power;
     }
 }


 const archer = {
     name: "robin",
     health: 10
 }

 console.log('1',archer);
 wizard.heal.call(archer,50);
 wizard.heal.apply(archer,[50]); array of arguments

 call() and apply() are same excepts the way we pass arguments (useful for borrowing methods b/w objects)


 const healthArcher = wizard.heal.bind(arhcer,80);
 healthArcher();
bind is useful for calling functions which can be later on used based on certain context or this.

const array = [1,2,3];

function getMaxNumber(arr){
  return Math.max.apply(null,arr) //code here   as args is array we can use apply and this doesn't matter in this case.
}

getMaxNumber(array) // should return 3

bind and currying passing half of the func params

function multiply(a,b){
    return a*b;
}
let mbytwo = multiply.bind(this,2);
console.log(mbytwo(4)) //8

```
- Context vs Scope 
- Scope: Scope is described as a function-based concept. It pertains to what variables a function can access when it is invoked. It refers to the variable environment of a function.
- Context: Context, on the other hand, is more object-oriented. It is related to the value of the this keyword, which refers to the object that owns the currently executing code. Context is often determined by how a function is invoked.
- 

