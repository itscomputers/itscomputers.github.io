---
layout: section
category: number theory
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
{: .definition}

Here are a few examples:
- $$ 15 $$ divides $$ 45 $$ since $$ 45 = 15 \cdot 3 $$
- $$ 9 $$ divides $$ 45 $$ since $$ 45 = 9 \cdot 5 $$
- $$ 10 $$ does not divide $$ 45 $$ since $$ 45 $$ is between
$$ 40 = 10 \cdot 4 $$ and $$ 50 = 10 \cdot 5 $$

<span id="exercises-divides" />
> **`exercises`**:
> Use the definition of *divides* to complete the following proofs.
> 1. Prove that any nonzero integer divides $$ 0. $$
> 2. Prove that $$ 1 $$ and $$ -1 $$ divide any integer.
> 3. Prove that any nonzero integer divides itself.
> 4. If $$ a $$ and $$ b $$ are positive integers and $$ b $$ divides
> $$ a, $$ prove that $$ b \le a. $$
> 5. Prove that two integers that divide each other must be equal.
> 6. Prove that the `divides` relation is *transitive*, ie
> if $$ c \mid b $$ and $$ b \mid a, $$ prove that $$ c \mid a. $$
{: .exercise}


The above definition is synonymous with saying that $$ b $$
may be expressed as a multiple of $$ a. $$  In fact, the following
statements are equivalent and mean that $$ a $$ is can be expressed as
$$ bn. $$
- $$ b $$ divides $$ a $$
- $$ b $$ is a divisor of $$ a $$
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

<span id="exercise-naive-divides" />
> **`exercise`**:
> Using *only* addition, multiplication, and comparison, write a function
> that takes as input two positive integers `b` and `a` and returns
> a boolean: `true` if $$ b \mid a $$ and `false` if $$ b \nmid a. $$
{: .exercise}

{% include button.html id="ruby-naive-divides" %}
<div id="ruby-naive-divides" style="display: none;">
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
</div>

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

<span id="exercises-divisibility" />
> **`exercises`**:
> 1. If $$ d $$ divides both $$ a $$ and $$ b, $$ prove that $$ d $$ divides
> their sum $$ a + b. $$
> 2. Disprove the converse of the previous exercise by
> producing a counter-example.
> 3. If $$ d $$ divides either $$ a $$ or $$ b, $$ prove that $$ d $$
> divides their product $$ ab. $$
> 4. Disprove the converse of the previous exercise by
> producing a counter-example.
{: .exercise}

