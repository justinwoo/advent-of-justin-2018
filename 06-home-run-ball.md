We've long seen row types being used to encode information in PureScript, with the built-in Record types (`data Record :: # Type -> Type`), with Polymorphic Variants (via the purescript-variant library), or even the old Eff type (which was not very useful: <https://purescript-resources.readthedocs.io/en/latest/eff-to-effect.html>). But not many people take enough advantage of them for how they hold information you can use. While many users of variant will take advantage of the `match` function and others that work by iterating the row type information via RowToList, they do not make their own implementations that use these.

## "Fun Row-typed Validation with Purescript-Home-Run-Ball"

One of the most fun things I worked on last year used row type information to store what validation should and have been performed on a value. And so, when this refinement type information is readily available, we are able to automatically derive functions to get a [Validation](https://qiita.com/kimagure/items/f75befebdd37f6e8879f) out of these values, with a newtype carrying the validations that have been performed.

<https://qiita.com/kimagure/items/eeb40541fc56b8dba2cc>

By using RowToList, we can iterate over the validations to be performed, and by producing a newtype with the validations row type parameter, we can use regular extensible row types for requiring validation sets, e.g.

```hs
onlyOnApples
  :: ValidatedValue (beginsApple :: BeginsWith "Apple") String
  -> String
onlyOnApples _ = "U R COOL"

onApples
  :: forall r
   . ValidatedValue (beginsApple :: BeginsWith "Apple" | r) String
  -> String
onApples _ = "U R COOL"
```
