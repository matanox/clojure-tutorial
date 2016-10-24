# Anonymous Functions
Since so many functions accept functions as their arguments, it is also convenient and concise to have anonymous functions ― functions defined right where they are needed, for one time use, rather than defined them ahead of the expression. So, if we had the following function definition, one that gives a name to the function:

```
(def my-function (fn [a b] (* a b)))
```

the anonymous equivalent of the same function would simply be:

#### anonymous function definition
```
(fn [a b] (* a b))
```

The only difference is that an anonymous function is defined without tying it to a name, and that it can be located in argument position. Thus it is more succinct for immediate use as an argument to another function, at the cost of not being reusable from other locations in the code (as there is no name to use for calling it from elsewhere). This is pretty much the same definition for an anonymous function as in mostly any other language. The syntax is simply the same as the case of a regular function definition, only without the `def` constituent.

#### and an alternative shorthand form
The following shorthand form is entirely equivalent to the former one. Use with good taste... e.g. for short, simple, or otherwise adequate cases.
```
#(* %1 %2)
```
It is shorter as it skips letting you specify names for the arguments, assigning the preset names %1, %2 .... %n, for you to access arguments in the function's body. (and you may also use `#&` for "rest of args").
