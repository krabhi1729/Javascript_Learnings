# Shortest JS Program, window & this keyword

`Shortest JS Program`:
The shortest JS program is empty file. Because even then, JS engine does a lot of things. As always, even in this case, it creates the GEC which has memory space and the execution context, which is like a workspace where your code can run. This workspace has memory and settings for your program.

`window Object:`
The window object is a special object that gets created automatically when your JS code runs in a browser. It's like a big container that holds many functions and pieces of information that your program can use. Think of it as a toolbox with tools (functions) and drawers (variables) that you can access from anywhere in your program.

`this Keyword:`
The this keyword is like a reference to the current object that your code is working with. At the global level (outside of any functions), this points to the window object. Imagine you're in a big room (the program), and you point to something in that room (using this).

So, when you run even a simple program like this:

```javascript
var x = 10;
console.log(x);          // Output: 10
console.log(this.x);     // Output: 10
console.log(window.x);   // Output: 10
```
Here's what's happening:

`var x = 10`;: You're creating a variable x and assigning the value 10 to it. Since it's created at the global level, it's attached to the window object like a drawer labeled "x" in your toolbox.

`console.log(x)`;: You're asking to print the value of x, which is 10. Since x is attached to the window object, you can access it directly.

`console.log(this.x)`;: Here, you're using the this keyword to point to the window object and then asking to print the value of x. It's the same as the previous line.

`console.log(window.x)`;: This line directly asks to print the value of x from the window object.

