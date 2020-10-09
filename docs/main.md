# Bagheera

A mix between Python and Elm, incorporating some sprinkles of Idris build upon LLVM. Eventually. For now there is only the language reference.

Some examples: 

Hello World: 

```
module Example exposing (helloWorld)

include Bagheera.Typing exposing (signature as sig)

helloWorld : String -> IO ()  #Alias for @sig <| String -> IO ()
helloWorld name = 
  print <| "Hello, " ++ name ++ "!"
```

Each first class citizen has the common python magic attributes:
```__repr__, __str__, __contains__, __iter__```


Contract: (TODO)


```
module Example.Binsearch exposing (search)

include Bagheera.Contracts exposing (pre,post,inv)

@pre isSorted a
search : {a = List (Comparable m)} -> Maybe m
search [] = Nothing
search [x] = Just x

isSorted : List m -> Proof (\ x y -> (List.indexOf x m) < (List.indexOf y m) |- (x <= y)
isSorted [].
isSorted [x].
isSorted [x]+[y]+z :- x <= y, isSorted [y]+z.
```
