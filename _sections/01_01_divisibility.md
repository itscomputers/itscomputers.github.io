---
layout: section
title: divisibility
chapter: 1
section: 1
next: division-with-remainder
permalink: divisibility
---

This study of integers begins with the notion of divisibility.  It is
assumed that addition, subtraction, and multiplication of integers has
already been defined and is well understood.

<span id="divides" />
> **`definition`**:
> A nonzero integer $$ b $$ *divides* an integer $$ a $$ if there exists
> some integer $$ n $$ such that $$ a = bn. $$
{: definition}

Here are a few examples:
- $$ 15 $$ divides $$ 45 $$ since $$ 45 = 15 \cdot 3 $$
- $$ 9 $$ divides $$ 45 $$ since $$ 45 = 9 \cdot 5 $$
- $$ 10 $$ does not divide $$ 45 $$ since $$ 45 $$ is between
$$ 40 = 10 \cdot 4 $$ and $$ 50 = 10 \cdot 5 $$

Notice that the above definition is synonymous with saying that $$ b $$
may be expressed as a multiple of $$ a. $$  In fact, the following
statements are equivalent and mean that $$ a $$ is can be expressed as
$$ bn. $$
- $$ b $$ divides $$ a $$
- $$ a $$ is divisible by $$ b $$
- $$ a $$ is a multiple of $$ b $$

The notation for this concept is $$ b \mid a, $$ which reads "$$ b $$
divides $$ a $$".  Using this notation, the examples above become:
- $$ 15 \mid 45 $$ since $$ 45 = 15 \cdot 3 $$
- $$ 9 \mid 45 $$ since $$ 45 = 9 \cdot 5 $$
- $$ 10 \nmid 45 $$ since $$ 10 \cdot 4 < 45 < 10 \cdot 5 $$

Be careful!  This notation may sometimes be confused with the division
operation. If you see $$ 15 / 45, $$ it is the operation that returns
the rational number $$ 1/3. $$  If you see $$ 15 \mid 45, $$ it is the
statement that $$ 15 $$ divides $$ 45, $$ ie, that $$ 45 $$ is divisible
by $$ 15, $$ ie, that $$ 45 / 15 $$ is an integer.

---
### in code

As the last example suggests, a naive approach to determining divisibility
is to check all multiples of $$ b $$ until you surpass $$ a. $$ Here is a
ruby implementation of this naive divisibility algorithm, assuming that
both $$ a $$ and $$ b $$ are positive.

<span id="ruby-naive-divides" />
{% highlight ruby %}
# ruby
def divides?(b, a)
  m = 0
  while m < a
    m += b
  end

  m == a
end
{% endhighlight %}

---
### linear combinations

A concept that will appear often is that of integer linear combinations.

<span id="integer-linear-combination" />
> **`definition`**:
> An *integer linear combination* of integers $$ a $$ and $$ b $$ is an
> integer of the form $$ ax + by $$ where $$ x $$ and $$ y $$ are integers.
{: .definition}

For example, $$ 11 $$ through $$ 15 $$ can all be expressed as linear
combinations of $$ 5 $$ and $$ 6 $$.  Here are two examples of each.
- $$ 11 = 5(1) + 6(1) $$ or $$ 11 = 5(7) + 6(-4) $$
- $$ 12 = 5(0) + 6(2) $$ or $$ 12 = 5(6) + 6(-3) $$
- $$ 13 = 5(-1) + 6(3) $$ or $$ 13 = 5(5) + 6(-2) $$
- $$ 14 = 5(-2) + 6(4) $$ or $$ 14 = 5(4) + 6(-1) $$
- $$ 15 = 5(-3) + 6(5) $$ or $$ 15 = 5(3) + 6(0) $$

The following proposition about integer linear combinations will be used
often.

<span id="divides-linear-combinations" />
> **`proposition 1`**:
> If $$ d $$ divides both $$ a $$ and $$ b, $$ then $$ d $$ divides any
> integer linear combination of $$ a $$ and $$ b. $$
{: .proposition}

> **`proof`**:
> Suppose that $$ d $$ divides $$ a $$ and $$ b. $$  By definition,
> $$ a = dm $$ and $$ b = dn $$ for some integers $$ m, n. $$  Let
> $$ c = ax + by $$ be an integer linear combination of $$ a $$ and
> $$ b. $$  Then $$ c $$ can be expressed as
> $$ (dm)x + (dn)y = d(mx + ny). $$  Since $$ mx + ny $$ is an integer,
> this proves that $$ d \mid c. $$
{: .proof}

---
### think about it

1. Why is $$ b $$ required to be nonzero in the
[definition of *divides*](#divides)?

1. Does an integer exist which divides every integer?  If so, find all
such integers.

---
<span id="exercises" />
### exercises

1. Prove that every integer divides $$ 0. $$

1. Prove that every integer divides itself.

1. If $$ a $$ and $$ b $$ are positive integers and $$ b $$ divides
$$ a, $$ prove that $$ b $$ is less than or equal to $$ a. $$

1. If two positive integers divide each other, prove that they are equal.

1. Prove that the `divides` relation is *transitive*.  In other words,
if $$ c \mid b $$ and $$ b \mid a, $$ prove that $$ c \mid a. $$

1. If $$ d $$ divides both $$ a $$ and $$ b, $$ prove that $$ d $$ divides
their sum $$ a + b. $$

1. Show that the converse of the previous exercise is not true by
producing a counter-example.

1. If $$ d $$ divides either $$ a $$ or $$ b, $$ prove that $$ d $$
divides their product $$ ab. $$

1. Show that the converse of the previous exercise is not true by
producing a counter-example.

1. Write an improved version of the
[naive divisibility function](#ruby-naive-divides) above.  It should
take *any nonzero* integer $$ b $$ and *any* integer $$ a $$ and return `true`
if `b` divides `a` and `false` otherwise.  The function
- may be in the language of your choice
- should **only** use addition, multiplication, and comparison.
- should handle negative inputs as well as positive.

