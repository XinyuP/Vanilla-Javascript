When the JavaScript engine executes the JavaScript code, it creates the global execution context. The global execution context has two phases:

Creation
Execution
## During the creation phase, the JavaScript engine moves the variable and function declarations to the top of your code. This is known as hoisting in JavaScript.
https://www.javascripttutorial.net/javascript-hoisting/ 





When the JavaScript engine executes the JavaScript code, it creates execution contexts.

Each **execution context** has two phases: the creation phase and the execution phase.
https://www.javascripttutorial.net/javascript-execution-context/

When the JavaScript engine executes a script for the first time, it **creates** the global execution context. During this phase, the JavaScript engine performs the following tasks:

Create the global object i.e., window in the web browser or global in Node.js.
Create the this object and bind it to the global object.
Setup a memory heap for storing variables and function references.
Store the function declarations in the memory heap and variables within the global execution context with the initial values as undefined.

During the **execution** phase, the JavaScript engine executes the code line by line, assigns the values to variables, and executes the function calls.








