Writing good function prototypes is mostly about the flexibilities of argument passing ― things like being able to use optional parameters, default values, etc, and it's therefore essential to master defining and passing function parameters to the level of a natural fluency. Without further ado:

A functions argument list is defined as a vector.

Inside the vector we can place names for the arguments (no types are specified, clojure is not type safe; another reason to use unit tests). E.g.

```
[x y z]
```

To define optional arguments:
```
```

Defining default values to arguments:
```
```
