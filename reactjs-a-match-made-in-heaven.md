Clojure lends itself very well to the writing of simple and solid react.js wrappers. As a consequence, bootstrapping a full-stack reactjs project is as simple as using leiningen.

There are currently three leading clojure react.js wrappers; the way to generate a fully working hello-world project per each is given [here](https://github.com/bhauman/figwheel-template#usage). For example, this one liner will create a rum project where everything has been take care of for building, running and deploying the project:

```
lein new figwheel hello-world -- --rum
```

Clojure's react.js wrappers tend to result in more elegant code than you'd get with raw react.js code. Of course, you could also use raw ClojureScript to manipulate the DOM by hand; but you know, it's like 2016.
