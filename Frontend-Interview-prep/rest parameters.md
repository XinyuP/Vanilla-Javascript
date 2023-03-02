everything in JS happens inside the **execution context**


JS is a synchronous single-threaded language
can only execute one command at a time in a specific order


arrow functions don't have their own *this*
also don't have the special *argument* object either 


##... is either Rest parameters or spread syntax
**Rest parameters**: get an array from the list of parameters
    sum(...args) --->  for (let arg of args) sum += arg
    sum(1,2,3) --> sum([1,2,3])

**spread syntax**: (does the opposite to rest) expands an iterable object into the list of argument 
    arr1 = [1,2,3]
    arr2 = [4,5,6]
    Math.max(...arg1, ...arg2) -->  Math.max(1,2,3,4,5,6)

    str = "hello"
    [...str]               =====          Array.from(str)  
works only with iterables             both array-likes and iterables

copy an array:
    let arrCopy = [...arr]  === let arrCopy = Object.assign([], arr)
copy an pbject:
    let objCopy = [...obj]  === let objCopy = Object.assign({}, arr)






