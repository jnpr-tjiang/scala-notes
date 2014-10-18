Scala <=> Java cheatsheet
-------------------------

**Repeated function parameters**

java: `public void foo(String ... args)`

scala: `def foo(args: String*)`

Type class
----------

**Private primary constructor**
```
class Device private (
  private val id: Int,
  private val domainId: Int
)
```
Private constructor can only be accessed within the class or its companion class
```
object Device {
  def apply(id: Int, domainId: Int) = new Device(id, domainId)
}
```

Function and Closure
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
