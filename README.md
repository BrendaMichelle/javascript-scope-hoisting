# JavaScript: Scope

![alt text](/pics/js-encouragement.jpg "You got this!")
### Objective
By the end of this lesson, students will be able to:
1. Explain what *scope* is
2. Describe the difference between *global scope* vs *function scope* vs *block scope*
3. Demonstrate understanding of the difference between *var*, *let*, & *const*

## What is [Scope](https://developer.mozilla.org/en-US/docs/Glossary/Scope)?

Scope refers to the accessibility of a variable from certain locations in your code. If a variable or another expression is not in the "current scope", then it means that we cannot use that variable or expression. If we try to use a variable that is not in the current scope, then we will get an error or unexpected/unintended behavior. Not good! We can avoid a lot of debugging headaches if we understand scope!

We have three different types of scope - global scope, function scope, and block scope. We can compare [scope to levels of government](https://blog.codeanalogies.com/2017/11/22/how-javascript-variable-scoping-is-just-like-multiple-levels-of-government/). There are laws that apply all over the world and laws that apply only to certain locations just like in scope, we have variables that are accessible everywhere and other variable that are only accessible in certain functions or blocks. 

For example, we have human rights laws created by the United Nations and those laws apply all over the world (global scope). Then each nation may have its own set of laws. For example, the US legal drinking age is 21 and this law applies only to the US and not to other countries (function scope). Then, we have states and each state may have their own laws. For example, the state of New York does not permit establishments to allow patrons to "B.Y.O.B." if the establishment does not have a license or permit to sell alcoholic beverages. This law applies to NY, but not necessarily to another state or nation.

##### Global Scope
If a variable has global scope, then it is accessible anywhere in your script. If it is not necessary to make a variable global, then we avoid making the variable global because we don't want to *pollute* the global scope. Polluting the global scope is bad practice because it will make it harder for us to debug and our code will be more error prone.

```javascript
function numOfPets () {
    petCount += 1; /* petCount is accessible here */
    console.log(`I have ${petCount} pets`); /* I have 6 pets */
}

var petCount = 5; /* we are declaring & initializing petCount variable in the global scope */
numOfPets();
```

##### Function Scope
If a variable has function scope, then it is accessible within that function, but not outside of that function.

```javascript
function numOfCats () {
    var catCount = 5; // this variable only exists within this function
    console.log(`I have ${catCount} cats!`); // I have 5 cats!

}

function numOfDogs () {
    var dogCount = 2; // this variable only exists within this function
    console.log(`I have ${dogCount} dogs!`); // I have 2 dogs!
}


numOfCats();
numOfDogs();
console.log(dogCount); // "Uncaught ReferenceError: dogCount is not defined"
console.log(catCount); // "Uncaught ReferenceError: catCount is not defined"

// catCount & dogCount do not exist in this scope! 
// So if you try to access them outside their scope, it will result in an error
```

##### Block Scope
If a variable has block scope, then it is accessible within its immediate enclosing parenthesis. A variable that has block scope has an even more narrow scope than variables with function scope. We will see examples of block scope in the **Let** section!


## [Var](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)
- We've been using **var**, but we have not talked about it in depth, yet. Var is a keyword that we can use to declare a variable. 
- If we declare a variable outside of any function using var, then our variable will have global scope. However, if we declare a variable inside of a function, then our variable will have function scope. Therefore, it will be accessible anywhere inside of that function and in any contained sub-functions, but not outside. 

- If we try to redeclare a variable using var, the original variable will simply be overwritten.

- Another tidbit to note is that variables declared with var are hoisted, but don't worry about what that means for now. We will get into it tomorrow.



## [Let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let) 
- **Let** was introduced in ES6. It is a keyword that we can use to declare a variable. 
- Variables declared with let are blocked scope meaning that they are accessible within the block in which they are defined and in any contained sub-blocks. You can think of a block being the area within a set of curly braces. However, note that if you declare a variable outside of any function using let, then that variable will have global scope. 

- Another feature of let is that if we try to redeclare a variable within the same scope using let, we will get a syntax error.

- Another tidbit to note is that variables declared with let are *not* hoisted, but again, don't worry about what that means for now as we will review that tomorrow.

## [Const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
- **Const** was also introduced in ES6 and like let & var, it is also a keyword that we can use to declare a variable.
- Variables declared with const are block scoped unless they are declared outside of any function just like let.
- Variables declared with const are constant meaning that they cannot be changed through reassignment and they cannot be redeclared. If you try to change or redeclare a constant variable, then you will get an error.
- Variables declared with const must also be initialized at the same time.

&nbsp;
&nbsp;



| Keyword        | Scope           | Can be reassigned?  | Can be redeclared? | Hoisted?
| :-------------: |:-------------:| :-----:| :------:| :--------:|
| var      | Function | Yes | Yes | Yes |
| let      | Block      |   Yes | No | No |
| const | Block      |    No | No | No |
___
---
## Let's review
1. What are some differences between var & let?
2. What are some differences between let & const?
3. What are some best practices regarding variable declaration?


___
---

![any questions?](/pics/any-questions.jpg)

___



## Test Yourself

1. 
```javascript
function doSomething () {
    var num = 9;
    let num = 1;
    console.log(num);
}
doSomething();
```
<details><summary>What will be logged out?</summary>
<p>

Nothing; We will get a syntax error.

<img src="pics/syntax-err.png">
</p>
</details>




2. 
```javascript
function doSomething () {
    const num = [];
    num.push(1);
    num.push(3);
    console.log(num);
}
doSomething();
```
<details><summary>What will be logged out?</summary>
<p>

[1, 3]

We are not reassigning the const num, so it is perfectly valid to change the contents within the array! It works similarly with const objects.
</p>
</details>




3. 
```javascript
function forecastWeather () {
    const weather = {snow: true};
    weather.rain = false;
    weather.sun = true;
    weather.temperature = 25;
    console.log(weather);
}
forecastWeather();
```
<details><summary>What will be logged out?</summary>
<p>

{snow: true, rain: false, sun: true, temperature: 25}

Just like the previous example, we are not changing the weather object by reassignment or redeclaration, so this does not throw an error.
</p>
</details>



4. 
```javascript
function decreaseTemp () {
    temperature -= 4;
    console.log(temperature); 
}

const temperature = 99;
decreaseTemp();
```
<details><summary>What will be logged out?</summary>
<p>
    
Nothing; This will throw an error.

<img src="pics/type-err.png">
</p>
</details>




5. 
```javascript
var num = 8;
function doMath () {
    num += 3;
    
    if (num % 4 == 0) {
        return true;
    }
    else{
        return false;
    }
}

num += 1;
doMath();
```
<details><summary>What will be returned?</summary>
<p>
    
True
</p>
</details>

6. 
```javascript

function doMath () {
    let x = 10;
    let y = 20;
    
    function add(){
        let x = 5;
        return x + y;
    }

    let z = add();
    console.log(`x = ${x}`);
    console.log(`z = ${z}`);
}

doMath();
```
<details><summary>What will be returned?</summary>
<p>
    
x = 10

z = 25
</p>
</details>



7. 
```javascript
function doSomething () {
    var num = 88;
    console.log(`inside of doSomething`);
    console.log(`num = ${num}`);
}
var num = 5;
console.log(`outside of function`);
console.log(`num = ${num}`);
```
<details><summary>What will be logged out?</summary>
<p>
    
outside of doSomething    

num = 5
</p>
</details>



 
8. 
```javascript
function doSomething () {
    var num = 88;
    console.log(`inside of doSomething`);
    console.log(`num = ${num}`);
}
var num = 5;
doSomething();
console.log(`outside of function`);
console.log(`num = ${num}`);
```
<details><summary>What will be logged out?</summary>
<p>
    
inside of doSomething

num = 88

outside of doSomething

num = 5
</p>
</details>


----

#### Extra Resources
- [W3 Schools on Scope](https://www.w3schools.com/js/js_scope.asp)
- [Digital Ocean on variables, scope, & hoisting](https://www.digitalocean.com/community/tutorials/understanding-variables-scope-hoisting-in-javascript)
