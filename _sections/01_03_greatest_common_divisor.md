---
layout: section
title: greatest common divisor
chapter: 1
section: 3
prev: division-with-remainder
next: bezouts-identity
permalink: greatest-common-divisor
---

<span id="greatest-common-divisor" />
> **`definition`**:
> A *common divisor* of two integers $$ a $$ and $$ b $$ is an integer
> $$ d $$ such that $$ d \mid a $$ and $$ d \mid b. $$  The *greatest
> common divisor* of $$ a $$ and $$ b $$ is their largest positive
> common divisor.
{: .definition}

- The notation for the greatest common divisor of $$ a $$ and $$ b $$ is
$$ \gcd(a, b). $$

- By definition, the greatest common divisor of two integers is independent
of the sign of the two integers --- the gcd is the same if you replace
$$ a $$ with $$ -a $$ or $$ b $$ with $$ -b. $$

- The definition of gcd does not make sense if $$ a $$ and $$ b $$ are
both equal to $$ 0. $$  The assumption for the rest of the section is
that at least one of them is nonzero.

The existence of a greatest common divisor stems from the following fact:
every pair of integers has at least one positive common divisor $$ 1, $$
and can only have finitely many positive common divisors since any
positive divisor of an integer is less than or equal to its absolute
value.

<span id="exercises-gcd" />
> **`exercises`**:
> 1. Explain why $$ \gcd(0, 0) $$ is undefined.
> 1. If $$ a $$ is nonzero, prove that $$ \gcd(a, 0) = \vert a \vert. $$
> 1. If $$ b \mid a, $$ prove that $$ \gcd(a, b) = \vert b \vert. $$
{: .exercise}

---
### naive computation

The greatest common divisor can be computed naively by finding the positive
divisors of each number and taking the intersection of the two sets.  For
example, to compute $$ \gcd(322, 70) $$
- the positive divisors of $$ 322 $$ are
$$ \{ 1, 2, 7, 14, 23, 46, 161, 322 \} $$
- the positive divisors of $$ 70 $$ are
$$ \{ 1, 2, 5, 7, 10, 14, 35, 70 \} $$
- the positive common divisors of $$ 322 $$ and $$ 70 $$ are
$$ \{ 1, 2, 7, 14 \} $$
- the greatest common divisor is $$ \gcd(322, 70) = 14 $$

<span id="exercise-naive-gcd" />
> **`exercise`**:
> Write a `naive_gcd` function that returns the greatest common divisor of two
> integer inputs.  It should only rely on divisibility checks.
{: .exercise}

{% include button.html id="ruby-naive-gcd" %}
<div id="ruby-naive-gcd" style="display: none;">
{% highlight ruby %}
# ruby
def naive_gcd(a, b)
  divisor = nil
  limit = [a.abs, b.abs].min

  (1..limit).each do |d|
    if a % d == 0 && b % d == 0
      divisor = d
    end
  end

  divisor
end
{% endhighlight %}
</div>

---
### Euclidean algorithm

This gcd algorithm is slow, growing linearly in the size of the smaller
of the two integers.  The next proposition is instrumental in
developing a more efficient algorithm to compute the gcd.

<span id="division-algorithm-and-gcd" />
> **`proposition 4`**:
> If $$ a = bq + r, $$ then $$ \gcd(a, b) = \gcd(b, r). $$
{: .proposition}

> **`proof`**:
> Since $$ a = bq + r $$ is a linear combination of $$ b $$ and $$ r, $$
> any common divisor of $$ b $$ and $$ r $$ must also be a divisor of
> $$ a. $$
>
> Since $$ r = a - bq $$ is a linear combination of $$ a $$ and $$ b, $$
> any common divisor of $$ a $$ and $$ b $$ must also be a divisor of
> $$ r. $$
>
> Taken together, the set of common divisors of $$ a, b $$ must be equal
> to the set of common divisors of $$ b, r. $$  Therefore, $$ \gcd(a, b) $$
> must be equal to $$ \gcd(b, r). $$
{: .proof}

Since the division algorithm results in a remainder that is strictly
smaller than the absolute value of the divisor, this proposition will give
a simpler pair of numbers for computing the greatest common divisor.

