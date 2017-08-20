# JavaScript Prelude to Redux:

## Function definitions
When we will explore the beauties of redux, we will work with functions a lot. So let's reherse the ways how one would write a function.


The traditional way of defining a function that has been in the language from the very beggining:
```js
function foo() {
  // function body where we can have anything
  console.log("howdy stranger?")

  // optional return statement which determines 
  // the return value of this function when called
  return "anything, like this string you are just reading"
}
```
If a function doesn't contain a `return` statement, or doesn't reach it, e.g.
```js
function foo() {
  if (false) { return 5 }
}
```
then it evaluates to `undefined`.

---
So yeah, a function, nothing new there.

We have a differrent way of defining a function using the arrow function syntax. We would go about it like so (let's make it behave like the previous one):
```js
const foo = () => {
  console.log("howdy stranger?")

  return "anything, like this string you are just reading"
}
```
So there you go, probably not much new stuff there. Now we have multiple ways of doing the same thing, right?

Well, not really. For many use cases, they are the same, and so we favor arrow functions where we can for the sake of consistency, but they cannot be blindly replaced. More info [here](https://stackoverflow.com/questions/34361379/arrow-function-vs-function-declaration-expressions-are-they-equivalent-exch).

I would like to focus on a second difference here. An arrow function, doesn't have to have a body. If an **expression** follows the fat arrow, it is used as an implicit return value.

So first things first, an `expression`. What is that? It's pretty much something that resolves to a value. So let's look at a few examples of expressions.
```js
[1, 2, 3] // an array is an expression
{name: 'Zoe', age: 10} // an object is an expression
5 // // a number is an expression
"hello" // a string is an expression

function() { return 5 } // a function is NOT an expression

// but it can be made into an expression
(function() { return 5 }()) // an expression
```
So the second example is an IIFE (immediately invoked function expression), making the definition of such function resolve to value, making it AN EXPRESSION.

Okay, so hopefully it had been reasonably clear so far, so let's see how we can utilize the knowledge we just gained.

We already mentioned, that an arrow function doesn't have to have a body, if an expression follows the `=>`.

Let's see that in action.
```js
const foo = () => 5 // the number 5 is implicitly returned
const foo = () => (5) // we can wrap it in parantheses
cost foo = x => x + 5
cost foo = x => x.toString().toUppercase()
```

This is also usefull when defining stateless react components, like so:
```js
const Component = () => (
  <div>I did NOT have to write the return keyword, oh yeah!</div>
)
```
This is good because that's how we ideally want our components to look like.
Sometimes, however, we need them to do something else, so a body may be required.
```js
const Component = () => {
  console.log('something')

  return (
    <div>I did NOT have to write the return keyword, oh yeah!</div>
  )
)
```
Notice how here, we had to specify the `return` keyword.

There's one specific thing, that we need to cover, though. Which will be crucial for us if we want to avoid carpal tunnel from writing too much code when using redux.

Notice how a function body is delimited by curly braces `{}`. What if we want to return an object, which is also using `{}` for it's definition.

This won't work:
```js
const foo = () => { name: 'John' }
```
Because JavaScript thinks it's function body, not an object that you want to implicitly return. Remember how we wrapped our boy `5` in parantheses though? Well guess what, we can do that here too.
```js
const foo = () => ({ name: 'John' })
```
And just like that, it works!

## Destructuring
I am unsure to what degree you covered object destructuring, but a quick recap won't hurt anybody, right?

So let's suppose we have this simple stateless component in react, that we are now capable of defining so many different ways!

```js
const Title = () => <h1>some title</h1>
```
Very nice component! Not very reusable, though. So let's try and see how we can fix that. For just that we have `props` in react, for the sake of this example, let's call the prop `text`.
```js
const Title = props => <h1>{props.text}</h1>
```
Props are passed to the stateless component as the first argument. We can then use the aformentioned destructuring feature to make at all nice and pretty.
```js
const Title = ({ text }) => <h1>{text}</h1>
```

To generalize upon this concept, let's have a look at the following code sample, but it doesn't really get any more complicated than what we've just seen.

```js
const someObject = { a: { b: 'some value' }, xx: 42 }
const { xx } = someObject
console.log(xx) // => 42

const { b } = someObject.a
console.log(b) // => 'some value'
```
You can also do nested destructuring, but personally I do not like it for it's inferior readability so I will not go over that here.

And just like that we covered what we needed for the redux lesson, in order for js syntax not to confuse us.

Sorry for disrupting your peace during a weekend, but I hope you will benefit from going over this info in order to get the most out of the redux lesson.
