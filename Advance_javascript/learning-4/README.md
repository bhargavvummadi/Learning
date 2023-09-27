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