---
author: Henry
topic: Greek
comments: true
---

Notes on the nice post [programming philosophy](https://www.yinwang.org/blog-cn/2015/11/21/programming-philosophy) by [YinWang](https://www.yinwang.org/).

1. Refine your code again and again.

   It is not about how many lines of code, but how much you think.<br/>
   Comments: I don't do this after I finish writing the code. Let's get started!

2. Write elegant code.

   Beautiful code looks like blocks in clear structure.<br/>
   Comments: It is definitely true! I will try to do thik in my code. 
  
3. Modulize the code.
   - Break code into functions within 40 lines (an area that your eyes can catch all at once).
   - Create small helper functions.
   - Simplify the functions.
   - Avoid using global variables and __class members to pass information__.<br/>
     I made this mistake in my recent project, where I used class members and think that it simplifies the interface.

4. Write readable code.

   Comments might not be necessary.<br/>
   - Use meaningful names for functions and variables, they speak for the comments.
   - Local variables should be defined close to where they are going to be used.
   - Short names for local variables, long "camelCase" names are hard to read as well.
   - Do not reuse local variables, use multiple instead.
   - Create functions for complex logic.
   - Simplify complex expressions using intermedia variables.
   - Break the code at proper place.<br/>
     This pattern is often seen in function calls, complex logic expressions and text formatting.
   
5. Write simple code
   - Avoid ++i, i++, use i++ only in for loop update or where it is a single line.
   - __never save the \{\}__, like after if in C++.
   - Use parenthethsis to make expressions clear, especially for logic expressions.
   - __Avoid continue and break in loops__.

6. Write direct code
   - Avoid using "&&" or "||" to replace "if" and "else".

7. Write Robust code
   - __Write "else" where there is an "if"__, don't be lazy, be clear.
   - Only write complex features in simple context.
     - list comprehension in python
     - A?B:C; in C++

8. Handle error in a correct way
   - You must handle the error.
   - Code inside try block should be simple and easy to locate error.
   - Catch specific exception, don't catch the exception that you are not going to handle.

9. Handle null pointer in a correct way
   - Don't accept null pointer as parameter, throw an exception.

10. Avoid over engineering
    - Solve current problem, then think about extending.
    - Write correct code first, refine it, then think about reusability.
    - Write code that there is obviously no bug, then think about testing.




