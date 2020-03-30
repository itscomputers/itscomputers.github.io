---
layout: section
title: divisibility
chapter: 1
section: 1
permalink: divisibility
---

<span id="1.1.1" />
> **`definition`**:
> We say that a nonzero integer `b` *divides* an integer `a` if there exists some
> integer `n` such that `a = b*n`.

Here are a few examples:
- `15` divides `45` since `45 = 15*3`
- `9` divides `45` since `45 = 9*5`
- `10` does not divide `45` since `45` is between `40 = 10*4` and `50 = 10*5`

Notice that the above definition is synonymous with saying that `b` may be
expressed as a multiple of `a`.  In fact, the following statements are
equivalent.
- `b` divides `a`
- `a` is divisible by `b`
- `a` is a multiple of `b`

Although the three phrases have the same meaning, we will often use the first one.
The notation for this is `b|a`, which reads `b` divides `a`.  The first two
examples above could be expressed as `15|45` and `9|45`.

Be careful!  This notation may sometimes be confused with the division operation.
If you see `15/45`, it is the operation that results in one third.
If you see `15|45`, it is the statement that `15` divides `45`, ie, that `45`
is divisible by `15`, ie, that `45/15` is an integer.

Here are a couple of propositions about integers that can be proved from the
definition of divisibility.

<span id="1.1.2" />
> **`proposition 1.1.2`**:
> If `d` divides both `a` and `b`, then `d` divides their sum.
>
> **`proof`**:
> Since `d|a`, there is an integer `m` such that `a = d*m`.  Similarly,
> since `d|b`, there is an integer `n` such that `b = d*n`.  Therefore,
> the sum satisfies `a + b = d*m + d*n = d*(m+n)`.  Since `m+n` is an integer,
> this equation implies that `d|(a+b)`.

<span id="1.1.3" />
> **`proposition 1.1.3`**:
> If `d` divides either `a` or `b`, then `d` divides their product.
>
> **`proof`**:
> If `d|a`, then there is an integer `m` such that `a = d*m`, so the product is
> `a*b = (d*m)*b = d*(m*b)`, which is a multiple of `d`.
> Otherwise, `d|b`, in which case there is an integer `n` such that `b = d*n`, so
> the product is `a*b = a*(d*n) = d*(a*n)`, which is also a multiple of `d`.
> Either way, `a*b` is divisible by `d`.

---
### think about it:

1. Why is `b` is required to be nonzero in <a href="#1.1.1">definition 1.1.1</a>?

1. Does an integer exist which divides every other integer?  If so, find the integer(s).

---
<span id="exercises" />
### exercises:

1. Prove that every integer divides `0`.

1. Prove that every integer divides itself.

1. If `a` and `b` are positive integers and `b` divides `a`, prove that `b` is less
than or equal to `a`.

1. If two positive integers divide each other, prove that they are equal.

1. Prove that the `divides` relation is *transitive*.  In other words, if `c|b`
and `b|a`, prove that `c|a`.

1. Prove that the converse of <a href="#1.1.2">proposition 1.1.2</a> is false by
providing a counter-example.

1. Prove that the converse of <a href="#1.1.3">proposition 1.1.3</a> is false by
providing a counter-example.

1. If `d` divides both `a` and `b`, prove that `d` divides any integer combination
of `a` and `b`.  (Note that an *integer combination* of `a` and `b` is defined to
be any integer of the form `a*x + b*y`, where `x` and `y` are integers.)

1. Show that propositions <a href="#1.1.2">1.1.2</a> and <a href="#1.1.3">1.1.3</a>
are special cases of the previous exercise.

1. Write a function in the language of your choice that takes a pair of integers
`b`, `a` and returns `true` if `b|a` and `false` otherwise.  In ruby, your function
might look something like this:

{% highlight ruby %}
def divides?(b, a)
  return false if b == 0
  (a / b) * b == a
end
{% endhighlight %}
