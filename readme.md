# A Clojure Getting Started

### Setup

+ Install clojure  
+ Install leiningen  
+ Install [Light Table](http://lighttable.com/)

Test it all together:

1. Create a clojure project from a template:
   ```
   lein new cljs-kickoff hello
   ```
2. You now have a minimal working project. See [here](https://github.com/konrad-garus/cljs-kickoff#usage) for running it.   
3. Open the project directory in LightTable to see that syntax highlighting and "jump to definition" (ctrl + ">") works.

### Why Clojure

* Cleanest functional language, that can reuse any Java library (now that's a combination!)
* Good concurrency idioms built into the language (much more elegant than Java, even Scala)
* [clojurescript](https://github.com/clojure/clojurescript) is probably the best way for organizing front-end code while elegantly handling events; you simply write clojure for front-end code. No more back-front skill set divide.
* Some other startups use it too, in case you are wondering at this point, and it's a good filter for attitude too!
* For the Scala addict ―  Clojure's concurrency model is way cleaner, well-rounded, and  while at it also more concise

## Down The Rabbit Hole

#### Syntax ― standing on the shoulders of giants ― and the leverage of being simple
Clojure is a LISP variant ― the syntax is a [fully-parenthesized prefix notation](https://www.wikiwand.com/en/Lisp_(programming_language)). While alien at first glance to the non-LISP programmer, this has many benefits, and we do not have to worry about [getting blinds from parentheses](https://www.safaribooksonline.com/library/view/clojure-programming/9781449310387/ch01s04.html).

The building blocks of a clojure program are recursively nested expressions, each expression being a parenthesized list. Within each expression, the first argument is the "what", and the rest of arguments are the "details". This means programs are concise, and uniform. No layers of syntax to learn ― there is no syntax ― only expressions! Further to this _meta-programming_ is natural to the language because being a lisp *code is data*!! this means that macros can easily manipulate code if you ever feel like going DSL, and it is easy to create programs that create programs. now compare that to Scala....

Before going in, note that comments begin with a semicolon (`;`)

So, a function call is written like so:
```
(foo x y) ; call a function foo, x and y being the parameters
```

And surprisingly (but very consistently!) an _if_ statement is written like so:
```
(if (< x y) "yes" "no")) ; evaluates to "yes" if x < y, "no" otherwise
```
