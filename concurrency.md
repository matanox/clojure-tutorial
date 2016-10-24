# Concurrency from the first line of code

This is really the sweet spot of clojure, that makes functional programming a winning paradigm for concurrent code; A well-rounded concurrency paradigm.

Note that it is not enough to write concurrency-friendly code; using external libraries, or any Java library in your application, raises the need to analyze and mitigate for concurrency-friendliness, as such external code, especially written in Java, might not be thread-safe. In such cases, you may wrap the external code with the most appropriate clojure concurrency idiom, such that your application remains concurrency-safe. Doing that would be quite straightforward after you have properly befriended clojure's concurrency paradigm.

The core of safe concurrency in clojure, is its system of reference types. We have four reference types in clojure. Think of a reference in clojure as just a reference to a value.

TBC