The **Euclidean algorithm** is repeated application of the
[division algorithm](division-with-remainder#division-algorithm),
replacing $$ a, b $$ with $$ b, r $$ until reaching a remainder of $$ 0, $$
at which point the gcd is trivial to compute.

|-----------------------:|:---------------------|
|                        | $$ \gcd(322, 70) $$  |
| $$ 322 = 70(4) + 42 $$ | $$ = \gcd(70, 42) $$ |
|  $$ 70 = 42(1) + 28 $$ | $$ = \gcd(42, 28) $$ |
|  $$ 42 = 28(1) + 14 $$ | $$ = \gcd(28, 14) $$ |
|   $$ 28 = 14(2) + 0 $$ | $$ = 14 $$           |

In the Euclidean algorithm, the last nonzero remainder is the gcd of the
original two integers.  The gcd is computed without explicitly finding
any of the divisors.

<span id="exercise-euclidean-algorithm" />
> **`exercise`**:
> Write a Euclidean algorithm function that prints the division algorithm
> result from each step. When run on the inputs `(322, 70)`, for
> example, it should print
> <pre class="console">
> 322 == 70 * 4 + 42
> 70 == 42 * 1 + 28
> 42 == 28 * 1 + 14
> 28 == 14 * 2 + 0
> </pre>
{: .exercise}

{% include button.html id="ruby-euclidean-algorithm" %}
<div id="ruby-euclidean-algorithm" style="display: none;">
{% highlight ruby %}
def euclidean_algorithm(a, b)
  while b != 0
    q, r = div_rem(a, b)
    puts "#{a} == #{b} * #{q} + #{r}"
  end
end
{% endhighlight %}
</div>

---
### computation of gcd

As mentioned, the Euclidean algorithm can be used to compute the greatest
common divisor.  One formulation of this is the following:

<span id="euclidean-algorithm" />
> **`Euclidean algorithm`**:
> To compute $$ \gcd(a, b) $$
> 1. If $$ b = 0, $$ return $$ \vert a \vert $$
> 2. Otherwise, compute $$ a = bq + r $$ and return to step 1, replacing
> $$ (a, b) $$ with $$ (b, r) $$

The Euclidean algorithm terminates after finitely many steps.  Since the
remainders form a decreasing sequence of positive integers, there
can only be finitely many of them.

In most programming languages, the modulus operator may return a negative
remainder when dealing with negative values.  However, the result of
`a % b` is still smaller than $$ b $$ in absolute value, so repeated
applications of the modulus operator will also terminate after finitely
many steps.  Since the proposition above applies regardless of whether
$$ a = bq + r $$ comes from the division algorithm, the Euclidean
algorithm may be implemented using only the modulus operator.

|-----------------:|:---------------------|
|                  | $$ \gcd(322, 70) $$  |
| `322 % 70 == 42` | $$ = \gcd(70, 42) $$ |
|  `70 % 42 == 28` | $$ = \gcd(42, 28) $$ |
|  `42 % 28 == 14` | $$ = \gcd(28, 14) $$ |
|   `28 % 14 == 0` | $$ = 14 $$           |

<span id="exercise-gcd" />
> **`exercise`**:
> Write a `gcd` function that uses the language's modulus operator: it
> should take two integer inputs and produce their greatest common
> divisor.  Remember that $$ gcd(0, 0) $$ is undefined.
{: .exercise}

{% include button.html id="ruby-gcd" %}
<div id="ruby-gcd" style="display: none;">
{% highlight ruby %}
# ruby
def gcd(a, b)
  while b != 0
    a, b = [b, a % b]
  end

  a == 0 ? nil : a.abs
end
{% endhighlight %}
</div>

This new `gcd` function is much faster than the naive version: it grows
logarithmically as opposed to linearly.  This fact will be proven later.

<span id="exercise-gcd-benchmark" />
> **`exercise`**:
> Benchmark `gcd` vs `naive_gcd` to convince yourself of the stated time
> complexity.
{: .exercise}

---
### testing

<span id="dividing-by-gcd-results-in-relatively-prime" />
> **`proposition 5`**:
> If $$ d = \gcd(a, b), $$ then $$ \gcd(a/d, b/d) = 1. $$
{: .proposition}

> **`proof`**:
> Let $$ k = \gcd(a/d, b/d). $$  Then $$ a/d = km $$ and $$ b/d = kn. $$
> This implies that $$ a = kdm $$ and $$ b = kdn. $$  Therefore, $$ kd $$
> is a common divisor of $$ a $$ and $$ b. $$  If $$ k $$ were not equal
> to $$ 1, $$ then $$ kd $$ would be a larger common divisor than the
> greatest common divisor $$ d, $$ a contradiction.
{: .proof}

This proposition adds a nice property to include in a test for the `gcd`
function.

{% highlight ruby %}
# ruby
def test_gcd(a, b)
  d = result || gcd(a, b)
  error = "`gcd` failed for #{a}, #{b}"

  raise error if a == 0 && b == 0 && !d.nil?
  raise error unless d > 0
  raise error unless a % d == 0
  raise error unless b % d == 0
  raise error unless gcd(a/d, b/d) == 1
end
{% endhighlight %}

