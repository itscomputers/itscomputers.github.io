---
layout: section
title: bezout's identity
chapter: 1
section: 4
prev: greatest-common-divisor
permalink: bezouts-identity
---

<span id="bezouts-identity" />
> **`proposition 6 (Bezout's identity)`**:
> The greatest common divisor can always be expressed as a linear
> combination of the two integers.  In other words, given two integers
> $$ a $$ and $$ b, $$ there exist integers $$ x $$ and $$ y $$ such that
> $$ ax + by = \gcd(a, b). $$
{: .proposition}

For example, if $$ a = 322 $$ and $$ b = 70, $$ Bezout's identity implies
that $$ 322x + 70y = 14 $$ for some integers $$ x $$ and $$ y. $$  Such
integers might be found by brute force.  In this case, a brute force
search might arrive at the simplest solution $$ (x, y) = (-2, 9). $$
However, a brute force search may not be successful so quickly.

> **`proof`**:
> It will be assumed that $$ a $$ and $$ b $$ are both nonnegative; if
> $$ a $$ or $$ b $$ were negative, then $$ x $$ or $$ y $$ could be
> replaced with $$ -x $$ or $$ -y, $$ respectively.
>
> Instead of proving Bezout's identity directly, it will be proved that
> that every remainder that occurs in the Euclidean algorithm can be
> expressed as a linear combination of the two integers.
>
> The Euclidean algorithm can be thought of as a sequence of equations
> of the form $$ i = jq + r. $$  If $$ i $$ and $$ j $$ are both linear
> combinations of $$ a $$ and $$ b, $$ then so is $$ r. $$  In particular,
> if $$ i = ax_0 + by_0 $$ and $$ j = ax_1 + by_1, $$ then
> $$ r = a(x_0 - qx_1) + b(y_0 - qy_1). $$  In the first instance,
> $$ i = a $$ and $$ j = b, $$ which are both linear combinations, namely
> $$ a = a(1) + b(0) $$ and $$ b = a(0) + b(1). $$  Therefore, the next
> remainder is a linear combination, implying the one after is, and so on.
{: .proof}

This proof is probably best illustrated with an example, say $$ a = 322 $$
and $$ b = 70. $$

|   `i` |  `j` | `q` |   `r` |   `(x, y)` |
|------:|-----:|----:|------:|-----------:|
|       |      |     | `322` |   `(1, 0)` |
|       |      |     |  `70` |   `(0, 1)` |
| `322` | `70` | `4` |  `42` |  `(1, -4)` |
|  `70` | `42` | `1` |  `28` |  `(-1, 5)` |
|  `42` | `28` | `1` |  `14` |  `(2, -9)` |
|  `28` | `14` | `2` |   `0` | `(-5, 23)` |

Ignoring the first two rows and the last column, this table has the same
information as the Euclidean algorithm, namely `i == j * q + r` always
holds.  The last column is how to express `r` as a linear combination,
namely `r == 322*x + 70*y` is always true.  The first two
$$ (x, y) $$ pairs show how to express `322` and `70` as linear
combinations of themselves.  After that, each pair is deduced from the
previous two pairs using the recursive relationships $$ x_2 = x_0 - qx_1 $$
and $$ y_2 = y_0 - qy_1. $$  In other words, the `q` value along with the
previous two $$ (x, y) $$ pairs is used to produce the next pair.

The second to last row is the one which gives a solution to Bezout's
identity, that $$ 322x + 70y = \gcd(322, 70) $$ for
$$ (x, y) = (2, -9). $$
The time complexity for this algorithm grows logarithmically since it
terminates as quickly as the gcd algorithm.

As another example, take $$ a = -322 $$ and $$ b = 70. $$

|    `i` |  `j` |  `q` |    `r` |   `(x, y)` |
|-------:|-----:|-----:|-------:|-----------:|
|        |      |      | `-322` |   `(1, 0)` |
|        |      |      |   `70` |   `(0, 1)` |
| `-322` | `70` | `-5` |   `28` |   `(1, 5)` |
|   `70` | `28` |  `2` |   `14` | `(-2, -9)` |
|   `28` | `14` |  `2` |   `0`  |  `(5, 23)` |

A solution to $$ -322x + 70y = \gcd(-322, 70) $$ is $$ (x, y) = (5, 23). $$

---
### in code

The proof above is a constructive proof: it not only proves that a solution
exists, but also shows how to produce a solution.

<span id="exercise-bezout" />
> **`exercise`**:
> Write a `bezout` function that takes integer inputs `(a, b)` and
> produces integers `(x, y)` such that $$ ax + by = \gcd(a, b). $$
{: .exercise}

{% include button.html id="ruby-bezout" %}
<div id="ruby-bezout" style="display: none;">
{% highlight ruby %}
# ruby
def bezout(a, b)
  pairs = [[1, 0], [0, 1]]
  while b != 0
    q, r = div_rem(a, b)
    a, b = b, r

    next_pair = pairs.transpose.map { |(u0, u1)| u0 - u1 * q }
    pairs = [pairs.last, next_pair]
  end

  return pairs.first.map(&:-) if a < 0
  pairs.first
end
{% endhighlight %}
</div>

---
### testing

The `bezout` function is very simple to test since a solution must satisfy
the given equation.  However, you will want to ensure that your testing
includes inputs with negative values, since getting the signs right can
sometimes be tricky, depending on the implementation.  Make sure to test
negative values for input pairs like `(a, 0)`, `(0, b)`, or `(a, b)`
with $$ b \mid a, $$ for example.

{% highlight ruby %}
# ruby
def test_bezout(a, b)
  x, y = bezout(a, b)
  error = "`bezout` invalid for #{a}, #{b}"

  raise error unless a * x + b * y == gcd(a, b)
end
{% endhighlight %}

---
### applications

> **`proposition 7`**:
> Every common divisor of $$ a $$ and $$ b $$ divides the greatest common
> divisor.
{: .proposition}

> **`proof`**:
> This follows from two facts: that
> [a common divisor divides all linear combinations](divisibility#divides-linear-combinations)
> of $$ a $$ and $$ b $$ and that $$ \gcd(a, b) $$ can be expressed as a
> linear combination of $$ a $$ and $$ b $$ by Bezout's identity.
{: .proof}

