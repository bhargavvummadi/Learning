- course map https://coggle.it/diagram/XE3ZoVj-rtA5hcxj/t/advanced-javascript
- Example code
  
```
setTimeout(()=>{console.log('1', 'is the loneliest number')}, 0)
setTimeout(()=>{console.log('2', 'can be as bad as one')}, 10)

//2
Promise.resolve('hi').then((data)=> console.log('2', data))

//3
console.log('3','is a crowd')

Output:
setTimeout(()=>{console.log('1', 'is the loneliest number')}, 0)
setTimeout(()=>{console.log('2', 'can be as bad as one')}, 10)

//2
Promise.resolve('hi').then((data)=> console.log('2', data))

//3
console.log('3','is a crowd')

```
- Promises
- A promise is an object that may produce a single value some time in future
- Either a resolved value, or a reson that it's not resolved (rejected) .
- Three possible states: 
-  fulfilled, rejected or pending
-  Before promises we have callbacks()

```
 const promise = new Promise((resolve, reject) => {
     if (true) {
         resolve('stuff worked')
     }
     else {
         reject('error, broker')
     }
 })

 promise.then(res=> {
     throw Error
     return res+'!'
     })
     .then(res2 => {
         console.log(res2);
     })
     .catch(()=>console.log('error!'))
// this is called chaining in promises and any error is caught in the catch call back
```

```
Promise exercise:
// Solve the questions below:

// #1) Create a promise that resolves in 4 seconds and returns "success" string

// #2) Run the above promise and make it console.log "success"


// #3) Read about Promise.resolve() and Promise.reject(). How can you make
// the above promise shorter with Promise.resolve() and console loggin "success"


// #4) Catch this error and console log 'Ooops something went wrong'
Promise.reject('failed')

// #5) Use Promise.all to fetch all of these people from Star Wars (SWAPI) at the same time.
// Console.log the output and make sure it has a catch block as well.
const urls = [
  'https://swapi.co/api/people/1',
  'https://swapi.co/api/people/2',
  'https://swapi.co/api/people/3',
  'https://swapi.co/api/people/4'
]

// #6) Change one of your urls above to make it incorrect and fail the promise
// does your catch block handle it?

My solution:
const promise = new Promise((res,rej) => {
    setTimeout(res,4000,'success');
})

promise.then((val)=>{
  console.log(val);
})

function resolved(val) {
  console.log(val);
}
function rejected(val) {
  console.log('errored out' + val);
}

Promise.resolve('success').then(resolved,rejected);
Promise.reject(new Error('errorr')).then(resolved,rejected);

const urls = [
  'https://swapi.co/api/people/1',
  'https://swapi.co/api/people/2',
  'https://swapi.co/api/people/3',
  'https://swapi.co/api/people/4'
]

Promise.all(urls.map((d)=>{
  fetch(d).then(r=>r.json());
})).then((d)=>{console.log(d[0])})
.catch((e)=>{console.error(e);})

Promise.all(urls.map(url =>
    fetch(url).then(people => people.json())
))
  .then(array => {
    console.log('1', array[0])
    console.log('2', array[1])
    console.log('3', array[2])
    console.log('4', array[3])
  })
  .catch(err => console.log('ughhhh fix it!', err));

Solution from course:https://cdn.fs.teachablecdn.com/B7fUr4YJTp94cSa9r3rj
```
- Async await (part of es8 and built on top of promise)
- It is as same as a promise but syntactic sugar to look better like synchronous.
- Add async before function or variable name and inplace of .then use await

```
fetch(url).then((res)=>res.json()).then(console.log)
VS
async function fetchUsers() {
   const res = await fetch('url');
   const data =await res.json();
   console.log(data);
}
we can use try,catch for replacing then,catch

Exercise:
// Solve the below problems:

// #1) Convert the below promise into async await
fetch('https://swapi.co/api/starships/9/')
  .then(response => response.json())
  .then(console.log)

async function fetchStarship() {
  const response = await fetch('https://swapi.co/api/starships/9/')
  const data = await response.json();
  console.log(data);
}

// #2) ADVANCED: Update the function below from the video to also have
// async await for this line: fetch(url).then(resp => resp.json())
// So there shouldn't be any .then() calls anymore!
// Don't get discouraged... this is a really tough one...
const urls = [
  'https://jsonplaceholder.typicode.com/users',
  'https://jsonplaceholder.typicode.com/posts',
  'https://jsonplaceholder.typicode.com/albums'
]

const getData = async function() {
  const [ users, posts, albums ] = await Promise.all(urls.map(url =>
      fetch(url).then(resp => resp.json())
  ));
  console.log('users', users);
  console.log('posta', posts);
  console.log('albums', albums);
}

const getData = async function() {
  const [ users, posts, albums ] = await Promise.all(urls.map(async function(url) {
      const response = await fetch(url);
      return response.json();
  }));
  console.log('users', users);
  console.log('posta', posts);
  console.log('albums', albums);
}

// #3)Add a try catch block to the #2 solution in order to catch any errors. // Now, use the given array containing an invalid url, so you console.log  //your error with 'oooooops'.
const urls = [
  'https://jsonplaceholder.typicode.com/users',
  'https://jsonplaceholdeTYPO.typicode.com/posts',
  'https://jsonplaceholder.typicode.com/albums'
]

const getData = async function() {
  try {
    const [ users, posts, albums ] = await Promise.all(urls.map(async function(url) {
        const response = await fetch(url);
        return response.json();
    }));
    console.log('users', users);
    console.log('posta', posts);
    console.log('albums', albums);
  } catch (err) {
    console.log('ooooooops', err);
  }
}

Solution for Exercise: https://cdn.fs.teachablecdn.com/LasINue3SECECn6p9RvQ

```
- spread in es6
```
const arr = [1,2,3];
function summer(a,b,c) {
    return a+b+c;
}
summer(...arr); //spreading of arr into a,b,c

```

- Similar or(object destructor in es6) es2018 object spread operator
```
const animals = {
    tiger:23,
    lion:5,
    monkey:2,
    bird:40
}

function objectSpreador(a1,a2,a3) {
    console.log(a1);
    console.log(a2);
    console.log(a3);
}

const {tiger,lion,...rest} = animals;

objectSpreador(tiger,lion,rest);

```

- finally in promise is similar to other languages called regardless of other then and catch
