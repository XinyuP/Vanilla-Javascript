https://www.javascripttutorial.net/javascript-call/
https://www.javascripttutorial.net/javascript-apply-method/
https://www.javascripttutorial.net/javascript-bind/

The call() method calls the function with a given this value and arguments provided individually.

<script>
    function Product(name, price) {
        this.name = name;
        this.price = price;
    }

    function Food(name, price) {
        Product.call(this, name, price);
        this.category = 'food';
    }

    console.log(new Food('cheese', 5).name);
    // Expected output: "cheese"

</script>

Using call() to invoke a function and specifying the this value
In the example below, when we call greet, the value of this will be bound to object obj, even when greet is not a method of obj.
<script>
function greet() {
  console.log(this.animal, "typically sleep between", this.sleepDuration);
}

const obj = {
  animal: "cats",
  sleepDuration: "12 and 16 hours",
};

greet.call(obj); // cats typically sleep between 12 and 16 hours
</script>

Using call() to invoke a function without specifying the first argument
If the first thisArg parameter is omitted, it defaults to undefined. In non-strict mode, the this value is then substituted with globalThis (which is akin to the global object).

<script>
globalThis.globProp = "Wisen";

function display() {
  console.log(`globProp value is ${this.globProp}`);
}

display.call(); // Logs "globProp value is Wisen"
</script>

In strict mode, the value of this is not substituted, so it stays as undefined.
<script>
"use strict";

globalThis.globProp = "Wisen";

function display() {
  console.log(`globProp value is ${this.globProp}`);
}

display.call(); // throws TypeError: Cannot read the property of 'globProp' of undefined
</script>

---------------------------------------------

The apply() method calls the specified function with a given this value, and arguments provided as an array (or an array-like object).
THe apply() method is similar to the call() method except that it takes the arguments of the function as an array instead of the individual arguments.


apply(thisArg)
apply(thisArg, argsArray)


This function is almost identical to call(), except that 
## call() accepts an argument list
## apply() accepts a single array of arguments 
— for example: 
    func.apply(this, ['eat', 'bananas'])
    func.call(this, 'eat', 'bananas').


--------------------------------------------
The bind() method returns a new function, when invoked, has its this sets to a specific value.

Unlike the call() and apply() methods, the bind() method doesn’t immediately execute the function. It just returns a new version of the function whose this sets to thisArg argument.

The bind() method allows an object to borrow a method from another object without making a copy of that method. This is known as function borrowing in JavaScript.

The bind() method creates a new function that, when called, has its this keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.

The bind() function creates a new bound function. Calling the bound function generally results in the execution of the function it wraps, which is also called the target function. The bound function will store the parameters passed — which include the value of this and the first few arguments — as its internal state. These values are stored in advance, instead of being passed at call time. You can generally see const boundFn = fn.bind(thisArg, arg1, arg2) as being equivalent to const boundFn = (...restArgs) => fn.call(thisArg, arg1, arg2, ...restArgs) for the effect when it's called (but not when boundFn is constructed).

A bound function can be further bound by calling boundFn.bind(thisArg, /_ more args _/), which creates another bound function boundFn2. The newly bound thisArg value is ignored, because the target function of boundFn2, which is boundFn, already has a bound this. When boundFn2 is called, it would call boundFn, which in turn calls fn. The arguments that fn ultimately receives are, in order: the arguments bound by boundFn, arguments bound by boundFn2, and the arguments received by boundFn2.

<script>
    "use strict"; // prevent `this` from being boxed into the wrapper object

    function log(...args) {
        console.log(this, ...args);
    }
    const boundLog = log.bind("this value", 1, 2);
    const boundLog2 = boundLog.bind("new this value", 3, 4);
    boundLog2(5, 6); // "this value", 1, 2, 3, 4, 5, 6

</script>

However, because a bound function does not have the prototype property, it cannot be used as a base class for extends.





<script>
///////////////////////////////////////
// The call and apply Methods
const lufthansa = {
  airline: 'Lufthansa',
  iataCode: 'LH',
  bookings: [],
  // book: function() {}
  book(flightNum, name) {
    console.log(
      `${name} booked a seat on ${this.airline} flight ${this.iataCode}${flightNum}`
    );
    this.bookings.push({ flight: `${this.iataCode}${flightNum}`, name });
  },
};

lufthansa.book(239, 'Jonas Schmedtmann');
lufthansa.book(635, 'John Smith');

const eurowings = {
  airline: 'Eurowings',
  iataCode: 'EW',
  bookings: [],
};

const book = lufthansa.book;

// Does NOT work
// book(23, 'Sarah Williams');

//////// Call method ////////////////
book.call(eurowings, 23, 'Sarah Williams');
console.log(eurowings);

book.call(lufthansa, 239, 'Mary Cooper');
console.log(lufthansa);

const swiss = {
  airline: 'Swiss Air Lines',
  iataCode: 'LX',
  bookings: [],
};

book.call(swiss, 583, 'Mary Cooper');

//////// Apply method  ///////////
// does basically the same thing, the only difference is that 
// apply does not receive a list of arguments after the this keywords, 
// but instead an array of the argument 

const flightData = [583, 'George Cooper'];
book.apply(swiss, flightData);
console.log(swiss);

book.call(swiss, ...flightData);

// explicitly define the this keyword in any function we want 



///////////////////////////////////////
// The bind Method
// Bind also allows us to manually set the this keywords for any function call
// The difference is that bind does not immediately call the function
// instead it returns a new function where the this keyword is bound
// book.call(eurowings, 23, 'Sarah Williams');

const bookEW = book.bind(eurowings);
const bookLH = book.bind(lufthansa);
const bookLX = book.bind(swiss);

bookEW(23, 'Steven Williams');

const bookEW23 = book.bind(eurowings, 23);
bookEW23('Jonas Schmedtmann');
bookEW23('Martha Cooper');

// With Event Listeners
lufthansa.planes = 300;
lufthansa.buyPlane = function () {
  console.log(this);

  this.planes++;
  console.log(this.planes);
};
// lufthansa.buyPlane();

document
  .querySelector('.buy')
  .addEventListener('click', lufthansa.buyPlane.bind(lufthansa));

// Partial application
const addTax = (rate, value) => value + value * rate;
console.log(addTax(0.1, 200));

const addVAT = addTax.bind(null, 0.23);
// addVAT = value => value + value * 0.23;

console.log(addVAT(100));
console.log(addVAT(23));

const addTaxRate = function (rate) {
  return function (value) {
    return value + value * rate;
  };
};
const addVAT2 = addTaxRate(0.23);
console.log(addVAT2(100));
console.log(addVAT2(23));
