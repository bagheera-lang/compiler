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

Each first class citizen has the common python magic attributes. These can be overwritten/implemented typewise as follows:
```
type alias B e = 
  { amount : Int
  , owner : e
  }

(B e).__init__ : Int -> e -> B e
(B e).__repr__ : B e -> String
(B e).__str__ : B e -> String
(B e).__contains__: B e -> e -> Maybe e
(B e).__iter__ : B e -> Iterable e
B e |> . __repr__  = (B e).__repr__ 
```
Each instance of a type has these variables preset but may also overwrite them:

```
updateView : B e -> B e
updateView old = 
  { old | __str__ = 
    case (B e).__str__ :
      Just f ->
        \x -> f x + " made by me"
      Nothing ->
        Nothing
  }
```
additionally:
```
for i in b:
  i^2
```
will be translated into
```
map (\i -> i^2) (b.__iter__ b)
```
but 
```
if i in b:
  doStuff
```
will become
```
if b.__contains__ i:
  doStuff
```
and finally 
```
case b[i]:
  Nothing ->
    someStuff
  Just v ->
    someOtherStuff v
```
will become
```
case b.__contains__ i:
  ...
```
Init fun. Usually, it is not necessary to overwrite Init as it will be prepopulated by the `type ...` declaration. It gathers all functions and
```
(B e).__init__ : Int -> e -> B e
(B e).__init__ amount owner =
  let
    fullB = (B e).__new__ amount owner
  in
    { fullB | __str__ = Nothing }
```
makes this instance not displayable.
Note: The Signature of `type ...` an `__new__` have to match, but `__init__` is not bound to that.

```
b : List args -> Dict String kwargs -> Maybe Int
b peter paul 

```

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
