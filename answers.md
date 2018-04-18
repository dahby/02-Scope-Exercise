#### Questions:
1. When this code is run in Node, e.g. `node index.js`, what are the two stages of execution for this file called, and which order do they happen in?

- The two stages are compilation and execution, and they occur in that order.

2. Write an explanation, using as much space as you need, relating to how the first stage of execution for this file operates.
    - For example, identify the high level steps in a line by line overview and then define what each of those steps are accomplishing.

- During the compilation phase, all variable and function declarations are hoisted and saved in memory. We have not assigned values to the variables as that part comes during the execution phase. foo and bar() are both assigned in memory on the global scope. Within the bar() function, foo is re-declared within the function scope, as well as the function baz() gets declared. foo is once again re-declared within the baz function.

3. Write an explanation, using as much space as you need, relating to how the second stage of execution for this file operates.
    - For example, identify the high level steps in a line by line overview and then define what each of those steps are accomplishing.

- The second stage of execution will actually assign the values to the declared variables in the code. In the global scope, foo is assigned the value of 'bar'. Within the bar() function, foo is re-assigned 'baz', and is again re-assigned 'bam' within the scope of the baz() function. It attempts to assign 'yay' to the variable bam within the baz function, however since bam was never actually declared, this will cause an error. Functions will also be executed during this phase.

4. During the second stage of execution how many scopes have been registered by the engine?
    - Which segments of the code do they belong to?
    - Please identify any variables/refs and which scope each belongs to?

- Three scopes have been registered by the engine: The global scope, the scope within function bar(), and the scope within function baz(). Working outward, baz()'s scope extends from lines 8-12, bar()'s from 5-14, and the global is everything outside of bar() & baz()'s scope. The lines that include baz()'s scope are not included in bar()'s scope. The foo variable belongs to every scope, as it is assigned to 'bar' in the global scope, 'baz' in the bar() scope, and 'bam' in the baz() scope. The other variable assignment, bam is in the baz() scope, however it is not defined where and therefore will throw an error. The function bar() is in the global scope and function baz() within the bar() scope.

5. When line 13 invokes the `baz` function, which `foo` will be assigned a value of `bam`? More specifically, `bam` will be assigned to the `foo` in ??? scope. Give a brief description in your own words to support your conclusion.

- foo is assigned to the value of 'bam' within the baz function, and when the function is run, the assignment will work from the inside out until it finds the variable and assignment. When the function baz() is called, it references the scope of the function and finds that foo is declared and assigned. If it had not found foo within it's scope, it would have moved outward and taken the assignment from the bar() scope, moving to the global scope if not found in bar().

6. Which scope, if any, will the variable `bam` on line 11 be registered to when the first stage of execution occurs on this file? Provide a brief description in your own words to support your conclusion.

- If there had actually been a variable declaration for 'bam', it would have been registered to the baz() scope. However, the first pass-through of the code never establishes bam as a variable in the memory, and therefore will cause an error when the code is run.

7. For each line, 16 through 19, what is the return value for each?

- bar() = undefined
- foo; = 'bar'
- bam; = ReferenceError
- baz() = ReferenceError