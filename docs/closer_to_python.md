Brainstorming: Closer to python
===============================

This snippet

```
def method(a, b, c):
    return a + b + c
```

basically defines a function `method` which takes three arguments in python. But one could also interpret it as a function which takes one 3-tuple as argument.
This might have interesting consequences for ex.:

```
def method2(a):
    return a**2
```

has some unnecessary paranthesis which we could strip:

```
def method2 a:
    return a**2
```

and on a higher level, we could interpret the `def` keyword as `Identifier -*> arg -> Colon -> body -> Function`
