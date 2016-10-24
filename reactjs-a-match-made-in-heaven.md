#Developing Applications with ClojureScript & [_react.js_](https://github.com/facebook/react)

Clojure lends itself very well to the writing of simple and solid [react.js](https://github.com/facebook/react) wrappers. As a consequence, bootstrapping a full-stack react.js project is as simple as using leiningen:

There are currently three leading clojure react.js wrappers; the way to generate a fully working hello-world project per each is [given here](https://github.com/bhauman/figwheel-template#usage). For example, this leiningen one liner will create a rum project where everything has been taken care of for building, running and deploying the project:

```
lein new figwheel hello-world -- --rum
```

Clojure's react.js wrappers tend to result in more elegant code than you'd get with raw react.js. Of course, you could even suffice with bare-bones ClojureScript to manipulate the DOM by hand; but you know, it's like 2016.
