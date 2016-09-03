#Name Spaces

If we had all our program symbols stuffed in one big name space, we'd not be able getting anything done. Even if your own program is small, just think about importing libraries that bring their own myriads of symbols into scope.

Clojure lets you elegantly manage your name space to avoid symbol name collisions. The only sucky part is that a name space must sit in a single source file (no idea why, probably the compilation process lacks some sophistication).

Other than that it's quite elegant though, so lets dive in.
