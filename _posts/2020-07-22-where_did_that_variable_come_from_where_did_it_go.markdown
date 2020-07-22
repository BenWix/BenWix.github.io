---
layout: post
title:      "Where did that variable come from? Where did it go?"
date:       2020-07-22 19:47:13 +0000
permalink:  where_did_that_variable_come_from_where_did_it_go
---


Javascript has some very powerful tools and with ES5 and ES6, it has gained great readbaility. However, there are still a few things that make javascript seem a little funky sometime. We can take a look at hositing and some of the scopes of variable to learn more of the quirks that can happen is javascript.

```
var x = 5 

console.log(x) //logs 5
```

We have this straight forward example, but below we have another example that accomplishes the same thing

```
x=5
console.log(x) //logs 5
var x
```

How can these two code snippets have the same outcome, when this third example won't work.

```
console.log(x) //logs undefined
var x = 5
```

Well this is down to a principle in javascript called hoisting. In simplest terms, when a script is run, it is run twice. The first time through javascript will find all the variable declarations and the second time it will execute the rest of the code. 

So if the variable is declared before the rest of the code is run, why doesn't the third code snippet work?

The variable x is declared, but the value has not been assigned to it yet. When hoisting, only the declaration is hosited and run first, not the assignment. So these are a bit funky, and they don't even happen all the time. When updates happened with es5 and es6, let and const were added. They behave differently from var in a few ways. 

Firstly when a variable is declared with const or let, it will NOT be hoisted. So in the following code example

```
console.log(x)
let x = 5
```

We would get an error stating "Cannot access 'x' before initialization. So when we use let, nothing is hoisted!! This definitely makes the code more intuitive to understand and it also allows for const and let to have block scope.

```
myFunction = () => {
   let myVar = 'What I said first'
	 
	 if (true) {
	    let myVar = 'What I said second'
			}
			
			console.log(myVar)


}

myFunction()
```

Now figuring out what the output of this function is can be a bit daunting. I can hear you screaming 'BUT BEN, you can't declare a variable with let more than once!!!'. And you would be right, but this would not throw an error and it will actually log 'What I said first'. The reason for this is that when a variable is declared with let or const, it has BLOCK SCOPE. So inside the if statement, javascript doesn't even look at the first declaration of myVar, it only knows the declaration inside of the block. And outside of that block, javascript will only look at the first declaration of myVar. 

Let's look at one more example of scope.

```
let myVar = 'I am on the way outside'

function printThings() {
   if (true) {
	 let myVar = 'I am on the way inside'
   }
	 
	 console.log(myVar)
}

printThings()
```

So since we learned about block scope, you might think that this console.log wouldn't know what myVar is, but it DOES know what myVar is. Javascript will first look inside the space where that variable is used, in this case it will look in the function printThings. If it doesn't see a declaration of that variable, it will move up to the next scope, which is the global scope in this case, and look for a declaration of this variable. So this will log 'I am on the way outside'. It will not log 'I am on the way inside' because javascript cannot and will not move to more specific scopes to find a variable, it will only move out to less specific scopes to find a variable.

So what are some techniques to help avoid the pitfalls of hoising and the confusing block scope.

* Don't reuse variable names whenever possible, always using different variable names will make your code much more clear and less likely to have errors
* Always declare variables with let or const. Var is outdated and can be slightly problamatic, and not declaring a variable will make it global scope which can cause a whole bunch of problems to your code if the variable name is used anywhere else 

Following these guidelines and knowing some of the funky behaviors of javascripts can help you make your code as clean and friendly as possible.



