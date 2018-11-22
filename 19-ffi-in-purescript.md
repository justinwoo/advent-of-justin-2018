One of the most convenient things about using PureScript is the FFI, which is quite lenient in letting you choose now you want to work with it. However, many times people don't learn enough about how the FFI works, usually because they think that it will be too hard/too much of a hassle, or see it as "below" them. Well, I don't know how we can help people in the latter camp, but the former camp can definitely be empowered with some references and examples.

## "User empowerment of FFI in PureScript"

In this post, I talked about the various common FFI techniques in PureScript, such as uncurried effect functions, opaque data types, Promises to Aff, and more:

<https://qiita.com/kimagure/items/0ce4d9d2792dd110ee45>

It's important to note that if you do want to validate some returned value from JS, you can readily put Simple-JSON to work to work on `Foreign`-typed values.

If reading a whole post seems like too much, I think your time is most well spent at least reading the Effect.Uncurried docs:

<https://pursuit.purescript.org/packages/purescript-effect/2.0.0/docs/Effect.Uncurried>
