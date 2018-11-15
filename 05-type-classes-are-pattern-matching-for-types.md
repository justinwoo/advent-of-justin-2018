Many who read more about type classes are surprised to find that "type classes" doesn't actually mean a single thing, but relates to a whole family of features and the idea of working with types at a level similar to working with values. And so, I wrote about this before in my infamous blog post, "What I've learned since quitting Elm
": <https://qiita.com/kimagure/items/93a42d67a8833f99fe2e#type-classes-is-not-a-single-feature>

Today, I invite you to learn more about what type classes and its family of features really are: pattern matching for types.

## "Type classes and instances are pattern matching for types"

In this post, I talk about how type classes and their instances are pattern matching for types of a kind, just as pattern matching with case expression are pattern matching for values of a Type. I specifically talk about this in terms of how it works with the RowList kind from RowToList:

<https://qiita.com/kimagure/items/08c59fa21adcd6968ae1>

Since the post is so heavily focused on how RowList matching works, I later prepared some examples and a talk about this topic starting from a simpler level, where I directly show some comparable code of data types and user-defined kinds with data types of that kind:

<https://speakerdeck.com/justinwoo/type-classes-pattern-matching-for-types>

(source: <https://github.com/justinwoo/purescript-typelevel-intro/blob/master/slides.md>)

Hopefully my slides will make more sense if you're not familiar with how RowToList/RowList and such work. And while many of the people who should read this material really won't, I hope others can make some derivative works that help spread this knowledge to others, such that people start to learn more about this.
