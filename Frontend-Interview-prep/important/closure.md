https://www.javascripttutorial.net/javascript-closure/
## A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function's scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.
// Closure
/*
inner members have access to outer members
members (variables, functions)
e.g. debounce, curry

function add1 () {
  var a = 1
  return function add2() {
     Can I get a?
  }
}
*/

JavaScript closures
Let’s modify the greeting() function:

function greeting() {
    let message = 'Hi';

    function sayHi() {
        console.log(message);
    }

    return sayHi;
}
let hi = greeting();
hi(); // still can access the message variable
Code language: JavaScript (javascript)
Now, instead of executing the sayHi() function inside the greeting() function, the greeting() function returns the sayHi() function object.

Note that functions are the first-class citizens in JavaScript, therefore, you can return a function from another function.

Outside of the greeting() function, we assigned the hi variable the value returned by the greeting() function, which is a reference of the sayHi() function.

Then we executed the sayHi() function using the reference of that function: hi(). If you run the code, you will get the same effect as the one above.

However, the interesting point here is that, normally, a local variable only exists during the execution of the function.

It means that when the greeting() function has completed executing, the message variable is no longer accessible.

In this case, we execute the hi() function that references the sayHi() function, the message variable still exists.

The magic of this is closure. In other words, the sayHi() function is a closure.

## A closure is a function that preserves the outer scope in its inner scope.

## A function can be created at any moment, passed as an argument to another function, and then called from a totally different place of code later.


sum(a) {
    sum(b){
        return a + b

    }
}

function sum(a) {
    return function(b){
        return a + b
    }
}

<script>
// function isBetween(a,b){
//     if this > a && this < b:
//         return true
//     else:
//         return false
// }

function isBetween(a,b){
    return function(x){
        return x >= a && x <= b;
    };
}

// function inArray(a){
//     if this in a:
//         return true
//     else:
//         return false
// }

function inArray(arr){
    return function(x){
        return arr.includes(x)
    }
}


function f() {
  let value = 123;

  return function() {
    alert(value);
  }
}

let g = f(); 


/////////
const greet = function(greeting) {
    return function(name) {
        console.log(greeting, name)
    };
};

const greetHey = greet('Hey');
greetHey('Jonas')
greetHey('Blaire')

greet('Hello')('Blaire')


///////// arrow function ///////

const greet = (greeting) => {
    return (name) => {
        console.log(greeting, name)
    };
};

const greetArrow = greeting => name => console.log(greeting, name);
greetArrow('Hello')('Blaire')


</script>




closure
A closure is a function that remembers its outer variables and can access them. In some languages, that’s not possible, or a function should be written in a special way to make it happen. But as explained above, in JavaScript, all functions are naturally closures (there is only one exception, to be covered in The "new Function" syntax).

That is: they automatically remember where they were created using a hidden [[Environment]] property, and then their code can access outer variables.



Variables are accessible only 
inside block (block scoped)
⚠ HOWEVER, this only applies to **let** and **const** variables!
**var** is still accessible outside of the block
var is *function scoped*

Functions are also block scoped
(only in strict mode



let and const --> block scoped
var --> function scoped


Scoping asks the question “Where do variables live?” or “Where can we access a certain variable, and where not?”;
� There are 3 types of scope in JavaScript: the global scope, scopes defined by functions, and scopes defined by blocks;
� Only let and const variables are block-scoped. Variables declared with var end up in the closest function scope;
� In JavaScript, we have lexical scoping, so the rules of where we can access variables are based on exactly where in the 
code functions and blocks are written;
� Every scope always has access to all the variables from all its outer scopes. This is the scope chain!
� When a variable is not in the current scope, the engine looks up in the scope chain until it finds the variable it’s looking 
for. This is called variable lookup;
� The scope chain is a one-way street: a scope will never, ever have access to the variables of an inner scope;
� The scope chain in a certain scope is equal to adding together all the variable environments of the all parent scopes;
� The scope chain has nothing to do with the order in which functions were called. It does not affect the scope chain at all