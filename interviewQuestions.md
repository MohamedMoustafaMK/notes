
# JS Interview Questions
## 𝟏-𝟏𝟎: 𝐁𝐚𝐬𝐢𝐜𝐬 𝐨𝐟 𝐉𝐚𝐯𝐚𝐒𝐜𝐫𝐢𝐩𝐭
1. **What is JavaScript?**
   JavaScript is a high-level, interpreted programming language primarily used for creating interactive and dynamic web pages. It is widely used for both client-side and server-side development.

2. **Explain the difference between let, const, and var.**
   - `let` and `const` were introduced in ES6, while `var` has been part of JavaScript since its early versions.
   - `let` allows you to declare block-scoped variables that can be reassigned.
   - `const` allows you to declare variables with constant values that cannot be reassigned. However, the value itself is not immutable if it's an object or array.
   - `var` declares variables with function or global scope and can be reassigned.

3. **How does hoisting work in JavaScript?**
   Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their containing scope during the compile phase. However, only the declarations are hoisted, not the initializations.

4. **Describe the concept of closures.**
   Closures occur when a function is able to remember and access its lexical scope even when that function is executing outside its original scope. This allows for creating private variables and functions in JavaScript.

5. **Explain the event loop in JavaScript.**
   The event loop is the mechanism in JavaScript that allows asynchronous tasks to be executed in a non-blocking manner. It continuously checks the call stack and the task queue. When the call stack is empty, it takes the first task from the queue and pushes it onto the stack for execution.

6. **What is the difference between == = and ===?**
   - `==` is the equality operator that performs type coercion, meaning it converts the operands to the same type before comparison.
   - `===` is the strict equality operator that checks both the value and the type of the operands without performing type coercion.

7. **How do you check the type of a variable in JavaScript?**
   You can use the `typeof` operator to check the data type of a variable. It returns a string indicating the type of the operand.

8. **What is the use of the this keyword in JavaScript?**
   The `this` keyword in JavaScript refers to the context within which a function is executed. Its value depends on how the function is called. In global scope, `this` refers to the global object (e.g., `window` in browsers), while inside a function, it refers to the object that invoked the function.

9. **Explain the difference between function declaration and function expression.**
   - Function Declaration: Declares a named function using the `function` keyword. Function declarations are hoisted.
   - Function Expression: Defines a function as part of an expression. They can be named or anonymous and are not hoisted.

10. **How does the setTimeout function work?**
    `setTimeout` is a function in JavaScript used to execute a function or a piece of code after a specified delay. It takes two parameters: a callback function or a piece of code to execute, and the delay in milliseconds before the execution. It returns a timer ID that can be used to cancel the execution using `clearTimeout`.


## 𝟏𝟏-𝟐𝟎: 𝐅𝐮𝐧𝐜𝐭𝐢𝐨𝐧𝐬 𝐚𝐧𝐝 𝐒𝐜𝐨𝐩𝐞

11. **What is a callback function?**
   A callback function is a function passed as an argument to another function, which is then invoked inside the outer function to complete some kind of action or operation. Callback functions are commonly used in asynchronous programming to handle tasks like event handling, timers, and AJAX requests.

12. **Explain the concept of a pure function.**
   A pure function is a function that:
   - Always returns the same output given the same input.
   - Has no side effects, meaning it doesn't modify variables outside its scope or interact with the external world.
   Pure functions are deterministic and easier to reason about, making code more predictable and maintainable.

13. **Describe the differences between function.call, function.apply, and function.bind.**
   - `function.call`: Invokes the function with a specified `this` value and arguments passed individually.
   - `function.apply`: Invokes the function with a specified `this` value and arguments passed as an array.
   - `function.bind`: Returns a new function with a specified `this` value and, optionally, initial arguments. It doesn't invoke the function immediately but can be invoked later.

14. **What is the purpose of the arguments object in a function?**
   The `arguments` object is an array-like object available inside functions that contain the values of the arguments passed to the function. It allows functions to work with variable numbers of arguments.

15. **How do you create a closure in JavaScript?**
   A closure is created when a function accesses variables from its outer scope, even after the outer function has finished executing. To create a closure, you need to define a function inside another function and have the inner function reference variables from the outer function's scope.

16. **What is the use of the bind method?**
   The `bind` method in JavaScript is used to create a new function with a specified `this` value and, optionally, initial arguments. It allows you to permanently bind a function to a specific context, which can be useful in event handling or when passing functions as callbacks.

17. **What is the difference between a shallow copy and a deep copy?**
   - Shallow copy: Copies the references to the original objects, so changes to nested objects are reflected in both copies.
   - Deep copy: Creates new copies of all nested objects, ensuring changes to nested objects in the copy don't affect the original objects.

18. **How does the call stack work in JavaScript?**
   The call stack in JavaScript is a data structure that records function calls made during the execution of a program. When a function is called, a new frame is pushed onto the stack, and when the function returns, its frame is popped off the stack. This process continues until all functions have been executed.

19. **Explain the concept of function currying.**
   Function currying is a technique in functional programming where a function with multiple arguments is transformed into a sequence of nested functions, each taking a single argument. This allows for partial application of the function, enabling more flexible and reusable code.

20. **How can you avoid callback hell in JavaScript?**
   Callback hell refers to the situation where multiple nested callback functions make the code difficult to read and maintain. To avoid callback hell, you can use techniques like modularization, Promises, async/await, or libraries like RxJS for reactive programming. These approaches help organize asynchronous code and make it more manageable.

## 𝟐𝟏-𝟑𝟎: 𝐎𝐛𝐣𝐞𝐜𝐭𝐬 𝐚𝐧𝐝 𝐏𝐫𝐨𝐭𝐨𝐭𝐲𝐩𝐞𝐬

