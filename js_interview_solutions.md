# Javascript interviews

## Part one - Core JS

Clojures
```js
for (var i = 0; i < 5; i++) {
  setTimeout(function() {
    console.log(i)
  }, 1000)
}
```

What will this log, and when?

This program will log the number 5, 5 times, after 1 second
Understanding the event loop and closures would have allowed you to answer this question

### This
```js
var pet = {
  name: 'meow',
  sayName: function() {
    console.log(this.name)
  }
}

var speak = pet.sayName
speak()
```

  1. What is logged to the console
  2. How can we fix this

If this program is run in the browser, outside 'strict mode'. `this` inside `sayName` will be equal to the `window` object. The program will most likely log `undefined`.
If this program runs in 'strict mode', or in node. The value of this will be undefined, and the program will throw an error
Why?
When a function is called as a method on an object, the `this` variable is bound to that object. In the code above, speak is not called as a method on pet, so the `this` variable is not bound to pet.
Fix?
The solution is to add `.bind(pet)` to the declaration of `speak`

You should know
  1. How the this parameter gets assigned in Javascript
  2. How the methods, `bind`, `call` and `apply` work

### Event loop
```js
var mockRequest = function(callback) {
  var error = null

  setTimeout(function() {
    callback(error, { user: 'eoin' })
  }, 0)
}

var result
mockRequest(function(_, data) {
  result = data
})

if (result.user !== 'eoin') {
  throw new Error('test failed')
}
```
Question: what happens when you execute this code

When you execute this code the line `if (result.user !== 'eoin') {` throws the error: `Type Error: Cannot read property 'name' of undefined`

You should understand
  * That the synchronous code executes before the async code (How the event loop works!)
  * How callbacks (or/and higher order functions) work
  * That trying to access a property of a variable with the value of undefined throws an error


### Async basics

```js
var getUser = function() {
  var userId = window.localStorage.getItem('currentUserId')

  return api.request('/user', userId, function(err, data) {
    if (err) {
      return err
    }
    return  data
  })
}
```

The candidate should be able to see that the callback is being used incorrectly
The canditate should be able to see that the function `getUser` requires a callback paramiter
The canditate should be able to fix the code

Generally, you should be familiar with callbacks.

### Final Question
```js
var generateId = ((counter = 0) => () => { return counter++ })()
```

What is the `typeof generateId`
what is output from `console.log(generateId()); console.log(generateId());`

I leave this last one as an exercise for the reader
  * ES6 default values
  * Higher order functions
  * ES6 arrow functions
  * Immediately invoked function expressions (IIFE)
  * Closures in Javascript
