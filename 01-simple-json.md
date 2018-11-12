Welcome to the Advent of Justin 2018! I've joked about making this happen, but I guess now it's actually happening.

For the first day, I figured I would introduce an old favorite: Simple-JSON. This is a library that I first made in July 2017, with some expectation that it would just be a demo. Little did I know, this library actually became fairly popular as a nice way to get automatic de/serialization of JSON/Foreign, and I found myself immediately putting this library to work when beginning to use PureScript for work.

The thing that I like so much about this library isn't really even the JSON part, but that it shows that you can readily use types to derive values to put to use. This is what makes me keep using PureScript over any other language that compiles to JS, and what you'll see featured in most of my posts about PureScript.

## "Writing a JSON decoder using Purescript's RowToList"

In this post, I go through what exactly a `Record` is, and how the row type information can be turned into a type-level iterable data structure to derive decoders and encoders for JS values:

<https://qiita.com/kimagure/items/d8a0681ae05b605c5abe>

Earlier this year, I started putting some effort into documentation of some of my libraries. From that effort, I have these docs for Simple-JSON now: <https://purescript-simple-json.readthedocs.io/en/latest/index.html>. Everything a user of this library should need is just about here, with even a guide for how to use Generics-Rep to write your own encodings for sum/product types.

Here's an excerpt from the quickstart page:

```hs
import Simple.JSON as JSON

type MyRecordAlias =
  { apple :: String
  , banana :: Array Int
  }

testJSON1 :: String
testJSON1 = """
{ "apple": "Hello"
, "banana": [ 1, 2, 3 ]
}
"""

main = do
  case JSON.readJSON testJSON1 of
    Right (r :: MyRecordAlias) -> do
      assertEqual { expected: r.apple, actual: "Hello"}
      assertEqual { expected: r.banana, actual: [ 1, 2, 3 ] }
    Left e -> do
      assertEqual { expected: "failed", actual: show e }
```

## P.S.

So the first post of the Advent of Justin ended up being a little longer than planned. The next posts will be shorter, but hopefully you'll read through some more of these.
