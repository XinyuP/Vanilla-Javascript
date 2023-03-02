https://www.javascripttutorial.net/es6/javascript-class/


ES6 introduced a new syntax for declaring a class as shown in this example:

<script>
class Person {
    constructor(name) { // initialize the properties of an instance
        this.name = name;
    }
    // JavaScript automatically calls the constructor() method when you instantiate an object of the class.
    getName() {
        return this.name;
    }
}


// The following creates a new Person object, which will automatically call the constructor() of the Person class:
let john = new Person("John Doe");


let name = john.getName();
console.log(name); // "John Doe"


///////***** classes are special functions
console.log(typeof Person); // function
console.log(john instanceof Person); // true
console.log(john instanceof Object); // true

</script>


class declarations are not hoisted like function declarations.


<script>
// If you place the following code above the Person class declaration section, you will get a ReferenceError.

let john = new Person("John Doe"); // Uncaught ReferenceError: Person is not defined


// Second, all the code inside a class automatically executes in the strict mode. And you cannot change this behavior.

let john = Person("John Doe"); // Uncaught TypeError: Class constructor Person cannot be invoked without 'new'


</script>



