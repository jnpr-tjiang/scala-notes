Function and closure
---------------------

**Free variable**

A free variable of an expression is a variable that is used inside the expression but not defined inside the function literal, 
For example, in function literal `x => x + y`, `y` is a free variable

**Bound variable**

A bound variable of an expression is a variable that is both used and defined inside the function literal. 
For example, in function literal `x => x + y`, `x` is a bound variable

**Closure**

A function object that captures free variables, and is said to be “closed” over the variable visible at the time it is created. A function literal without free variable is called *closed term* instead of *closure*. 

Here is a function that creates and returns the “increase” closure:

```
def makeIncreaser(more: Int) = (x: Int) => x + more

val increaseByTen = makeIncreaser(10)
increaseByTen(100) // returns 110
```
