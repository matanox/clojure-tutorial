### Anonymous functions
Since so many functions accept functions as their arguments, it is sometimes very convenient and concise to use anonymous functions ― functions defined right where they are needed, for one time use, rather than define them ahead of the expression. In clojure this has the same syntax as a regular function definition, so, if we had the following regular function definition:

```
(def my-function (fn [a b] (* a b)))
```

the anonymous equivalent would be the following:

#### anonymous function definition
```
(fn [a b] (* a b))
```

The result of its application is the same. The only difference is that an anonymous function is defined without tying it to a name. Thus it is more succinct for immediate use as an argument to another function, at the cost of not being reusable from other locations in the code (as there is no name to use for calling it from elsewhere). This is pretty much the same definition for an anonymous function as in mostly any other language. The syntax is simply the same as the case of a regular function definition, sans the `def` constituent.

#### and an alternative shorthand form
The following shorthand form is entirely equivalent to the former one. Use with good taste... e.g. for short, simple, or otherwise adequate cases.
```
#(* %1 %2)
```
