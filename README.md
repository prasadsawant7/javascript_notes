# JavaScript Notes

# How JavaScript Works?

Everything in JS happens inside an **Execution Context**.

## Execution Context

- Memory Component
    - It contains variable and functions, etc. in key: value pairs.
    - It is also known as **Variable Environment**.
- Code Component
    - It is a place where whole JS code is executed.
    - It is also known as **Thread of Execution**.

| Memory | Code |
| --- | --- |
| key: value | // Code |
| a: 10 (Variables) | // Code |
| fn: {…} | // Code |

<aside>
📌 “JavaScript is a synchronous single-threaded language”

</aside>

> **Synchronous Single-Threaded** means JS can only execute the code in a specific order i.e. JS will execute one line of at a time and after execution of that line then only JS will go to the next line for execution.
> 

# How JavaScript code is executed?

```jsx
1. var n = 2
2. 
3. function sqaure(num) {
4. 	   var ans = num * num
5.		 return ans;
6. }
7. 
8. var sqaure2 = sqaure(n)
9. var sqaure4 = sqaure(4)
```

<aside>
💡 When the code starts the execution, JS engine creates a **Global Execution Context**

</aside>

1. When we will run the above code, the Global Execution Context (GEC) is created.
2. As we studied previously, GEC has two components, such as:
    1. Memory Component
    2. Code Component
3. Global Execution Context is created in two phases:
    1. Memory Creation Phase
    2. Code Execution Phase

> **Memory Creation** phase steps:
> 
> 1. GEC is created
> 2. JS will allocate the memory to variables and function, this process is done in Memory Creation Phase
> 3. Allocation will start from the 1st line, first it’ll allocate memory to variable named as ‘**n’** in the Memory Component of GEC and as we are in the Memory Creation Phase so, JS will assign the value to it as **undefined**. 
>     
>     <aside>
>     💡 **undefined** is a special keyword reserved in JavaScript.
>     
>     </aside>
>     
> 4. As we previously seen, Memory Component stores variable and functions in key: value pairs. So ‘**n**’ variable will store the value undefined as:
>     
>     ```jsx
>     // Memory Component                 // Code Component
>     
>     n: undefined
>     ```
>     
> 5. Then on next line there is one function named as ‘**sqaure**’. So, JS will also store the function sqaure in Memory Component but in case of functions JS will assign the whole function code as value.
>     
>     ```jsx
>     // Memory Component                 // Code Component
>     
>     n: undefined
>     sqaure: {...}
>     // Whole Function Code
>     ```
>     
> 6. After the function, the next two lines there are two variables declared. Similarly to variable ‘**n**’ it will store the variables ‘**sqaure2**’ and ‘**sqaure4**’ in the Memory Component and as in this case both are variables so JS will assign them undefined as value.
>     
>     ```jsx
>     // Memory Component                 // Code Component
>     
>     n: undefined
>     sqaure: {...}
>     // Whole Function Code
>     sqaure2: undefined
>     sqaure4: undefined
>     ```
>     

