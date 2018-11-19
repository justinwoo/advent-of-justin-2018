With most libraries that work purely with instances, working with an exception is quite annoying. Take for an example the case where you have a record of a couple different fields. If all of the fields have an instance for your decoding type class, everything works just fine. What if just one of those fields is actually a date, but in JSON is represented as a state? Then your entire record no longer has an instance for decoding.

But surely, we should be able to hot swap this, right? There's no catch-all instance for printing and parsing date strings, since everyone likes to use different formats. Sure, we might newtype the field itself, but then we pay the penalty of having to carry around a newtype for whatever date type we use elsewhere. We could also newtype the type that carries this type, but then we need to manually write out how the other fields of the record are read too. Surely there must be some kind of solution where we can tell the compiler to do the default decoding of all of the other fields save one, which we'll handle ourselves.

Well, considering that PureScript has anonymous record types, couldn't we get the compiler to infer some other type here that we can work with? Yeah, we can!

## "Modified JSON parsing for free with PureScript-Simple-JSON"

In this post, I talked about how we can get the compiler to infer for us a type that is decoded from some JSON that we can then further manually decode and replace properties.

<https://qiita.com/kimagure/items/801e1c55d4f8f218f11e>

Since I wrote this post, I also wrote a page in the Simple-JSON guide:

<https://purescript-simple-json.readthedocs.io/en/latest/inferred-record-types.html>

In short, inferred record types let us to do this:

```hs
type RecordMisnamedField =
  { cherry :: Int
  }
  
readRecordMisnamedField :: String -> Either Foreign.MultipleErrors RecordMisnamedField
readRecordMisnamedField s = do
  inter <- JSON.readJSON s
  pure $ Record.rename grapeP cherryP inter
  where
    grapeP = SProxy :: SProxy "grape"
    cherryP = SProxy :: SProxy "cherry"
```

And this will read JSON with `grape :: Int` from the inferred context.
