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
    
     Take a look at the code, do you find the comments necessary?
     ```python
     def read(self, objs, time_acc):
        ''' generate lidar scan from obj '''
        # find visible edges of objs
        visible_edges = self.find_visible_edges(objs)
        # generate scan from edges
        sensor_data = self.find_scan(visible_edges)
     ```
   - Local variables should be defined close to where they are going to be used.
   - Short names for local variables, long "camelCase" names are hard to read as well.
   - Do not reuse local variables, use multiple instead.
   - Create functions for complex logic.
     I wrote below in one line
     ```cpp
     if ((reversedNumber > INT_MAX / 10) || (reversedNumber < INT_MIN / 10))
     ```
     but for complex case where we need more condition, a function is created.
     ```cpp
     bool willMultiplyOverflow(int num1, int num2)
     {
         if (((num1 == -1) && (INT_MIN == num2)) ||
             ((num2 == -1) && (INT_MIN == num1)) ||
             (num1 > INT_MAX / num2) ||
             (num1 < INT_MIN / num2)) {
             return true;
         }
         else {
             return false;
         }
         
     }

     ...
     int reverse (int x) {
         ...
         if (willMultiplyOverflow(reversedNumber, 10))
         ...
     }
     
     ```
   - Simplify complex expressions using intermedia variables.
   - Break the code at proper place.<br/>
     This pattern is often seen in function calls, complex logic expressions and text formatting.<br/>
     code example can check the if condition part in the function 'willMultiplyOverflow' above.
   - Comments:
     - It is generally true that we use verbs for method names, like find, get, compute, generate.
       - Use get if it is there, or super fast. 
       - Use find if it requires a requires computetaion.
       - Compute, generate, calculate are fine, but just too long.
       - math libraries often do not use get or find and they are fine, cause no attribute is called np.sqrt().
       - <https://stackoverflow.com/questions/7151418/determining-which-verb-to-use-for-method-names-in-java>
       - <https://softwareengineering.stackexchange.com/questions/182113/how-and-why-to-decide-between-naming-methods-with-get-and-find-prefixes>
   
5. Write simple code
   - Avoid ++i, i++, use i++ only in for loop update or where it is a single line.
   - __never save the \{\}__, like after if in C++.
   - Use parenthethsis to make expressions clear, especially for logic expressions.
   - __Avoid continue and break in loops__.<br/>
     Because they separate stop loop conditions and delayed the consequences. Using return statements, or put conditions together instead.

6. Write direct code
   - Avoid using "&&" or "||" to replace "if" and "else".

7. Write Robust code
   - __Write "else" where there is an "if"__, don't be lazy, be clear.
     I would usually write code this way
     ```cpp
     int positive = x;
     if (sign == false) {
         positive = -x;
     }
     ```
     this looks shorter, but logically is not a good habit. I wrote like below instead
     ```cpp
     int positive;
        
     if (sign == false) {
         positive = -x;
     }
     else {
         positive = x;
     }
     ```

   - Only write complex features in simple context.
     - list comprehension in python
     - A?B:C; in C++

8. Handle error in a correct way
   - You must handle the error.
   - Code inside try block should be simple and easy to locate error.<br/>
     Note that this is a failed example because arithmetic in C++ don't throw overflow exception, but the idea is that we should not put the while expression inside try, but instead put only the part that has the error that you care about, so that it is easy to locate the error.
     ```cpp
     while (x != 0)
     {
         int digit = x % 10;
         x = x / 10;
 
         try {
             reversedNumber = reversedNumber * 10 + digit;
         }
         catch(const runtime_error& e) {
             std::cerr << e.what() << '\n';
             return 0;
         }
     }
     ```
   - Catch specific exception, don't catch the exception that you are not going to handle.

9. Handle null pointer in a correct way
   - Don't accept null pointer as parameter, throw an exception.

10. Avoid over engineering
    - Solve current problem, then think about extending.<br/>
      Think about how you get stuck by the [pycar (private)](https://github.com/henryzhangzhy/pycar) or [pykffusion](https://github.com/henryzhangzhy/pykffusion) when you are thinking about extensibility and reusability. :)
    - Write correct code first, refine it, then think about reusability.
    - Write code that there is obviously no bug, then think about testing.<br/>
      My [python_testing](https://github.com/henryzhangzhy/python_learn/tree/master/python_testing) gets hurt! :)