> **Code Execution** phase steps:
> 
> 1. As we seen before, JS will start the execution line by line and in Code Execution phase every calculation or function calls is done.
> 2. As soon as JS encounters the first line of the code it checks the value of the variable and overwrites the value of the variable in GEC.
>     
>     ```jsx
>     // Memory Component                 // Code Component
>     
>     n: 2
>     sqaure: {...}
>     // Whole Function Code
>     sqaure2: undefined
>     sqaure4: undefined
>     ```
>     
> 3. After completing the above steps, control moves to the next line and encounters that we don’t have anything here to assign any value. That is there no value to assign to the function. So it will move to the next line.
> 4. So in line no. 8 JS encounters the function call/invocation, whenever function is invoked the brand new **Execution Context** is created.
> 5. So in the Code Component of GEC new Execution Context is created for sqaure function call. So again we will again go through the Memory Creation and Code Execution phases.
> 6. Now we are in the Execution Context of sqaure function only, so the phase 1 will start i.e. Memory Creation Phase.
>     
>     > **Memory Creation** phase:
>     > 
>     > 1. As we seen previously memory is allocated to the variables and functions. So, here it will allocate the memory to variables used inside the function and to parameters as well. Here there is no another function inside this function, no memory will be allocated to any function.
>     > 2. So JS will encounter ‘**num’** variable first inside square function and will assign the undefined value to it.
>     >     
>     >     ```jsx
>     >     // Memory Component           // Code Component
>     >     
>     >     num: undefined
>     >     ```
>     >     
>     > 3. Then JS will encounter ‘**ans**’ variable and again it’ll assign the undefined value to it.
>     >     
>     >     ```jsx
>     >     // Memory Component           // Code Component
>     >     
>     >     num: undefined
>     >     ans: undefined
>     >     ```
>     >     
>     
>     > **Code Execution** phase
>     > 
>     > 1. In this phase we will be executing the body of the function.
>     > 2. When the function is invoked the variable ‘**n**’ is passed to variable ‘**num**’. In above code ‘**n**’ is the parameter and ‘**num**’ is the argument. So, now the value of ‘**num’** will be overwritten with value of ‘**n**’ that is 2, because we have passed the ‘**n**’ as argument through the function call.
>     >     
>     >     ```jsx
>     >     // Memory Component           // Code Component
>     >     
>     >     num: 2
>     >     ans: undefined
>     >     ```
>     >     
>     > 3. So now the control have moved to the next line i.e. line no. 4. On this line the calculation will be done i.e. **num** * **num** and the result will be stored in **ans**. **num * num**  this calculation will be done in Code Component and after that the result will be replaced with value of **ans.**
>     >     
>     >     ```jsx
>     >     // Memory Component           // Code Component
>     >     
>     >     num: 2                           num * num | (2 * 2)
>     >     ans: 4
>     >     ```
>     >     
>     > 4. Now the control will be on line no. 5. Now JS will encounter the keyword **return.** return keyword states that return the control of the program where the function was invoked. As in above code the function was invoked on line no. 8, so it will return the value of ans where function was invoked. That means the Code Execution is done for function and the value of ans will be return and assigned to the variable **sqaure2.**
>     >     
>     >     ```jsx
>     >     // Memory Component           // Code Component
>     >     
>     >     num: 2                           return ans
>     >     ans: 4
>     >     ```
>     >     
> 7. So now the function Execution Context has executed the function and returned the value of **ans** to the **sqaure2** variable.
>     
>     ```jsx
>     // Memory Component                 // Code Component
>     
>     n: 2
>     sqaure: {...}
>     // Whole Function Code
>     sqaure2: 4
>     sqaure4: undefined
>     ```
>     
> 8. After returning the value to the **sqaure2** variable the new Execution Context created for function will be completely destroyed. So, there won’t be any Execution Context inside Code Component. Meaning as soon as function is executed and returned the value, the Execution Context created for that particular function will be destroyed.
> 9. Now the control will move to the line no. 9. JS will again encounter the function call, but this time the argument is directly written in the () round brackets instead of passing any variable. So, this the value 4 will be passed as an argument to the **num** parameter i.e. **num** will store the value as 4.
> 10. The most important thing now is that, for the second function call again the brand new **Execution Context** will be created.
>     
>     ```jsx
>     // Memory Component                 // Code Component
>     ```
>     
>     So, now control will again go through the 2 phases such as Memory Creation and Code Execution phases for sqaure function execution.
>     
>     > **Memory Creation Phase**
>     > 
>     > 1. Firstly, the memory is allocated to the **num** and the value will be assigned to it is **undefined**.
>     > 2. Secondly, the memory is allocated to the **ans** and again undefined will be stored in it.
>     >     
>     >     ```jsx
>     >     // Memory Component           // Code Component
>     >     
>     >     num: undefined
>     >     ans: undefined
>     >     ```
>     >     
>     
>     > **Code Execution Phase**
>     > 
>     > 1. Now **num** will get the value 4 from the invokation of function i.e. from line no. 9. Now undefined will be replaced by 4.
>     >     
>     >     ```jsx
>     >     // Memory Component           // Code Component
>     >     
>     >     num: 4
>     >     ans: undefined
>     >     ```
>     >     
>     > 2. Now the control is moved to the next line, now the calculation will be done in Code Component. That means **num * num** will be calculated and stored in **ans** variable by replacing undefined.
>     >     
>     >     ```jsx
>     >     // Memory Component           // Code Component
>     >     
>     >     num: 4                           num * num | (4 * 4)
>     >     ans: 16
>     >     ```
>     >     
>     > 3. Now the control moves to line no. 5. JS will encounter the return statement. So, the control will take back to the line no. 9 and the value of ans will be replaced/overwrite by 16. Meaning the value of **sqaure4** will get updated by 16.
>     >     
>     >     ```jsx
>     >     // Memory Component           // Code Component
>     >     
>     >     num: 4                           return ans
>     >     ans: 16
>     >     ```
>     >     
>     > 4. As soon as the value of **ans** is returned to the **sqaure4** the **Execution Context** for second sqaure function call will be destroyed.
> 11. Now, the value of **sqaure4** is replaced by 16.
>     
>     ```jsx
>     // Memory Component                 // Code Component
>     
>     n: 2
>     sqaure: {...}
>     // Whole Function Code
>     sqaure2: 4
>     sqaure4: 16
>     ```
>     
> 12. Now the line no. 9 is also completely executed, so there is nothing left to execute and program is finished.
> 13. Now the **Global Execution Context** is also deleted/destroyed.

