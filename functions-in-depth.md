# Using and defining functions like a boss

In any language, but especially in a functional one, it is essential to know the variety of ways of defining and using functions, as you'll want to be as flexible as your thought in defining and using functions, as well as understand all kinds of function calls you'll be reading in other people's code. Things like default argument values, anonymous functions, etc. Here's a hopefully inclusive guide.

## argument passing and retrieval
Writing good function prototypes is mostly about the flexibilities of argument passing ― things like being able to use optional parameters, default values, etc, and it's therefore essential to master defining and passing function parameters to the level of a natural fluency.

### multiple arities and default values
Like most languages, in clojure we are free to define multiple functions of the same name yet accepting a different argument list each. We need to do that within a single list expression, rather than make every function definition its own expression. Here's an example:

```
(defn foo
  ([x]
    (* x x))
  ([x y]
    (* x y)))
```

What we have there is a definition of a function `foo` that takes two implementations; one implementation accepting just one argument `x` and the other taking two arguments `x` _and_ `y`. This also paves the way for default values for arguments. For example, here's a function that takes two arguments whereas the default value for the second argument is `1`.
```
(defn bar
  ([x y]
    (* x y))
  ([x]
    (bar x 1)))

(bar 3 2) ; evaluates to 6
(bar 3) ; evaluates to 3
```

### optional arguments, and functions with unbounded argument arity
It is often the case that optional arguments should be permitted ― arguments which may optionally be allowed for the caller to use. It's a little different than omitting a given required argument like we've shown that default values allow [above](#multiple-arities-and-default-values), if only because default values assume there's a finite set of arguments. Functions admitting an unbounded variable number of arguments fit this role. For example:
```
(defn f1
  [x & options]
  (println (if (> (count options) 0) (str "options supplied: " options) "no options supplied")))

(defn f2
  [& args]
  (println (str args))) ; the function `str` uses the same mechanism itself
```

## dynamic function dispatch
This is like [multi-arity functions](#multiple-arities-and-default-values) on steroids, and in case until now you've only witnessed multiple-dispatch exclusively in Object Oriented languages, this would remind you of how method calling is resolved in those languages. Whereas in OOP languages you would dispatch a method based on the type of an object ― in clojure the capability for dynamic-dispatch of functions is by far generalized through the [multimethod](multimethods.md) abstraction. Of course, you could simply branch per your arguments within a single function rather than use that abstraction, but in other, arguably more complex cases, using the _multimethod_ abstraction might seem to echo a better mental model for your code.
