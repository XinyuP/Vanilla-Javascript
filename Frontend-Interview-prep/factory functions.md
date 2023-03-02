A factory function is a function that returns a new object.

**When a function creates and returns a new object, it is called a factory function.**

https://www.javascripttutorial.net/javascript-factory-functions/


<script>
let person1 = {
  firstName: 'John',
  lastName: 'Doe',
  getFullName() {
    return this.firstName + ' ' + this.lastName;
  },
};

console.log(person1.getFullName());


let person2 = {
  firstName: 'Jane',
  lastName: 'Doe',
  getFullName() {
    return this.firstName + ' ' + this.lastName;
  },
};

console.log(person2.getFullName());

// In this example, the person1 and person2 objects have the same properties and methods.

// The problem is that the more objects you want to create, the more duplicate code you have.

// To avoid copying the same code all over again, you can define a function that creates the person object:


function createPerson(firstName, lastName) {
  return {
    firstName: firstName,
    lastName: lastName,
    getFullName() {
      return firstName + ' ' + lastName;
    },
  };
}
let person1 = createPerson('John', 'Doe');
let person2 = createPerson('Jane', 'Doe');
// The createPerson() is a factory function because it returns a new person object.


// When a function creates and returns a new object, it is called a factory function.

// By using the factory function, you create any number of the person objects without duplicating code.


// A factory function is a function that returns a new object.

// Use Object.create() to create an object using an existing object as a prototype.
