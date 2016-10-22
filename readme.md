# A Clojure Getting Started

## Setup

+ Install clojure  
+ Install leiningen  
+ Install [Light Table](http://lighttable.com/)

Test it all together:

1. Create a clojure project from a template:
   ```
   lein new cljs-kickoff hello
   ```

   This template actually just instantiated a full-stack project for you. The server side is clojure, and the front-end side, is ClojureScript ― clojure code that transpiles to javascript.

2. You now have a minimal working project. See [here](https://github.com/konrad-garus/cljs-kickoff#usage) for running it.   

3. Open the project directory in LightTable to see that syntax highlighting and "jump to definition" (ctrl + ">") works.

## Why Clojure

* Cleanest functional language, that can reuse any Java library (now that's a combination!)
* Good concurrency idioms built into the language (much more elegant than Java, even Scala)
* [clojurescript](https://github.com/clojure/clojurescript) is probably the best way for organizing front-end code while elegantly handling events; you simply write clojure for front-end code. No more back-front skill set divide.
* Some other startups use it too, in case you are wondering at this point, and it's a good filter for attitude too!
* For the Scala addict ―  Clojure's concurrency model is way cleaner, well-rounded, and  while at it also more concise

## Down The Rabbit Hole

#### syntax ― standing on the shoulders of giants ― and the leverage of being simple
Clojure is a LISP variant ― the syntax is a [fully-parenthesized prefix notation](https://www.wikiwand.com/en/Lisp_(programming_language)). While alien at first glance to the non-LISP programmer, this has many benefits, and we do not have to worry about [getting blind from parentheses](https://www.safaribooksonline.com/library/view/clojure-programming/9781449310387/ch01s04.html), especially when using LightTable or another clojure coding environment such as CIDER [or others](http://blog.cognitect.com/blog/2016/1/28/state-of-clojure-2015-survey-results).

The building blocks of a clojure program are recursively nested expressions, the most notable and common kind of expressions being a parenthesized list (which we can just call a list expression). Within each list expression, the first argument is the "what", and the rest of arguments are the "details". This means programs are concise, and very uniformly structured compared to other languages. Further to this, _meta-programming_ is natural to the language because clojure code is also clojure data, or put differently the language is [homoiconic](http://blog.muhuk.com/2014/09/28/is_clojure_homoiconic.html#.WAucEnV96kA). This means that macros can easily manipulate code, and it is easy to create programs that create programs. now compare that to Scala....

Before going in, note that comments begin with a semicolon (`;`)

So, a function call is written like so:
```
(foo x y z) ; calls a function foo, x, y and z being the parameters
(bar x y) ; calls a macro bar, x and y being the parameters
```

And surprisingly (but very consistently!) an _if_ statement is written like so:
```
(if (< x y) "yes" "no")) ; evaluates to "yes" if x < y, "no" otherwise
```

#### defining immutable variables

We can define values (a bit confusing but they are called `Vars` in clojure jargon):
```
(def my-val 5)
```

And define functions like so:
```
(def my-function (fn [a b] (* a b)))
(defn my-function [a b] (* ab))      ; shorter form of the same
```

As we discuss in the [namespaces page](namespaces.md), definitions become known inside their namespace or if they have been summoned into the current workspace similar to how imports work in other languages.

#### calling java and javascript

A list expression can also invoke any Java thingy at all, thus letting you fully reuse Java code. While the syntax for that uses the same list syntax where the first list item is the "what" and the others are the arguments, clojure provides equivalent convenience forms per Java interop verb (which are actually implemented under-the-hood as macros).
```
(new classname args)  ; alternatively by sugared form: (Classname. args*)
(. toLowerCase "AAA") ; alternatively by sugared form: (.toLowerCase "AAA")
(. Math sin x)        ; alternatively by sugared form: (Math/sin x)
```

Other than facilitating Java and javascript interop, clojure is not object oriented. Object Orientation is just one way to model the world and clojure provides for a more natural way of managing state, which we will arrive at later. But we can use any Java object as shown above, building on top existing Java libraries.

Similarly to Java interop, when using [clojurescript](https://github.com/clojure/clojurescript), we can also use javascript native functions and javascript libraries. For example:
```
(.log js/console "Hello World!") ; accessing stuff available in javascript global scope
(js/console.log "Hello World!")  ; same, using further-sugared form
```

#### defining data structures

Apart from list expressions denoting calls and Java invocations (as just discussed), clojure has syntax for data structures, as follows. These are the basic data structures that you have and use in clojure. You can read about their data access performance characteristics over the Internet, but basically you'd not bump into special surprises if these types sound familiar:

```
`(1 2 3)              ; a list ― will not be interpreted as a call thanks to the quote escaping
[1 2 3]               ; a vector (more or less, the equivalent of a Java array)
#{1 2 3}              ; a set
{:foo "bar" :count 3) ; a keyed map (keys are colon-prefixed and called "keywords" in clojure)
```

You can easily find functions built into clojure which operate on these data types in the documentation or in examples. You manipulate data by deriving new data from it, not by mutating it! if this is your first time bumping into immutability, take a read about functional programming. You can however, at the cost of dropping the concurrency safety of immutable programming, turn a given data into a mutable one ― and even very elegantly so ― [see here](https://clojuredocs.org/clojure.core/transient). Of course you'll have to reason about conurrency considerations on your own then, isolating the involved code for concurrency safety.

As mentioned inline the list data type must be prefixed with a quote (') to differentiate from a call expression. Without the escaping a list will be (as broadly shown above) interpreted as a call expression, with the quote, it will be interpreted as a data literal.

#### playing around

We need to see some examples of nested expressions and real programs, and augment with the special forms that augment the list expression syntax. But first, play around with the above code lines in a clojure REPL. The REPL is just a console environment where you can evaluate (clojure) expressions before putting them into a source file (as well as you can import modules of your project into the repl and play with them there). Fire up a REPL session by running:

```
lein repl
```

And explore some of the clojure expressions given on this page..... each expression you enter will be evaluated, and variables and functions defined by you are remembered for the duration of your session!

What else should we do before going next to learn how to write real programs? Observe that you have a _clojure.clj_ file in the root directory of the project you generated above. It was auto-generated by the template which you used (`lein new cljs-kickoff hello`). This file is much like a build definition; it enables leiningen compiling, running and bundling your project for deployment.

#### so what's leiningen again?
Leiningen is _the_ tool for creating and managing clojure projects. It compiles your clojure code, transpiles your ClojureScript code (if you bootstrapped from a ClojureScript template) and does many other things which in other languages (notoriously Java) you'd need external tools for. Its plugin architecture lets you use elegant things like [figwheel](https://github.com/bhauman/lein-figwheel) for hacking on your full-stack ClojureScript projects.
