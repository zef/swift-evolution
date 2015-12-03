# Add Shorthand Syntax for Optional Binding

* Proposal: [SE-NNNN](https://github.com/apple/swift-evolution/proposals/NNNN-optional-binding-shorthand.md)
* Author: [Zef Houssney](https://github.com/zef)
* Status: **Awaiting Review**
* Review manager: TBD

## Introduction

A common practice in Swift is to use the `if let foo = foo {}` syntax to bind an
optional. I propose an optional simplification to this syntax by allowing simply
`if let foo {}` to bind the optional to `foo`.


## Motivation

This would reduce the amount of redundant code that does not add value or
clarity, leading to shorter lines and code that can be visually processed more
quickly.

Additionally, a common pattern I see is that people tend to rename the bound
value with often meaningless and unhelpful variants of the original variable or
constant name. For example people often write `if let newFoo = foo {}` or worse
something like `unwrappedFoo`. While this renaming _can_ add value, I generally
believe that it doesn't, but rather adds overhead to mentally parsing code.
Introducing a shorthand syntax would encourage simply masking a carefully chosen
variable name inside the block, which reduces the amount of time that goes into
thinking about naming variables and removes the unnecessary step.


## Proposed solution

Compare the following
```
// before
if let thing = thing, otherThing = otherThing, moreThings = moreThings where thing > 0 {
  // ...
}

// after
if let thing, otherThing, moreThings where thing > 0 {
  // ...
}
```

This syntax proposal encourages shorter, more readable lines. This is especially
valuable when chaining multiple bindings together and using where clauses.



Describe your solution to the problem. Provide examples and describe
how they work. Show how your solution is better than current
workarounds: is a cleaner, safer, or more efficient?


## Detailed design

TODO


## Impact on existing code

This change would introduce a new syntax that could be adopted, but would not
require any changes to existing code. An automatic migration to encourage
adoption of this syntax would be relatively simple, if desired. If desired, I
would suggest doing the automatic replacement when both sides of the `=` are
identical, but not suggesting the change for renamed variables.


## Alternatives considered

Alternatively, the Swift syntax could stay the same and developers would be
_forced_ to retype _thousands_ of redundant variable names to unwrap them. :)

