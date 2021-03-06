Scala <=> Java cheatsheet
-------------------------

**Repeated function parameters**

java: `public void foo(String ... args)`

scala: `def foo(args: String*)`

To pass a list or array or other collection to `foo()`, scala supports a special syntax `list: _*`
```
scala> def echo(args: String*) = for (arg <- args) println(arg)
scala> val list = List("Hello", "world")
scala> echo(list: _*)
```

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

A function object that captures free variables, and is said to be **closed** over the variable visible at the time it is created. A function literal without free variable is called *closed term* instead of *closure*. 

Here is a function that creates and returns the **increaser** closure:

```
def makeIncreaser(more: Int) = (x: Int) => x + more

val increaseByTen = makeIncreaser(10)
increaseByTen(100) // returns 110
```
**Named argments**
```
scala> def speed(distance: Float, time: Float): Float = distance / time
scala> speed(time = 100, distance = 300)
```
Named arguments allows you to pass arguments to a function in any order

**Defaults for function arguments**
```
scala> def speed(distance: Float = 100, time: Float): Float = distance / time
```

**Tail recursion**

A function is tail recursive if the only place the function calls itself is the last operation of the function.
```
def approximate(guess: Double): Double = 
  if (isGoodEnough(guess) guess
  else approximate(improve(guss))
```

**By-name Parameter**

When a function parameter is given a type starting with `=>`, it is called *by-name parameter*
```
def byNameAssert(implicit assertionEnabled: Boolean)(predicate: => Boolean) = 
  if (assertionEnabled && !predicate())
    throw new AssertionError
    
byNameAssert(5 > 3)
```
------------------