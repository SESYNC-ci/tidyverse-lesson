---
---

## Defining a function

We already saw examples of a few built-in functions, such as `type()` or `len()`.
You can define your own Python functions as a block of code starting with a `def`
statement.


~~~python
>>> def add_2(num):
...     result = num + 2
...     return result
...
>>> add_2(10)
12

~~~
{:.term}



===

The `def` keyword is followed by the function name, its arguments enclosed in
parentheses (separated by commas if there are more than one), and a colon. The
`return` statement passes the specified result as the output of the function. 
A simple `return` line with no output value just exits the function.

After it is defined, the function is invoked using its name and specifying the
arguments in parentheses, in the same order as in its definition.

===

**Exercise**: Create a function that takes a list as an argument and returns
its first and last elements as a new list.