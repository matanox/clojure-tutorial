# Why Immutability?

### understanding first what functional programming really is

The word "Functional" is so trivial and ambiguous, that you might assume you know what the functional programming paradigm is whereas that might be entirely not the case! Functional programming is a mathematical programming paradigm, where we only call and compose functions to each other. Wikipedia says:

> In computer science, functional programming is a programming paradigm—a style of building the structure and elements of computer programs—that treats computation as the evaluation of mathematical functions and avoids changing-state and mutable data.

What the hell does that mean? Well, first of all, functional programming is a paradigm coupled with an abstraction on top low-level programming; just like object-oriented is a paradigm and an abstraction on top low-level programming. Think about it for a moment through the lens of the object-oriented paradigm: our computers have no notion of objects. This could not be stressed more: today's generation of computers aren't object-oriented machines nor functional machines: they hold memory on which a cpu performs operations (give or take input and output devices). Compilers transform the high-level constructs that a higher-level language lets us use, into something that the hardware (or JVM as a proxy) can execute. So then, a functional programming language ― like clojure ― lets us program under a functional programming paradigm. It is an abstraction.

And what does this programming paradigm comprise? In functional programming we have _expressions_ getting evaluated. Our expressions call functions we or others have defined, producing either just values (numbers, strings, etc.) or compound data structures (vectors, sets, maps, etc.) and at times performing side-effects like IO. In a composition of mathematical functions like this, we don't have mutable variables. We only have values being derived from earlier-derived values, which is why immutability is a core in functional programming.

### immutability is natural to FP, and helpful

_It turns out_ that much of our programming can be done the same way ― without modifying variables we've already assigned. This makes thread-safety more inherent in our programs. And why is this helpful?

Imagine a (static) function that does not modify any of its variables nor perform side-effecting operations ― that function is by definition thread-safe. You would not get that if your function were to modify any of its variables (think about it!). Why does this matter so much? because functional programming is all about functions calling functions. If all our functions are so pure, we are, by definition, concurrency-friendly. So immutable programming is a good building block for writing concurrency-friendly applications.

Concurrency is also _somewhat_ easier through immutable programming, by owing to another more benign property: creating a piece of immutable data is an atomic operation ― the data is either in existence and ready for use, or non-existent yet. So two or more threads accessing the same data will always see the same data (thus we get some atomic consistency for free).

### can we really always be immutable?!
No, and we are supposed to use specific abstractions to keep the _mutable parts of our code_ concurrency-friendly. Clojure provides the most magnificent concurrency-preserving abstractions to that end, which you'll read about in the concurrency section. Which is the main sticking point of clojure.

Writing immutable code is just a safe building block to use whenever possible. And there's cases where it's a good idea not to write immutable code. We preserve concurrency-friendliness by wrapping those mutable areas of our code with clojure's concurrency abstractions. This is okay, and if we later find the associated performance penalty bothersome, we can later refactor into immutable code, or conceive a better structure to our program. So as said, immutable code is only a default practice for writing concurrency-safe code, and there's reasons and cases where it should actually be avoided:

### when to be _not immutable_
One major case can be the case of pure algorithms. Many algorithms cannot be implemented with any sense of efficiency in immutable code. Many algorithms do not easily map to scalable tail recursions, and trying to implement them in a functional manner may give one a nice intellectual stimuli ― but result in very inefficient execution compared to a straightforward mutable implementation. So careful discretion (or experience) need be applied, in deciding when to stick to immutability and when not to.

Another motivation to avoid immutability is, in cases where the mental effort of twisting a known algorithm into mutable form stands in your way of coding-efficiency. This goes much beyond laziness: as you are not always sure to begin with, that you may find a tail-recursion for your algorithm, the intellectual drill may simply be _a waste of time_.

As a semi-concrete example, say you have an algorithm which iteratively updates a large data structure in intricate, ways while going over its input. Instantiating a new matrix for each cell-update is simply inefficient compared to updating the matrix in place. So sticking to full immutability is definitely something you would often avoid in the hotspots of your application.

__So do not feel bad for the mutable parts of your code__, but do wrap them the right way as per the concurrency section.
If you've been spoiled by non-functional programming for too long, you'll have to flip your mind the first times. Eventually then, you'll make the trade-offs naturally enough.

## summary

So why does it all matter? Why fuss to think and code immutable? because in today's world we need to write concurrency-friendly programs ― programs that can concurrently execute on multiple cores and threads, programs that need to respond to randomly arriving external events, and programs that need to respond to equally random user events on a UI.

If we stick to immutables in our code, we are safe for concurrency at the micro-level; things will not blow up inside our small pieces when things go concurrent. While we'll be safe at the macro level, owing to the use of the appropriate concurrency idioms described in the [concurrency section](concurrency.md). It's been mentioned so much here that you should probably proceed reading it now!
