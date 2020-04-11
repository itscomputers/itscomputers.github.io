---
layout: section
title: division with remainder
chapter: 1
section: 2
prev: divisibility
next: greatest-common-divisor
permalink: division-with-remainder
---

The [naive divisibility function](/divisibility#ruby-naive-divides)
in the previous section has a `while` loop whose termination depends on
the following principle.

<span id="archimedes-principle" />
> **`Archimedes' principle`**:
> For an integer $$ a $$ and a nonzero integer $$ b $$, there exists a
> multiple of $$ b $$ which is greater than or equal to $$ a $$.
{: .proposition}

This principle is equivalent to the **division algorithm**.

<span id="division-algorithm" />
> **`proposition 1.2.1 (division algorithm)`**:
> For an integer $$ a $$ and a nonzero integer $$ b $$, there are unique
> integers $$ q $$ and $$ r $$ such that
> $$ a = bq + r $$ and $$ 0 \le r < |b|. $$
{: .proposition}

Terminology:
- $$ a $$ is called the *dividend*
- $$ b $$ is called the *divisor*
- $$ q $$ is called the *quotient*
- $$ r $$ is called the *remainder*

Before proving the division algorithm, here are a few examples.
- Dividing $$ 71 $$ by $$ 20 $$ gives $$ 71 = 20(3) + 11 $$
- Dividing $$ 71 $$ by $$ -20 $$ gives $$ 71 = -20(-3) + 11  $$
- Dividing $$ -71 $$ by $$ 20 $$ gives $$ -71 = 20(-4) + 9 $$
- Dividing $$ -71 $$ by $$ -20 $$ gives $$ -71 = -20(4) + 9 $$

> **`proof of division algorithm`**:
> If $$ a \ge 0 $$, consider the set $$ S $$, consisting of integers of
> the form $$ a - bn $$ where $$ n $$ is an integer,
> ie, $$ S = \{ a - bn : n \in \mathbf{Z} \}. $$
> The intersection of $$ S $$ the with nonnegative integers is non-empty,
> since $$ a $$ itself is nonnegative. By the well-ordering principle,
> there must be a unique smallest nonnegative element of $$ S $$, say
> $$ r = a - bq $$.  Since $$ r - |b| = a - b(q \pm 1) $$ is a smaller
> element of $$ S $$, it must be negative, hence $$ r < |b|. $$
>
> If $$ a < 0 $$, then $$ -a $$ is positive, which was proven above to be
> expressable as $$ -a = bQ + R. $$  If $$ R = 0 $$, set $$ q = -Q $$ and
> $$ r = 0. $$  Otherwise, set $$ r = -R + |b| $$ and
> $$ q = -Q - |b| / b. $$  In either case, this gives
> $$ a = -bQ - R = bq + r $$ with $$ 0 \le r < |b|. $$
{: .proof}

In computing, the implementation of a division and remainder (modulus)
operator likely will not match the specification given by the division
algorithm.  When the dividend or divisor is negative, it may result
in a negative remainder.

In ruby, integer division is floor division, so the quotient `a / b` is
computed by rounding down the rational number $$ a / b. $$  The sign of
the remainder `a % b` is the same as the sign of the divisor `b`.

{% highlight python %}
#ruby
(71 / 20, 71 % 20)
# ~> (3, 11)

(-71 / 20, -71 % 20)
# ~> (-4, 9)

(71 / -20, 71 % -20)
# ~> (-4, -9)

(-71 / -20, -71 % -20)
# ~> (3, -11)
{% endhighlight %}

In rust, integer division is truncation, so the quotient `a / b` is
computed by rounding the rational number $$ a / b $$ toward zero.  The
sign of the remainder `a % b` is the same as the sign of the dividend `a`.

{% highlight rust %}
// rust
(71 / 20, 71 % 20)
// ~> (3, 11)

(-71 / 20, -71 % 20)
// ~> (-3, -11)

(71 / -20, 71 % -20)
// ~> (-3, 11)

(-71 / -20, -71 % -20)
// ~> (3, -11)
{% endhighlight %}

The implementation of a division algorithm function is therefore dependent
on the chosen language.  In ruby, it might look something like this.

{% highlight ruby %}
# ruby
def div_rem(a, b)
  q = a / b
  r = a % b
  b < 0 ? [q + 1, r - b] : [q, r]
end
{% endhighlight %}

The division algorithm is intimately related to the question of
divisibility, as this proposition makes clear.

<span id="1.2.2" />
> **`proposition 1.2.2`**:
> A nonzero integer $$ b $$ divides an integer $$ a $$ if and only if
> the division of $$ a $$ by $$ b $$ yields a remainder of $$ 0 $$.
{: .proposition}

> **`proof`**:
> If the division algorithm gives $$ a = bq + r $$ with $$ r = 0$$, then $$ a = bq $$,
> which implies the $$ b \mid a $$.  Conversely, if $$ b \mid a $$, then $$ a = bn $$
> for some $$ n $$.  Since the division algorithm produces a unique quotient and remainder,
> it must be true that $$ q = n $$ and $$ r = 0 $$.
{: .proof}

Using this proposition, the
[naive divisibility function](/divisibility#ruby-naive-divides)
is no longer needed.  Simply put, $$ b $$ divides $$ a $$ if and only if
`a % b == 0`.

---
<span id="exercises" />
### exercises

1. Write a division algorithm function in a language other than ruby.

