---
layout: section
title: division with remainder
chapter: 1
section: 2
prev: divisibility
permalink: division-with-remainder
---

The ruby implementation of the `divides?` function in the last exercise of the
previous section has a while loop whose termination depends on **Archimedes' principle**.

> **`Archimedes' principle`**:
> For an integer $$ a $$ and a nonzero integer $$ b $$, there exists a multiple
> of $$ b $$ which is greater than or equal to $$ a $$.
{: .proposition}

This is equivalent to the
**division algorithm**,
which will be proven shortly.

<span id="1.2.1" />
> **`proposition 1.2.1 (division algorithm)`**:
> For an integer $$ a $$ and a nonzero integer $$ b $$, there are unique integers
> $$ q $$ and $$ r $$ such that
> $$ a = bq + r $$ and
> $$ 0 \le r < |b|. $$
> These integers are called the *quotient* and *remainder*, respectively.
{: .proposition}

Before proving the division algorithm, here are a few examples.
- Dividing $$ 71 $$ by $$ 20 $$ gives $$ 71 = 20(3) + 11 $$
- Dividing $$ 71 $$ by $$ -20 $$ gives $$ 71 = -20(-3) + 9  $$
- Dividing $$ -71 $$ by $$ 20 $$ gives $$ -71 = 20(-4) + 11 $$
- Dividing $$ -71 $$ by $$ -20 $$ gives $$ -71 = -20(4) + 9 $$

> **`proof of division algorithm`**:
> If $$ a \ge 0 $$, consider the set $$ S $$, consisting of integers of the form
> $$ a - bn $$ where $$ n $$ is an integer,
> ie, $$ S = \{ a - bn : n \in \mathbf{Z} \}. $$
> The intersection of $$ S $$ the with nonnegative integers is non-empty,
> since $$ a $$ itself is nonnegative.
> By the well-ordering principle, there must be a smallest nonnegative element of
> $$ S $$, say $$ r = a - bq $$.  Since $$ r - |b| = a - b(q \pm 1) $$ is a smaller
> element of $$ S $$, it must be negative, hence $$ r < |b| $$.
>
> If $$ a < 0 $$, then $$ -a $$ is positive, which was proven above to be expressable
> as $$ -a = bQ + R. $$  If $$ R = 0 $$, set $$ q = -Q $$ and $$ r = 0 $$, so that
> $$ a = -bQ = bq + r. $$
> Otherwise, set $$ r = -R + |b| $$ and $$ q = -Q - |b| / b $$, so that
> $$
> bq + r = (-bQ - |b|) + (-R + |b|) = -bQ - R = a.
> $$
{: .proof}

Most computer languages have functions that quickly and easily produce the quotient
and remainder for dividing positive integers.  Here are a few examples:

{% highlight ruby %}
# ruby
71 / 20 # returns 3
71 % 20 # returns 11
71.divmod(20) # returns [3, 11]
{% endhighlight %}

{% highlight python %}
# python
71 // 20 # returns 3
71 % 20 # returns 11
divmod(71, 20) # returns (3, 11)
{% endhighlight %}

{% highlight javascript %}
// javascript
Math.floor(71 / 20); // returns 3
71 % 20; // returns 11
{% endhighlight %}

Each language, however, may handle negative values differently.
In ruby, the computed remainder always has the same sign
as the divisor, eg, `71 % -20` results in `-9`.
In javascript, on the other hand, the computed remainder always has the same sign as
the dividend, eg `-71 % 20` results in `-9`.
Writing a function that produces the quotient and remainder required by the
division algorithm may therefore require additional steps, depending on the
language.  For example, the function in javascript might look as follows.

{% highlight javascript %}
function divisionWithRemainder(a, b) {
  let r = a % b;
  let q = (a - r) / b;
  if (a < 0) {
    r += Math.abs(b);
    q += (b < 0) ? 1 : -1;
  }
  return [q, r];
}
{% endhighlight %}


The division algorithm can be used to determine divisibility.

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

The `divides?` function from the previous section can now be written more simply.

{% highlight ruby %}
# ruby
def divides?(a, b)
  a % b == 0
end
{% endhighlight %}

