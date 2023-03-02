Currying is a function that takes one argument at a time and returns a new function expecting the next argument. It is a transformation of functions that translates a function from callable as f(a, b, c) into callable as f(a)(b)(c).

Currying simply means evaluating functions with multiple arguments and decomposing them into a sequence of functions with a single argument.

In other terms, currying is when a function — instead of taking all arguments at one time — takes the first one and returns a new function, which takes the second one and returns a new function, which takes the third one, etc. until all arguments are completed.

https://blog.logrocket.com/understanding-javascript-currying/ 

Currying doesn't call a function. It just transforms it.

**Currying**: a function that accepts multiple arguments. It will transform this function into a series of functions, where every little function will accept a single argument until all arguments are completed
**Partial application**: a function is partially applied when it is given fewer arguments than it expects and returns a new function expecting the remaining arguments
const addPartial=(x,y,z) => {
    return x+y+z 
}
var partialFunc= addPartial.bind(this,2,3);
partialFunc(5); //returns 10

Currying is converting a single function of n arguments into n functions with a single argument each. Given the following function:

function f(x,y,z) { z(x(y));}
When curried, becomes:

function f(x) { lambda(y) { lambda(z) { z(x(y)); } } }
In order to get the full application of f(x,y,z), you need to do this:

f(x)(y)(z);
Many functional languages let you write f x y z. If you only call f x y or f(x)(y) then you get a partially-applied function—the return value is a closure of lambda(z){z(x(y))} with passed-in the values of x and y to f(x,y).

 The easiest way to see how they differ is to consider a real example. Let's assume that we have a function Add which takes 2 numbers as input and returns a number as output, e.g. Add(7, 5) returns 12. In this case:

Partial applying the function Add with a value 7 will give us a new function as output. That function itself takes 1 number as input and outputs a number. As such:

Partial(Add, 7); // returns a function f2 as output

                 // f2 takes 1 number as input and returns a number as output
So we can do this:

f2 = Partial(Add, 7);
f2(5); // returns 12;
       // f2(7)(5) is just a syntactic shortcut
Currying the function Add will give us a new function as output. That function itself takes 1 number as input and outputs yet another new function. That third function then takes 1 number as input and returns a number as output. As such:

Curry(Add); // returns a function f2 as output

            // f2 takes 1 number as input and returns a function f3 as output
            // i.e. f2(number) = f3

            // f3 takes 1 number as input and returns a number as output
            // i.e. f3(number) = number
So we can do this:

f2 = Curry(Add);
f3 = f2(7);
f3(5); // returns 12
In other words, "currying" and "partial application" are two totally different functions. Currying takes exactly 1 input, whereas partial application takes 2 (or more) inputs.

Even though they both return a function as output, the returned functions are of totally different forms as demonstrated above.




--------------
**Partial application**
Is a technique of fixing a number of arguments to a function, producing another function of smaller arguments i.e binding values to one or more of those arguments as the chain of function progressed.

function add1(x) {
  return 1 + x;
}
JavaScript has the built-in method .bindthat works on functions with any number of arguments and can bind an arbitrary amount of parameters. Its invocation has the following syntax.

function.bind(thisValue, [arg1], [arg2], ...)
It turns function into a new function whose implicit this parameter is this value and whose initial arguments are always as given.

function addition(x, y) {
   return x + y;
}
const plus5 = addition.bind(null, 5)
plus5(10) // output -> 15
Note: this value does not matter for the (non-method) function addition which is why it is null above.

When using underscore or lodash you can use the partial function which is much nicer than the raw bind method.

Here is a detailed post on partial application and left, right partial application function implementation.
--------





<script>

function curry(f) {
    return function(a) {
        return function(b) {
            return f(a,b)
        }
    }
}

function sum(a,b){
    return a+b
}

let curriedSum = curry(sum)
console.log(curriedSum(1)(2)) // 3


let curriedSum = _.curry(sum) // from lodash library
console.log(curriedSum(1,2)) // 3
console.log(curriedSum(1)(2)) // 3

// More advanced implementations of currying, such as _.curry from lodash library, return a wrapper that allows a function to be called both normally and partially:

Noncurried version//
const add = (a, b, c)=>{
    return a+ b + c
}
console.log(add(2, 3, 5)) // 10

Curried version//
const addCurry =(a) => {
    return (b)=>{
        return (c)=>{
            return a+b+c
        }
    }
}
console.log(addCurry(2)(3)(5)) // 10



/////////// advanced currying /////////////////
const curry =(fn) =>{
    return curried = (...args) => {
        if (fn.length !== args.length){
            return curried.bind(null, ...args)
        }
    return fn(...args);
    };
}
const totalNum=(x,y,z) => {
    return x+y+z 
} 
const curriedTotal = curry(totalNum);
console.log(curriedTotal(10) (20) (30));
//////////////////////////////////////////

//////// Using bind method //////////
let multiply = function (x, y) {
    console.log(x*y)
}

let multiplyByTwo = multiply.bind(this, 2);
// is the same as
// let multiplyByTwo = function (y) {
//     let x = 2;
//     console.log(x*y)
// }

multiplyByTwo(5); // x = 2, y = 5 // 10

let multiplyByTwo = multiply.bind(this, 2, 3); 
multiplyByTwo(5); // x = 2, y = 3 // 6 // ignore 5 

let multiplyByTwo = multiply.bind(this,); 
multiplyByTwo(2, 3); // x = 2, y = 3 // 6 


let multiplyByThree = multiply.bind(this, 3);
multiplyByThree(5); // y = 5 // 15


//////////// using closures //////////////

let multiply = function (x) {
    return function(y) {
        console.log(x*y)
    }
}
let multiplyByTwo = multiply(); 
multiplyByTwo(2)(3)


let multiply = function (x) {
    return function (y) {
        return function(z){
            console.log(x*y*z);
        } 
    };
};
let multiplyByTwo = multiply(2)(3);
multiplyByTwo(4); // 24


let multiplyByTwo = multiply(2);
multiplyByTwo(3)(4); // 24



// not work
// let multiplyByTwo = multiply(2,3);
// multiplyByTwo(4);

// let multiplyByTwo = multiply(2);
// multiplyByTwo(3, 4);

</script>

Summary

Currying is a transform that makes f(a,b,c) callable as f(a)(b)(c). JavaScript implementations usually both keep the function callable normally and return the partial if the arguments count is not enough.

Currying allows us to easily get partials. As we’ve seen in the logging example, after currying the three argument universal function log(date, importance, message) gives us partials when called with one argument (like log(date)) or two arguments (like log(date, importance)).