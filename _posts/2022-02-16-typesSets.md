---
title: "Types vs Sets"
categories:
  - Programming Languages
tags:
  - Types
  - Functional Programming
  - Imperative Programming
  - Concurrency
---

I came across a blog post a while ago. The overarching question of it was about the relationship between types and sets in a programming language and I wasn't really happy with the answer they gave. Specifically, it was applied in a particular expression:

```
{1, 2, 3} ⊆ Nat
```

This is a comparison of what we would usually think about as a set with a type. Furthermore, it should be possible that if this expression were included in code, it could be executed during compile time rather than runtime.

The primary reason this should work is that a type and a set are the same thing. So, why does this seem off?

To make sense of it, it is important to first go into a separate distinction: types and values. As an example, let's say that you have a `uint8 x`. The type of `x` is all of the possible values that it can have, which is in fact a set. Here, it can be any value from 0-255. But, you don't know which of those 256 values it actually is.

In comparison, a value for `x` is concrete like 2 or 10. In general, concrete values will only be known once the code is actually run. Often it requires various inputs, files, or computations to find it.

In summary, a type corresponds to what you know before code is run. A value is what you know when it is running. The difference between the two is time.

Now going back to our example of `{1, 2, 3} ⊆ Nat`, the real reason it seems off is not because we are comparing a set and a type. It is because we are comparing a value to a type.

To some extent, it can be done. There are functions that take some type arguments and some value arguments. But, working with values and with types are very different techniques. One deals with possibilities and one deals with certainties.

Rather than trying to combine the two, it is better to pick one methodology to use and stick with it. Either convert your problem into a "value to value" or "type to type" problem. Fortunately, in this situation, both are possible. And, I think there is value in understanding both solutions.

## Values to values

The more straightforward case is to turn a type into a value. There are two main ways to do it. The first is by defining how to enumerate the type:

```
enum<Enumerable $T> -> Set<$T>
```

A type can be enumerable if you can list all of the elements inside it and store it into memory as a HashSet or TreeSet. An example would be:

```
enum<Boolean> = set([True, False])
```

At this point, we can simply use this type like a normal set. And, once we are comparing two set values, we can just compute them normally.

But, that's not quite our goal. We want to be able to do this during compile time and this code will typically run during runtime. Now, we know that both `{1, 2, 3}` and `Nat` are constant values. And, expressions involving only constant values are also constant. So, it is possible to compute this during compile time.

So, we just have to indicate to the compiler that this constant expression should be precomputed during compile time. This is a completely separate feature from working with types and has many use cases. This just happens to be one. But assuming the language does have a precompute feature implemented, we just need to indicate that the expression should be precomputed and we are done.

Not really. While `enum` would work for some types, it won't work for `Nat`. Many types such as `Nat` are infinite. So, unless you also have a computer with infinite memory and computing power, storing all natural values in a `HashSet` or `TreeSet` is not going to end well.

Instead, we need some kind of virtual set that merely describes the contents rather than enumerates it. And, the easiest way to do that is to simply use types to indicate the set contents assuming that types are powerful enough. In that case, we would have something like `TypeSet<Nat>`. When we use it for our operation, it should work something like:

```
   {1, 2, 3}.subset(TypeSet<Nat>)
 = {1, 2, 3}.all<Nat>                    # definition of Set.subset(TypeSet)
 = True                                  # definition of Set.all<$T>
```

Just like with the memory set, these value computations are usually done during runtime. So, we still need to indicate that we should precompute it. But, this is the final solution to our problem using values.

## Types to types

The other option to solve our problem is to instead look at the problem in terms of types.

Let's go back to our original example of `unit8 x`. Now, just because we don't know exactly what `x` is doesn't mean we don't know anything. If you ask whether `x < 100`, we don't know because we don't the value. But, if we ask if `x < 1000`, we don't even need to know what `x` is because every one of the 256 possible values for `x` would make it true.

Returning to our main goal of `{1, 2, 3} ⊆ Nat`, the function we are calling in our expression is:

```
Set.subset(Set other) -> Boolean
```

One of the ways to best work with types is to have supplementary definitions that represent specific cases of the main definition. Here, we are dealing with the case where the other is a typeset. The function could be defined as:

```
Set.subset(TypeSet<$T> other) = this.all<$T>
```

But, there is also an even more specific supplementary definition that we can add. We know all of the possible values of the main set as that is it's type. And, a `TypeSet`, unlike a regular `Set`, means we know it's exact values rather than just some possibilities. So, we can check beforehand if the main `Set` is guaranteed to be a subset because then we don't need to do any runtime work. Specifically, it would look like:

```
Set<$T _>.subset(TypeSet<$T> other) = True
```

The only potential problem is what is the type of `{1, 2, 3}`? If it is `Set<Int>` for example, then not all `Int` are `Nat`. While `Set<Int>` is a valid bound on the type, it is too loose of a bound. In order to know that it contains only `Nat`, then it's type must be determined more precisely.

The simplest way is to define `class Nat = Int_gte(0)`. Then, by computing the minimum of the set it can be determined that the type of `{1, 2, 3} :: Int_gte(1)_lte(3)`. If the language is sufficiently precise to compute this for constant values where it can be computed, then it satisfies the requirements to simplify the whole subset operation to True.

## Conclusion

In this post, I wanted to give an intuitive argument about how to work with types and sets. It should make the problem simpler and provide useful tools to work with similar problems. I hope I have achieved that.

While I presented both a solution working with values and types, I think types should really be the correct solution in this instance. If the type information is sufficient, it would work automatically. The value solution, however, requires some effort to handle pre-computing. For other problems with more computation required, the value one may still be useful.
