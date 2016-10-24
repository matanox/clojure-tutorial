# Shared Interfaces: clojure's _Protocols_

Clojure provides an abstraction for tying together multiple implementations under a uniform interface.

The clojure api for this sake is called _Protocols_. If the word feels odd on first read, consider that a protocol is an orderly way of defining what can be done between parties, which is entirely close to what a Java interface is. A java interface, like a clojure protocol, provides no implementation. So hopefully you have your mental anchor for the terminology now.

The api for protocols comprises the obviously complementary pieces:

1. Defining a protocol
2. Providing implementations for a protocol
3. Calling functionality through a protocol

A protocol is very much like an interface, but does not have certain limiting properties that e.g. Java interfaces have, or under a different perspective, clojure is just differently opinionated about what interfaces should be like (you can explore the subtle differences [here](http://clojure.org/reference/protocols)). Under the hood, defining a protocol generates a Java interface, and so you may also expose polymorphic functionality to a Java program, an aspect we do not focus on here.

Let us review the api for protocols.

### Defining and Using protocols
A protocol definition simply assigns a set of function signatures, which an implementation must implement, to a name. Here's an example:
```
(defprotocol P1
  (foo [this])
  (bar [this x] [this x y]))
```
This defines a protocol `P1`, which when implemented, has to include an implmentation of _3_ (not two!) functions:
+ a function foo taking a single argument
+ a function bar taking a single argument
+ a function bar taking a two arguments

Now you can define object types that follow this protocol with [deftype](http://clojure.github.io/clojure/clojure.core-api.html#clojure.core/deftype):
```
(deftype MyType [a]
  P1
  (foo [this] a)
  (bar [this x] (* x a))
  (bar [this x y] (* x y a)))

(deftype MyOtherType [a]
  P1
  (foo [this] a)
  (bar [this x] (+ x a))
  (bar [this x y] (+ x y a)))
```
Instantiate objects of these types that implment the `P1` interface:
```
(def object1 (MyType. 1))
(def object2 (MyType. 2))
(def object3 (MyOtherType. 1))
```
And ultimately use collections of them through the common interface:
```
(bar object1 10) ; evaluates to 10
(bar object2 10) ; evaluates to 20
(bar object3 10) ; evaluates to 11

(def my-vec [object1 object2 object3])

(map foo my-vec) ; evaluates to (1 2 1)
```

We used the `map` function here, which takes the sequence `my-vec` and applies the interface function `foo` to all its members. For advanced features of clojure's `map` function you may consult the documentation [here](http://clojuredocs.org/clojure.core/map), but otherwise you do not have to worry about them as it is quite the ordinary map function as in most functional languages.

While the combination of protocols and deftypes provide an excellent way of exposing functionality to a Java or other JVM language, or to model code in a type-laden way, there is nothing to suggest you should use this abstraction for a given model at hand, unless the model you code to really calls for this kind of type-laden abstraction.

In fact, _java interop aside_, you can simply use clojure's dynamic disptach feature ― [multimethods](multimethods.md) ― for quite the same effect, with greater simplicity.
