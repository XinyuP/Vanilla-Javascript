https://www.javascripttutorial.net/javascript-prototype/ 
In JavaScript, objects can inherit features from one another via prototypes. Every object has its own property called prototype.

Because a prototype itself is also another object, the prototype has its own prototype. This creates a something called prototype chain. The prototype chain ends when a prototype has null for its own prototype.


// console.log(this)
let myObj = {}

function Cat() {

}

let kitty = new Cat()

console.log(myObj.__proto__)
console.log(Object.prototype)

console.log(kitty.__proto__ === Cat.prototype)

console.log(kitty.__proto__.__proto__ === Object.prototype)


<script>
person.__proto__

person.constructor
ƒ Object() { [native code] }

person.constructor.prototype
{constructor: ƒ, __defineGetter__: ƒ, __defineSetter__: ƒ, hasOwnProperty: ƒ, __lookupGetter__: ƒ, …}

person.__proto__
{constructor: ƒ, __defineGetter__: ƒ, __defineSetter__: ƒ, hasOwnProperty: ƒ, __lookupGetter__: ƒ, …}

person.__proto__ === person.constructor.prototype
true


---------------------------
let person = { 'name': 'John' }
function Cat() {}
let kitty = new Cat();

kitty.constructor.prototype
{constructor: ƒ}
kitty.__proto__
{constructor: ƒ}
kitty.constructor.prototype === kitty.__proto__
true
kitty.constructor.prototype=== Cat.prototype
true
kitty.__proto__ === Cat.prototype
true

kitty.__proto__.__proto__
{constructor: ƒ, __defineGetter__: ƒ, __defineSetter__: ƒ, hasOwnProperty: ƒ, __lookupGetter__: ƒ, …}
kitty.__proto__.__proto__ === Object.prototype
true
kitty.__proto__.__proto__ === person.__proto__
true

kitty.constructor.prototype=== Cat.prototype
true
kitty.constructor=== Cat
true
Object.getPrototypeOf(kitty)
{constructor: ƒ}
Object.getPrototypeOf(kitty) === Cat.prototype
true

</script>

JavaScript has the built-in Object() function. The typeof operator returns 'function' if you pass the Object function to it. 

Please note that Object() is a function, not an object. It’s confusing if this is the first time you’ve learned about the JavaScript prototype.

Also, JavaScript provides an anonymous object that can be referenced via the prototype property of the Object() function:



The Object.prototype object has some useful properties and methods such as toString() and valueOf().

The Object.prototype also has an important property called **constructor** that references the Object() function.

The following statement confirms that the Object.prototype.constructor property references the Object function:

console.log(Object.prototype.constructor === Object); // true 
kitty.constructor.prototype === kitty.__proto__
