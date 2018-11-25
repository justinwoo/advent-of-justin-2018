While we've previously talked about ways to model JS charting library specs by using Row.Union, another interesting viewpoint to look from instead is how to allow for building an arbitrary spec just based on restricting what properties can be set based on what kind of chart we are building.

## "Using Rows and RowToList to model Chart.js spec building"

In this article, I talked about how we might model spec-building for Chart.js, by using a row type to specify which functions for builder components are valid for which types of charts:

<https://qiita.com/kimagure/items/fd05ad13ee8def0fb4ed>

The problem that this article mainly focused on was that we needed to get the intersection of two row types when composing chart builders:

```hs
newtype ChartBuilder
  (appliesTo :: # Type)
  (input :: # Type)
  (output :: # Type)
  = ChartBuilder (Builder (Record input) (Record output))
```

So to compose two of these chart builders together, we need to make sure that the new chart builder that we output has a `appliesTo` parameter that is valid. So given the composition of `( a :: _ , b :: _ )` and `( a :: _ )`, we need to produce the output `( a :: _ )`.

While it would be convenient if we could have multiple constraints solved simultaneously to allow us to express a system of Union constraints, we do need to actually implement this in terms of RowToList as only one constraint can be fully determined at a time. I wrote about this problem more in the follow-up article, "Making Diffs of differently-typed Records in PureScript", so I hope you'll read through it sometime:

<https://qiita.com/kimagure/items/ca229cb4ba76db0c24a8>
