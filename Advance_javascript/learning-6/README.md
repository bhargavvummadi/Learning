## Functional Programming

- It is all about seperation of concerns
- seperation of data and (behavior of function) functions
- objects of fp are  immutable (can't be changed)
- Pillar of FP is pure function

```
Amazon Exercise
// Amazon shopping
const user = {
  name: 'Kim',
  active: true,
  cart: [],
  purchases: []
}


//Implement a cart feature:
// 1. Add items to cart.
// 2. Add 3% tax to item in cart
// 3. Buy item: cart --> purchases
// 4. Empty cart

//Bonus:
// accept refunds.
// Track user history.
```

```
my solution for above code:

// Amazon shopping
const user = {
  name: 'Kim',
  active: true,
  cart: [],
  purchases: []
}
const item = {
  0 : {
  name: 'brush',
  color: 'black',
  price : 30, },
  1 : {
  name: 'paste',
  color: 'blue',
  price : 20, },
}

function addItemsToCart(user,items) {
  let itemsList = Object.values(items);
  for(let item in itemsList) {
    let temp_item = itemsList[item];
    temp_item.price = (temp_item.price + (temp_item.price*0.03))
    user.cart.push(temp_item)
  }
  console.log(user);
}

function buyItem(user,item) {
  for(let i in user.cart) {
    if (user.cart[i]==item) {
      user.purchases.push(item);
      user.cart = user.cart.filter((it) => {
        return it!== item
      })
    }
  }
  console.log(user)
}

function emptyCart(user) {
  user.cart.splice(0,user.cart.length);
  console.log(user);
}

addItemsToCart(user,item);
buyItem(user,item[1]);
emptyCart(user);

//Implement a cart feature:
// 1. Add items to cart.
// 2. Add 3% tax to item in cart
// 3. Buy item: cart --> purchases
// 4. Empty cart

//Bonus:
// accept refunds.
// Track user history.
```

- Pure function definition : A function has to return the same output given the same input and has no side effects (can't modify anything outside the scope)

- Example of function which has side effects , because it modifies the global object (which is outside of the scope) and order of execution matters.

```
//Side effects:
const array = [1,2,3];
function mutateArray(arr) {
  arr.pop()
}
function mutateArray2(arr) {
  arr.forEach(item => arr.push(1
  ))
}
//The order of the function calls will matter.
mutateArray(array) // [1,2]
mutateArray2(array) // [1,2,1,1]
array
```

- Referntial transparency (no matter how many times we run given the same input a function should return the same output).

- In computer science, idempotence refers to the property of an operation where applying it multiple times has the same effect as applying it once. In the context of JavaScript, this concept is often discussed in the context of HTTP methods, specifically with regard to API design.

- For example, if you have an HTTP endpoint that updates a resource, making multiple identical requests should have the same result as making a single request. This is important for preventing unintended side effects when requests are duplicated, such as due to network issues.

- Here's a short example using JavaScript and a hypothetical API endpoint:

```
// Function to make an HTTP request to update a resource
function updateResource(data) {
    // Assuming 'axios' for making HTTP requests
    return axios.put('/api/resource', data);
}

// Example usage
const dataToUpdate = { name: 'New Name' };

// Making an update request (idempotent operation)
updateResource(dataToUpdate)
    .then(response => {
        console.log('First update:', response.data);
    })
    .catch(error => {
        console.error('Error during the first update:', error);
    });

// Making the same update request again (should have the same effect)
updateResource(dataToUpdate)
    .then(response => {
        console.log('Second update:', response.data);
    })
    .catch(error => {
        console.error('Error during the second update:', error);
    });


```

- In this example, calling updateResource twice with the same dataToUpdate should ideally produce the same result as calling it once. This ensures that if the request is duplicated, it doesn't cause unintended changes or errors due to the operation being applied multiple times.


- Side Note of http methods
  
```
Certainly! Here are the most common HTTP methods with neat bullet points and examples:

GET:

Purpose: Retrieve data from the server.
Example:
http
Copy code
GET /api/users
POST:

Purpose: Submit data to be processed to a specified resource.
Example:
http
Copy code
POST /api/users
Content-Type: application/json

{ "name": "John Doe", "email": "john@example.com" }
PUT:

Purpose: Update a resource or create it if it doesn't exist.
Example:
http
Copy code
PUT /api/users/1
Content-Type: application/json

{ "name": "Updated Name", "email": "updated@example.com" }
PATCH:

Purpose: Partially update a resource.
Example:
http
Copy code
PATCH /api/users/1
Content-Type: application/json

{ "email": "new_email@example.com" }
DELETE:

Purpose: Delete a specified resource.
Example:
http
Copy code
DELETE /api/users/1
OPTIONS:

Purpose: Describes the communication options for the target resource.
Example:
http
Copy code
OPTIONS /api/users
HEAD:

Purpose: Same as GET, but only retrieves headers (no response body).
Example:
http
Copy code
HEAD /api/users
TRACE:

Purpose: Echoes back the received request for diagnostic purposes.
Example:
http
Copy code
TRACE /api/echo
These methods are fundamental in RESTful API design and are used to perform various operations on resources.




User
difference between patch put and post
ChatGPT
The main differences between PATCH, PUT, and POST HTTP methods lie in their intended use cases and the nature of the operations they perform:

POST (Create):

Purpose: Used to submit data to be processed to a specified resource. It often results in the creation of a new resource.
Example:
http
Copy code
POST /api/users
Content-Type: application/json

{ "name": "John Doe", "email": "john@example.com" }
PUT (Update/Create):

Purpose: Typically used to update a resource or create it if it doesn't exist. It replaces the entire resource with the new data provided.
Example:
http
Copy code
PUT /api/users/1
Content-Type: application/json

{ "name": "Updated Name", "email": "updated@example.com" }
PATCH (Partial Update):

Purpose: Used to apply partial modifications to a resource. It only updates the fields provided in the request, leaving the other fields unchanged.
Example:
http
Copy code
PATCH /api/users/1
Content-Type: application/json

{ "email": "new_email@example.com" }
In summary:

POST is for creating a new resource.
PUT is for updating or creating a resource, and it replaces the entire resource.
PATCH is for partially updating a resource, allowing you to update specific fields without affecting the others.



User
main diff between post and get
ChatGPT
The main differences between the POST and GET HTTP methods are in their purpose and how they handle data:

GET:

Purpose: Used to request data from a specified resource.
Data Handling: Sends data in the URL (query parameters).
Idempotent: Generally considered idempotent, meaning multiple identical requests should have the same effect as a single request.
Security: Parameters are visible in the URL, which may not be suitable for sensitive information.
Example:
http
Copy code
GET /api/users?id=1
POST:

Purpose: Used to submit data to be processed to a specified resource.
Data Handling: Sends data in the request body. Suitable for larger amounts of data.
Idempotent: Not considered idempotent. Multiple identical requests may have different effects, especially if they result in the creation of a new resource.
Security: Parameters are not visible in the URL, enhancing security for sensitive information.
Example:
http
Copy code
POST /api/users
Content-Type: application/json

{ "name": "John Doe", "email": "john@example.com" }
In summary:

GET is used for retrieving data, and parameters are included in the URL.
POST is used for submitting data, and the data is sent in the request body.
```


- Imperative (step by step saying of any process) and Declarative (concrete steps ex. just bring water by friend)
- Another item is for loop and forEach in JS
- Jquery is more imperative
- ReactJS is more declarative
- FP is more declarative, tell what to do more than how to do it
- declarative compiles down to imperative
- Immutability - not chaging the state but instead making copy of state and returning that in case of FP like pure function.
- 

```
const obj = {name: 'Andrei'}
function clone(obj) {
  return {...obj}; // this is pure
}

function updateName(obj) {
  const obj2 = clone
  (obj);
  obj2.name = 'Nana'
  return obj2
}

const updatedObj = updateName(obj)
console.log(obj, updatedObj)


```
- Seems like lot of memory waste but not because of structural sharing (https://medium.com/@dtinth/immutable-js-persistent-data-structures-and-structural-sharing-6d163fbd73d2)


- Higher Order Functions (accepts fn as parameter or returns fn as result) and Clousers (remembers the state has to use careful we have make it as private variables look below example)
```
//HOF
const hof = (fn) => fn(5);
hof(function a(x){ return x})
//Closure
const closure = function() {
  let count = 55;
  return function getCounter() {
    return count;
  }
}

const getCounter = closure()
getCounter()
getCounter()
getCounter()
```


- currying in JS (using a function with only a single parameter help of closures as it remebers the outer function variables)
```
//Currying
const multiply = (a, b) => a * b
const curriedMultiply = (a) => (b) => a * b
curriedMultiply(5)(20)
const multiplyBy5 = curriedMultiply(5)

//After 10 years still multiplyBy5 has the value remebered
multiplyBy5(20)
```
- Partial application (on second call i expect all parameters while currying expect one parameter at a time)

```
//Partial Application
const multiply = (a, b, c) => a * b * c
const partialMultiplyBy5 = multiply.bind(null, 5)
partialMultiplyBy5(10, 20)
```
-  I have decided to include them on here because it will help you understand an interesting topic (Memoization) when it comes to functional programming in Javascript. Enjoy!

- Memoization is caching
  
```
//learn to cache
function addTo80(n) {
  return n + 80;
}

addTo80(5)

let cache = {};
function memoizeAddTo80(n) {
  if (n in cache) {
    return cache[n];
  } else {
    console.log('long time');
    const answer = n + 80;
    cache[n] = answer;
    return answer;
  }
}

// console.log(1, memoizeAddTo80(6))
// // console.log(cache)
// // console.log('-----------')
// console.log(2, memoizeAddTo80(6))

// let's make that better with no global scope. This is closure in javascript so.
function memoizeAddTo80(n) { 
  let cache = {};
  return function(n) {
    if (n in cache) {
      return cache[n];
    } else {
      console.log('long time');
      const answer = n + 80;
      cache[n] = answer;
      return answer;
    }
  }
}

const memoized = memoizeAddTo80();
console.log(1, memoized(6))
// console.log(cache)
// console.log('-----------')
console.log(2, memoized(6))


```

- closures plus pure functions & memoization caching --> companies love it!!!!

- Compose and pipe
- Certainly! In JavaScript, compose and pipe are higher-order functions used for function composition. Here's a neat example of both:

compose Example:
```
// Function to add 5
const add5 = x => x + 5;

// Function to multiply by 2
const multiplyBy2 = x => x * 2;

// Function to square a number
const square = x => x * x;

// Using compose to create a new function that squares, multiplies by 2, and adds 5
const composedFunction = compose(
  add5,
  multiplyBy2,
  square
);

// Applying the composed function to a value
const result = composedFunction(3); // (((3^2) * 2) + 5) = 23
console.log(result);

```

- pipe example

```
// Function to add 5
const add5 = x => x + 5;

// Function to multiply by 2
const multiplyBy2 = x => x * 2;

// Function to square a number
const square = x => x * x;

// Using pipe to create a new function that adds 5, multiplies by 2, and squares
const pipedFunction = pipe(
  add5,
  multiplyBy2,
  square
);

// Applying the piped function to a value
const result = pipedFunction(3); // ((3 + 5) * 2)^2 = 64
console.log(result);

```

- In both examples:

- compose and pipe are utility functions for function composition.
They take a series of functions as arguments and return a new function.
- The order of function application differs: compose applies functions from right to left, while pipe applies them from left to right.
- These functions are useful for creating concise and readable code when you need to apply a series of transformations or operations to a value.

```
Example from course

fn1(fn2(fn3(50)));

compose(fn1, fn2, fn3)(50) //Right to lext
pipe(fn3, fn2, fn1)(50)//left to right

const compose = (f, g) => (a) => f(g(a))
const pipe = (f, g) => (a) => g(f(a))
const multiplyBy3AndAbsolute = compose((num) => num*3, Math.abs)
console.log(multiplyBy3AndAbsolute(-50))

```

- Arity (the numbers of arguments a function takes)

```
Amazon solution from course:

const user = {
  name: 'Kim',
  active: true,
  cart: [],
  purchases: []
}
const history1 = [];
const compose = (f, g) => (...args) => f(g(...args))
const pipe = (f, g) => (...args) => g(f(...args))
const purchaseItem  = (...fns) => fns.reduce(compose);
const purchaseItem2  = (...fns) => fns.reduce(pipe);
purchaseItem2(
  addItemToCart,
  applyTaxToItems,
  buyItem,
  emptyUserCart,
)(user, {name: 'laptop', price: 60})
// purchaseItem(
//   emptyUserCart,
//   buyItem,
//   applyTaxToItems,
//   addItemToCart
// )(user, {name: 'laptop', price: 50})
function addItemToCart(user, item) {
  history1.push(user)
  const updatedCart = user.cart.concat(item)
  return Object.assign({}, user, {cart: updatedCart});
}

function applyTaxToItems(user) {
  history1.push(user)
  const {cart} = user;
  const taxRate = 1.3;
  const updatedCart = cart.map(item => {
    return {
      name: item.name,
      price: item.price*taxRate
    }
  })
  return Object.assign({}, user, { cart: updatedCart });
}

function buyItem(user) {
  history1.push(user)
  const itemsInCart = user.cart;
  return Object.assign({}, user, { purchases: itemsInCart });
}
function emptyUserCart(user) {
  history1.push(user)
  return Object.assign({}, user, { cart: [] });
}

function refundItem() {

}

function getUserState() {

}

function goBack() {

}

function goForward() {

}
```

- Absolutely! Let's break down the code and explain it step by step:

- Code Overview:
- User Object:

- Represents a user with properties such as name, active status, shopping cart, and purchase history.
javascript
Copy code
const user = {
  name: 'Kim',
  active: true,
  cart: [],
  purchases: []
};
History Array:

- An array (history1) used to keep track of user state at various points in the process.
javascript
Copy code
const history1 = [];
Function Composition Helpers:

- compose and pipe functions are utility functions for function composition.
javascript
Copy code
const compose = (f, g) => (...args) => f(g(...args));
const pipe = (f, g) => (...args) => g(f(...args));
Purchase Item Function:

- purchaseItem and purchaseItem2 are functions that use function composition to execute a series of actions on the user object.
javascript
Copy code
const purchaseItem  = (...fns) => fns.reduce(compose);
const purchaseItem2  = (...fns) => fns.reduce(pipe);
Action Functions:

- Functions like addItemToCart, applyTaxToItems, buyItem, and emptyUserCart perform specific actions on the user object.
javascript
Copy code
function addItemToCart(user, item) { /* ... */ }
function applyTaxToItems(user) { /* ... */ }
function buyItem(user) { /* ... */ }
function emptyUserCart(user) { /* ... */ }
Executing Actions:

- Using purchaseItem2 to compose actions and execute them on the user object.
javascript
Copy code
purchaseItem2(
  addItemToCart,
  applyTaxToItems,
  buyItem,
  emptyUserCart
)(user, { name: 'laptop', price: 60 });
Explanation of Actions:

- Each action (e.g., add item to cart, apply tax, buy item, empty cart) is performed sequentially on the user object, modifying it at each step.
The history1 array keeps track of the user state after each action.
Execution Flow:
Add Item to Cart:

- addItemToCart adds an item to the user's cart.
Apply Tax to Items:

applyTaxToItems applies tax to items in the user's cart.
Buy Item:

- buyItem moves items from the cart to the purchase history.
Empty User Cart:

- emptyUserCart clears the user's shopping cart.
Additional Notes:
The history1 array is used to log the user's state after each action for tracking purposes.
- The purchaseItem2 function uses pipe, which applies functions from left to right, making the code read more sequentially.
Remember, this code is demonstrating function composition and doesn't cover actual UI interactions or state management in a real application. Feel free to ask if you have any specific questions!