21. **What is prototypal inheritance?**
   Prototypal inheritance is a feature of JavaScript where objects can inherit properties and methods from other objects. Each object in JavaScript has a prototype object, and when a property or method is accessed on an object, JavaScript first checks the object itself and then its prototype chain for the property or method.

22. **How do you create an object in JavaScript?**
   There are multiple ways to create objects in JavaScript:
   - Using object literal notation: `let obj = {}`
   - Using the `new` keyword with a constructor function: `let obj = new Object()`
   - Using Object.create(): `let obj = Object.create(proto)`

23. **What is the purpose of the prototype property in JavaScript?**
   The `prototype` property is used in constructor functions to add properties and methods to all instances created with that constructor. It allows for the implementation of inheritance and sharing of behavior among objects.

24. **Explain the difference between Object.create and the constructor pattern.**
   - `Object.create(proto)`: Creates a new object with the specified prototype object.
   - Constructor pattern: Involves defining a function that serves as a constructor for creating objects. Instances created with the constructor function inherit properties and methods from its prototype.

25. **How do you add a property to an object in JavaScript?**
   You can add a property to an object by simply assigning a value to a new or existing property key: `obj.property = value`.

26. **What is the hasOwnProperty method used for?**
   The `hasOwnProperty` method is used to check if an object has a property with a specific key. It returns a boolean value indicating whether the object has the property as its own property, rather than inherited from its prototype chain.

27. **How can you prevent modification of object properties in JavaScript?**
   You can prevent modification of object properties in JavaScript using:
   - Object.freeze(): Prevents adding, deleting, or modifying properties of an object.
   - Object.seal(): Prevents adding or deleting properties, but allows modifying existing properties.
   - Object.preventExtensions(): Prevents adding new properties to an object.

28. **Describe the use of the new keyword.**
   The `new` keyword in JavaScript is used to create instances of constructor functions. When `new` is used with a constructor function, it creates a new object, sets the constructor's prototype as the prototype of the new object, and invokes the constructor function with `this` referring to the newly created object.

29. **Explain the concept of Object Destructuring in JavaScript.**
   Object destructuring is a feature in JavaScript that allows you to extract multiple properties from an object and assign them to variables in a single statement. It provides a concise way to extract and use properties from objects.

30. **What is the difference between null and undefined?**
   - `null`: Represents the intentional absence of any object value. It is a primitive value and can be assigned to variables to explicitly indicate "no value."
   - `undefined`: Represents the absence of a value in variables that have not been assigned a value or in properties that do not exist in an object. It is also a primitive value.

## 𝟑𝟏-𝟒𝟎: 𝐃𝐎𝐌 𝐌𝐚𝐧𝐢𝐩𝐮𝐥𝐚𝐭𝐢𝐨𝐧 𝐚𝐧𝐝 𝐄𝐯𝐞𝐧𝐭𝐬


31. **What is the DOM?**
   The DOM (Document Object Model) is a programming interface for web documents. It represents the structure of HTML and XML documents as a tree-like structure where each node represents an element, attribute, or text in the document. The DOM provides a way for scripts to dynamically access and manipulate the content, structure, and style of a web page.

32. **How do you select elements with Vanilla JavaScript?**
   You can select elements using various methods such as:
   - `document.getElementById()`
   - `document.querySelector()`
   - `document.querySelectorAll()`
   - `document.getElementsByTagName()`
   - `document.getElementsByClassName()`
   
33. **Explain event delegation in JavaScript.**
   Event delegation is a technique in JavaScript where you attach an event listener to a parent element instead of individual child elements. This allows you to handle events on multiple child elements with a single event listener, improving performance and reducing memory usage.

34. **What is the purpose of the addEventListener method?**
   The `addEventListener` method is used to attach an event listener to an HTML element. It takes two arguments: the type of event to listen for (e.g., 'click', 'mouseover') and a callback function to execute when the event occurs. It allows for handling multiple events of the same type on a single element and supports event delegation.

35. **How do you create and remove elements in the DOM?**
   - To create elements, you can use methods like `document.createElement()` and `element.appendChild()`.
   - To remove elements, you can use methods like `element.parentNode.removeChild()` or `element.remove()`.

36. **Explain the concept of event propagation.**
   Event propagation refers to the process by which an event is dispatched and delivered to event listeners in the DOM tree. There are two phases of event propagation: capturing phase and bubbling phase. During the capturing phase, the event is dispatched from the root of the tree to the target element. During the bubbling phase, the event bubbles up from the target element to the root of the tree.

37. **How can you prevent the default behavior of an event?**
   You can prevent the default behavior of an event using the `preventDefault()` method on the event object. This method must be called within the event listener function and prevents the default action associated with the event from occurring.

38. **What is the purpose of the data- attribute in HTML?**
   The `data-` attribute in HTML is used to store custom data attributes associated with an element. It allows you to store extra information that is not directly visible to users but can be used by scripts or CSS.

39. **Describe the difference between innerHTML and textContent.**
   - `innerHTML`: Property of an element that represents the HTML content inside the element, including any HTML tags. It can be used to get or set the HTML content of an element.
   - `textContent`: Property of an element that represents the text content inside the element, without interpreting any HTML tags. It only deals with text content and is often preferred when you want to avoid any potential security risks associated with injecting HTML.

40. **How do you handle asynchronous code in JavaScript?**
   Asynchronous code in JavaScript can be handled using techniques such as callbacks, Promises, async/await, and event listeners. Callbacks are the traditional way of handling asynchronous operations, while Promises provide a cleaner and more structured approach. Async/await is a modern syntax that allows for writing asynchronous code in a synchronous style. Event listeners are commonly used for handling asynchronous events such as user input or network requests.