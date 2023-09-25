- JAVASCRIPT TYPES
```
typeof 5    //number
typeof true //boolean
typeof 'To ne or not' //string
typeof undefined //undefined absence of definition
typeof null  //object absecnce of value
typeof Symbol('just me') //symbol (do something interesting with object properties)

these have object wrapper like Number, Boolean
type of Infinity //number

//non-premitive
typeof {} //object
typeof [] //object
typeof function(){} //function (but it is a object in real)


let arr = [1,2,3] its just like
let arr2 = {
    0: 1,
    1: 2,
    2: 3,
}

we have
Array.isArray(arr) //true
Array.isArray(arr2) //false


```

- Pass By reference vs Pass ny value
```
 var a = 5  // a has access to value 5
 var b = 10  // b has 10
 by default primitive values are pass by value

 That means objects are passed by reference (objects are stored in memory and passed in reference)

 let obj1 = {name:'bhargav',password:123}
 let obj2 = obj1 //shallow copy and pass by reference
 if we change obj2.password = 456 it changes in both objects

 
```
-for arrays [].concate(different array) //deep copy
- for objects Object.assing({},different object) //shallow copy of object
- for same objects we can use spread operator = {...obj} //only first level of object
- which means when we have object inside an object we cannot copy the internal object values
- We can use JSON.parse(JSON.stringfy(obj)) to deep copy of an object or we can also  use structuredClone() function https://web.dev/structured-clone/

- Type Coercion (just like implict type conversion like type casting) https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness and https://dorey.github.io/JavaScript-Equality-Table/
- 1 == '1' //true 
- 1 === '1' //false
- false == "": true - The empty string "" is falsy, and false is also falsy, so they are equal after type coercion.

- false == []: true - An empty array [] is also falsy, so it is considered equal to false after type coercion.

- false == {}: false - An empty object {} is not falsy, so this comparison results in false.

- "" == 0: true - The empty string "" is falsy, and 0 is also falsy, so they are equal after type coercion.

- "" == []: true - An empty array [] is also falsy, so it is considered equal to the empty string "" after type coercion.

- "" == {}: false - An empty object {} is not falsy, so this comparison results in false.

- 0 == []: true - An empty array [] is also falsy, so it is considered equal to 0 after type coercion.

- 0 == {}: false - An empty object {} is not falsy, so this comparison results in false.

- 0 == null: false - null is falsy, but 0 is not equal to null after type coercion.