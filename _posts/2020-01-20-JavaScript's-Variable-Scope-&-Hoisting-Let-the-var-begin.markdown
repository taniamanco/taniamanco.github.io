---
layout: post
title:  "JavaScript's Variable Scope & Hoisting - Let the var begin"
date:   2020-01-20 08:00:00 -0400
categories: from zero to tech
---



Scope & Hoisting are two JavaScript concepts which are a bit confusing to newcomers. For a better understanding of what those concepts are and before we look at variables, functions, and it's behavior, let's examine those concepts in detail.

**Scope:**

Defines the visibility or, in other words, where variables and functions accessible in the program. Scope divides into two kinds; Local and Global. Simply put, If a variable declaration occurs inside a function, the variable's scope is local. Making it to be visible in the scope of that function and invisible (not accessible) outside. On the other hand, any declaration outside a function means that the variable's scope is global. 

Let's examine the following example: 
```
function innerScopeEx () {
  let innerScope= "I'm accsesble only inside this function";
  console.log("In function");
  console.log(innerScope);
}
console.log(innerScope);

innerScopeEx(); 
```

Will work the same with var declaration. 

```
let globalScope = "I'm accessible on the global scope";

function globalScopeEx(){
  console.log("In function");
  console.log(globalScope); 
}
console.log("out of function");
console.log(globleScope); 
```
Will print: 
In function
I'm accessible on the global scope
out of function

**Hoisting:**

 "A strict definition of Hoisting suggests that variable and function declarations are physically moved to the top of your code, but this is not what happens. Instead, the variable and function declarations are put into memory during the compile phase, but stay exactly where you typed them in your code." (-mdn)

In other words, when the JavaScript interpreter runs, it will first scan through the entire program's code then bump (hoist) variable declarations to the top of their respective scope. By the end of the interpretation phase, the program is ready to be executed.

Once again, let's examine some examples:
```
function myName(name) {
  console.log(" My name is " + name);
}

myName("Tania"); 
```
Will print: My name is Tania

In this example, the function written and declared then invoked with an argument. What will happen if we will invoke the function before it declared like the next example? 

```
myName("Tania");

function myName(name) {
  console.log(" My name is " + name);
}
```
Will print: My name is Tania

Based on what we just discussed, Hoisting is allowing us to invoke a function before it was declared. 
Hoisting works with other data types and variables as well. 
The variables can be initialized and used before the declaration.

Please keep in mind that Hoisting is applicable only for declarations, **NOT** initializations!

For example: 
```
let name = "Tania";
console.log(  " My name is  " + name +  " , " + city);
let city = "NYC"; 
```
This one won't work because it can't access the city before initialization. We can fix it many ways, to explain Hoisting, we will split the declaration and initialization of "City." 

```
var name = "Tania";
city = "NYC";
console.log( " My name is " + name + ", " + "I live in " + city);
var city; 
```
Will print: My name is Tania, I live in NYC.
Here we initialized the city but declared only later on. 
Another example for Hoisting: 

```
name = "Tania";
city = "NYC"; 
console.log(  " My name is  " + name +  ", " + "I live in " + city);
var name, city;
```
in this example, we initialized first and declared only later (Will discuss why its var and not let later on)

**Variables:**

Variables declarations processed before any code executed (Hoisting). 
Variable scope declared with var, let or const in its current execution context, which can be a function or a block or neither. (see scope explanation). 
Assigning a value to an undeclared variable by default made the variable a global variable when the assignment executed.

For example:
```
function x () {
  city = "NYC";
  let name = "Tania";
}
x()

console.log(city);
console.log(name);
```
As we discussed in Hoisting, declared variables created **BEFORE** any code executed; undeclared variables do not exist until the code executed. 

**Tip:** 
Recommended to declare variables, regardless of their scope. 

There are three types of variables, var, let & const. 
Les go through each one to learn more. 

**var** - can be reassigned. 
    Scope of a var variable is the entire enclosing function.
    Hoisting - undefined when accessing a variable before the declaration. 
    Create a property on the global obj.
    
**let** - can be reassigned, initialization is not final.
    Block scoped, available inside the whole block, is created in as well as any sub-blocks. 
  Hoisting  - reference error when accessing a variable before the declaration.
     Do not become property of the obj.
     
**const** - 
   Behaves the same as let, the only difference is that const cant reassigned, initialization is final and mandatory. That is what makes the const variable to a Read-only reference of a value. 

For example: 
```
scopping();

function scopping () {
  let a = "One";
  var b = "Two";
  const c = "Three";
  if (true) {
    a = "Four";
    b = "Five";
    console.log(a, b)
    c = "Six";
  }
}
```
Will print Four, Five, and an error because const can't be reassigned. 
```
function scoppingEx () {
  let d = "One";
  var e = "Two";
}
console.log(d, e)
```
In this case d will rise an error of undifeined, d defined as let variable while var was accssible out side ot the function. 

resources:
mdn.org