Here we are done with the code, but for the more information. Assume a case where a function is calling another function inside it. Then there would have been main **Global Execution Context** inside it in the Code Component there would have been another new **Execution Context** for 1st function call but now inner function call will also create new Execution Context inside the Code Component of 1st function’s Execution Context. Likewise if there are n number of functions inside one another, then the Execution Context will go deeper. Like this:

```jsx
// Memory Component    // Code Component
                       // Memory Component    // Code Component
                                              // Memory Component    // Code Component
                                                                     // Memory Component    // Code Component
```

But these procedure seems to be very complicated to handle for JS, but JS handles it beautifully. It handles everything from creating the GCE, creating the new Execution Context to deleting every Execution Context.

JS manages everything using a stack, which is usually said as **Call Stack.**

| Call Stack |
| --- |
|  |
|  |
|  |

**Call Stack** is also known as:

1. Execution Context Stack
2. Program Stack
3. Control Stack
4. Runtime Stack
5. Machine Stack

It is similar to Stack which used in DSA. When we run the JS code **GCE** is created and pushed in the **Call Stack.** Everytime we have **Global Execution Context** at the bottom of the stack.

| Call Stack |
| --- |
|  |
|  |
| GEC |

Whenever any function is invoked the new Execution Context is created for it and this newly created Execution Context is pushed inside the Call Stack.

| Call Stack |
| --- |
|  |
| EC1 |
| GEC |

Once we executed the function and returned the value to where the function is invoked then the function is destroyed from the GEC and poped out from Call Stack as well.

| Call Stack |
| --- |
|  |
|  |
| GEC |

Again if there is another or same function in the code is called then again **Execution Context** (EC) will be created and that EC will be pushed inside the **Call Stack.**

| Call Stack |
| --- |
|  |
| EC2 |
| GEC |

Once the second function call is executed the EC for it will be destroyed from GEC and also it will be popped out from the **Call Stack**.

| Call Stack |
| --- |
|  |
|  |
| GEC |

Finally the whole code is executed, now the GEC will be destroyed and popped out from **Call Stack**. Now **Call Stack** is empty.

| Call Stack |
| --- |
|  |
|  |
|  |

Whenever the Execution Stack is created it is pushed inside the Call Stack and whenever it is deleted or destroyed it is popped out from the Call Stack.

<aside>
💡 “**Call Stack** maintains the **order of execution** of **Execution Contexts**”

</aside>
