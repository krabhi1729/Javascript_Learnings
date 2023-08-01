## EXECUTION CONTEXT IN JAVASCRIPT
- Imagine that you are a chef working in a kitchen. The kitchen is like the "execution context" for your cooking activities. In this kitchen, there are two main components: the "memory component" and the "code component."

## 1. Memory Component (Variable Environment):
Think of the memory component as your recipe book and kitchen storage. It contains all the ingredients (variables) and cooking instructions (functions) you need to prepare a dish. Each ingredient (variable) and cooking instruction (function) is stored in the recipe book with a label (variable name) so that you can easily find and use them when needed.
- ### Note:- All the variables and functions in` key value pairs`. It is also called Variable environment.
## 2. Code Component (Thread of Execution):
The code component is like your cooking process. It's where you follow the instructions step-by-step and prepare the dish. You start from the first step, execute it, move on to the next, and so on, until you finish cooking the entire dish.

- Now, let's see how the execution of JavaScript works with this analogy:

1. When you enter the kitchen to cook a dish, a new "execution context" is created, just like your sealed-off container.

2. In this new execution context, JavaScript looks at the recipe book (memory component) to find the variables and functions you'll need for cooking.

3. Then, it follows the cooking instructions (code component) step-by-step, executing one line of code at a time. Each line is like a cooking instruction.

4. As you go through the instructions, you might need to use some ingredients (variables) from the recipe book. You take the required ingredients from the storage and use them accordingly.

5. Once you have executed all the instructions in order, you finish cooking the dish, and the execution context for that specific task is complete.

6. If you have another dish to cook, you'll create a new execution context for that task, just like starting over with a new recipe.

Diagram:

```
   +----------------------------------+
   |         Execution Context        |
   |----------------------------------|
   |                                  |
   |     Memory Component (Variables  |
   |     and Functions)               |
   |     (Your Recipe Book)           |
   |                                  |
   |----------------------------------|
   |                                  |
   |   Code Component (Thread of      |
   |   Execution)                     |
   |   (Your Cooking Process)         |
   |                                  |
   +----------------------------------+
```
- JS is a synchronous, single-threaded language
 - #### Synchronus
   Synchronous refers to the order in which tasks are executed relative to each other.

 - #### Single-threaded language
  Single-threaded refers to the number of execution paths or "lanes" available for processing tasks in a 
  program or language.
   
  
