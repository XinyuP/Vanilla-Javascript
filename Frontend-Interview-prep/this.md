**this** keyword/variable: 
Special variable that is created for every **execution context** (every function).

Takes the value of (points to) the "owner" of the function in which the this keyword is used.


*this* is NOT static. 
It depends on how the function is called, and its value is only assigned when the 
function is actually called


**Method**: this = <Object that is calling the method>
**Simple function**: this = undefined
**Arrow functions**: this = <this of surrounding function (lexical this)>
    arrow functions do not get their own this keyword 
**Event listener**: this = <DOM element that the handler is attached to>
**new, call, apply, bind** : 






## *this* does NOT point to the function in which we are using 
## also NOT the variable environment of the Function

<script>
// The this Keyword in Practice
console.log(this);

const calcAge = function (birthYear) {
  console.log(2037 - birthYear);
  console.log(this);
};
calcAge(1991);

const calcAgeArrow = birthYear => {
  console.log(2037 - birthYear);
  console.log(this);
};
calcAgeArrow(1980);

const jonas = {
  year: 1991,
  calcAge: function () {
    console.log(this);
    console.log(2037 - this.year);
  },
};
jonas.calcAge();

const matilda = {
  year: 2017,
};

matilda.calcAge = jonas.calcAge;
matilda.calcAge();

const f = jonas.calcAge;
f();
</script>
