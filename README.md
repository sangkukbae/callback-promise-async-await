# callback-promise-async-await

## Callbacks
```javascript
function printString(string){
  setTimeout(
    () => {
      console.log(string)
    }, 
    Math.floor(Math.random() * 100) + 1
  )
}

function printAll(){
  printString("A", () => {
    printString("B", () => {
      printString("C", () => {})
    })
  })
}
printAll()
```
:warning: The problem with callbacks is it creates something called *“Callback Hell.”* Basically, you start nesting functions within functions within functions, and it starts to get really hard to read the code.

## [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
```javascript
function printString(string){
  return new Promise((resolve, reject) => {
    setTimeout(
      () => {
       console.log(string)
       resolve()
      }, 
     Math.floor(Math.random() * 100) + 1
    )
  })
}

function printAll(){
  printString("A")
  .then(() => {
    return printString("B")
  })
  .then(() => {
    return printString("C")
  })
}
printAll()

//es6
function printAll(){
  printString("A")
  .then(() => printString("B"))
  .then(() => printString("C"))
}
printAll()
```
## [Async Await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
```javascript
async function printAll(){
  await printString("A")
  await printString("B")
  await printString("C")
}
printAll()
```
**callback-promise-async await**
```javascript
function addString(previous, current, callback){
  setTimeout(
    () => {
      callback((previous + ' ' + current))
    }, 
    Math.floor(Math.random() * 100) + 1
  )
}

//callback
function addAll(){
  addString('', 'A', result => {
    addString(result, 'B', result => {
      addString(result, 'C', result => {
       console.log(result) // Prints out " A B C"
      })
    })
  })
}
addAll()

//promise
function addString(previous, current){
  return new Promise((resolve, reject) => {
    setTimeout(
      () => {
        resolve(previous + ' ' + current)
      }, 
      Math.floor(Math.random() * 100) + 1
    )
  })
}

function addAll(){  
  addString('', 'A')
  .then(result => addString(result, 'B'))
  .then(result => addString(result, 'C'))
  .then(result => {
    console.log(result) // Prints out " A B C"
  })
}
addAll()

//async await
async function addAll(){
  let toPrint = await addString('', 'A')
  toPrint = await addString(toPrint, 'B')
  toPrint = await addString(toPrint, 'C')
  console.log(toPrint) // Prints out " A B C"
}
addAll()
```
:memo: **참고 자료**
* [https://medium.com/front-end-weekly/callbacks-promises-and-async-await-ad4756e01d90](https://medium.com/front-end-weekly/callbacks-promises-and-async-await-ad4756e01d90)   
* [https://scotch.io/courses/10-need-to-know-javascript-concepts/callbacks-promises-and-async](https://scotch.io/courses/10-need-to-know-javascript-concepts/callbacks-promises-and-async)   
* [https://www.sitepoint.com/flow-control-callbacks-promises-async-await/](https://www.sitepoint.com/flow-control-callbacks-promises-async-await/) :bookmark:   
* [https://developers.google.com/web/fundamentals/primers/async-functions](https://developers.google.com/web/fundamentals/primers/async-functions)   
* [https://www.sitepoint.com/simplifying-asynchronous-coding-async-functions/](https://www.sitepoint.com/simplifying-asynchronous-coding-async-functions/)   
* [https://eloquentjavascript.net/11_async.html#c_f7XSZ4G+k8](https://eloquentjavascript.net/11_async.html#c_f7XSZ4G+k8)   
* [https://leanpub.com/understandinges6/read/#leanpub-auto-promises-and-asynchronous-programming](https://leanpub.com/understandinges6/read/#leanpub-auto-promises-and-asynchronous-programming)   
* [https://exploringjs.com/es2016-es2017/ch_async-functions.html](https://exploringjs.com/es2016-es2017/ch_async-functions.html) :orange_book:   
* [https://exploringjs.com/es6/ch_promises.html](https://exploringjs.com/es6/ch_promises.html)   
* [https://ponyfoo.com/books/practical-modern-javascript/chapters/4#promise-continuation-and-chaining-6NszCpCz](https://ponyfoo.com/books/practical-modern-javascript/chapters/4#promise-continuation-and-chaining-6NszCpCz)   
