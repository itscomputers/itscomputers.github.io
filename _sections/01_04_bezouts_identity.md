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

---
### example 1

For example, if $$ a = 322 $$ and $$ b = 70, $$ Bezout's identity implies
that $$ 322x + 70y = 14 $$ for some integers $$ x $$ and $$ y. $$  Such
integers might be found by brute force.  In this case, a brute force
search might arrive at the simplest solution $$ (x, y) = (-2, 9). $$
However, the Euclidean algorithm provides an efficient way to find a
solution.

The first division algorithm yields $$ 322 = 70(4) + 42, $$ giving a
quotient of $$ q_0 = 4 $$ and a remainder of $$ r_0 = 42. $$  Solving for
$$ r_0 $$ gives $$ 42 = 322 - 70(4). $$  In particular, the remainder
$$ r_0 $$ can be expressed as a linear combination of $$ 322 $$ and
$$ 70, $$ namely $$ r_0 = 322(1) + 70(-4). $$

The second division algorithm yields $$ 70 = 42(1) + 28 $$ with a quotient
of $$ q_1 = 1 $$ and $$ r_1 = 28. $$  Solving for $$ r_1 $$ gives
$$ 28 = 70 - 42(1). $$  The linear combination for $$ 42 $$ may be
substituted here and simplified to $$ 28 = -322 + 70(5). $$  Therefore,
the remainder $$ r_1 = 322(-1) + 70(5) $$ is also a linear combination
of the original two integers.

The third division algorithm gives $$ 42 = 28(1) + 14 $$ with a quotient
of $$ q_2 = 1 $$ and $$ r_2 = 28. $$  The linear combinations can be
substituted for $$ 42 $$ and $$ 28, $$ which will then simplify to
$$ 14 = 322(2) + 70(-9), $$ which is the solution to Bezout's identity
that was found by brute force.

These computations are summarizedin the table below. In each of the first
three rows, the last column is how to express `r` as a linear combination
of the original $$ 322 $$ and $$ 70, $$ namely, $$ r = 322x + 70y. $$
The last row verifies that the algorithm has terminated, ie, that the
gcd of $$ 322 $$ and $$ 70 $$ is the second-to-last remainder $$ 14. $$

|  `a'` | `b'` |   `r` | `q` |  `(x, y)` |
|------:|-----:|------:|----:|:----------|
| `322` | `70` |  `42` | `4` | `(1, -4)` |
|  `70` | `42` |  `28` | `1` | `(-1, 5)` |
|  `42` | `28` |  `14` | `1` | `(2, -9)` |
|  `28` | `14` |   `0` | `2` |           |

We would like a programatic way to compute the $$ (x, y) $$ pairs as we
go.  Suppose that on some row we have $$ a' = b'q + r $$ and that we have
already calculated that $$ a' = 322 x_0 + 70 y_0 $$ and
$$ b' = 322 x_1 + 70 y_1. $$  We can substitute these expressions into
the division algorithm equation to get
$$ 322 x_0 + 70 y_0 = (322 x_1 + 70 y_1)q + r. $$  Solving for $$ r $$
and rearranging, we get $$ r = 322 (x_0 - x_1 q) + 70(y_0 - y_1 q). $$

This is great news, because we can compute the the next $$ (x, y) $$
pair from the previous two pairs.  The recursive relation for both $$ x $$
and $$ y $$ can be expressed as $$ u_2 = u_0 - u_1 \cdot q. $$  In other
words, the next value is the previous value minus the quotient multiplied
by the current value.

We augment the table above keep track of the previous, the current, and
the next $$ (x, y) $$ pairs.


|  `a'` |  `b'` |   `r` | `q` | `a': (x, y)` | `b': (x, y)` | `r: (x, y)` |
|------:|------:|------:|----:|-------------:|-------------:|------------:|
| `322` |  `70` |  `42` | `4` |     `(1, 0)` |     `(0, 1)` |   `(1, -4)` |
|  `70` |  `42` |  `28` | `1` |     `(0, 1)` |    `(1, -4)` |   `(-1, 5)` |
|  `42` |  `28` |  `14` | `1` |    `(1, -4)` |    `(-1, 5)` |   `(2, -9)` |
|  `28` |  `14` |   `0` | `2` |    `(-1, 5)` |    `(2, -9)` |             |

In this table, the final three columns show how to express `a'`, `b'`, and
`r` as linear combinations of `322` and `70`.  The first row has the
the initial conditions for the recursive algorithm.  The first two pairs
are obtained by observing that $$ 322 = 322(1) + 70(0) $$ and
$$ 70 = 322(0) + 70(1). $$

If we think of the `a'` pair as the previous `(x, y)`, the `b'` pair as the
 current `(x, y)`, then the `x` and `y` for `r` can be computed using the
relation `next = prev - curr * q`.  In the first row, for example, we
calculate the next `x` and `y` by `next = prev - curr * q`.  In the `x`
case we get `next_x = 1 - 0 * 4 = 1`, and in the `y` case we get
`next_y = 0 - 1 * 4 = -4`.

---
### example 2

Here is another example to illustrate this process.  Suppose we want to
find a solution to $$ 5831 x + 482 y = \gcd(5831, 482). $$ The initial
conditions are populated in the table as follows.

|   `a'` |   `b'` |   `r` | `q` | `a': (x, y)` | `b': (x, y)` | `r: (x, y)` |
|-------:|-------:|------:|----:|-------------:|-------------:|------------:|
| `5831` |  `482` |       |     |     `(1, 0)` |     `(0, 1)` |             |

The division algorithm yields $$ 5831 = 482(12) + 47. $$  We calculate the
next `(x, y)` pair using `next = curr - prev * q` with $$ q = 12. $$  So
`next_x = 1 - 0 * 12 = 1` and `next_y = 0 - 1 * 12 = -12`.  Fill these values into
the table and being the next row as follows.

|   `a'` |   `b'` |   `r` |  `q` | `a': (x, y)` | `b': (x, y)` | `r: (x, y)` |
|-------:|-------:|------:|-----:|-------------:|-------------:|------------:|
| `5831` |  `482` |  `47` | `12` |     `(1, 0)` |     `(0, 1)` |  `(1, -12)` |
|  `482` |   `47` |       |      |     `(0, 1)` |   `(1, -12)` |             |

The division algorithm on $$ 482 $$ and $$ 47 $$ has a quotient
$$ q = 10 $$ and a remainder $$ r = 12. $$ Therefore,
`next_x = 0 - 1 * 10 = -10` and `next_y = 1 - (-12) * 10 = 121`.
You can verify here that $$ 12 = 5831(-10) + 482(120). $$

|   `a'` |   `b'` |   `r` |  `q` | `a': (x, y)` | `b': (x, y)` |  `r: (x, y)` |
|-------:|-------:|------:|-----:|-------------:|-------------:|-------------:|
| `5831` |  `482` |  `47` | `12` |     `(1, 0)` |     `(0, 1)` |   `(1, -12)` |
|  `482` |   `47` |  `12` | `10` |     `(0, 1)` |   `(1, -12)` | `(-10, 121)` |
|   `47` |   `12` |       |      |   `(1, -12)` | `(-10, 121)` |              |

The division algorithm on $$ 47 $$ and $$ 12 $$ has a quotient $$ q = 3 $$
and a remainder $$ r = 11. $$  So, `next_x = 1 - (-10) * 3 = 31` and
`next_y = -12 - 121 * 3 = -375`.  Again, you can verify that
$$ 11 = 5831(31) + 482(-375). $$

|   `a'` |   `b'` |   `r` |  `q` | `a': (x, y)` | `b': (x, y)` |  `r: (x, y)` |
|-------:|-------:|------:|-----:|-------------:|-------------:|-------------:|
| `5831` |  `482` |  `47` | `12` |     `(1, 0)` |     `(0, 1)` |   `(1, -12)` |
|  `482` |   `47` |  `12` | `10` |     `(0, 1)` |   `(1, -12)` | `(-10, 121)` |
|   `47` |   `12` |  `11` |  `3` |   `(1, -12)` | `(-10, 121)` | `(31, -375)` |
|   `12` |   `11` |       |      | `(-10, 121)` | `(31, -375)` |              |

The division algorithm on $$ 12 $$ and $$ 11 $$ has a quotient $$ q = 1 $$
and a remainder $$ r = 1. $$  So, `next_x = -10 - 31 * 1 = -41` and
`next_y = 121 - (-375) * 1 = 496`.  You can verify that
$$ 1 = 5831(-41) + 482(496). $$
The algorithm terminates here, because the next remainder will be 0.

|   `a'` |   `b'` |   `r` |  `q` | `a': (x, y)` | `b': (x, y)` |  `r: (x, y)` |
|-------:|-------:|------:|-----:|-------------:|-------------:|-------------:|
| `5831` |  `482` |  `47` | `12` |     `(1, 0)` |     `(0, 1)` |   `(1, -12)` |
|  `482` |   `47` |  `12` | `10` |     `(0, 1)` |   `(1, -12)` | `(-10, 121)` |
|   `47` |   `12` |  `11` |  `3` |   `(1, -12)` | `(-10, 121)` | `(31, -375)` |
|   `12` |   `11` |   `1` |  `1` | `(-10, 121)` | `(31, -375)` | `(-41, 496)` |
|   `11` |    `1` |   `0` | `11` | `(31, -375)` | `(-41, 496)` |              |

We arrive at the solution $$ (x, y) = (-41, 496) $$ to the equation
$$ 5831x + 482y = 1. $$

---
### in code

The examples above can be generalized into a constructive proof of Bezout's
identity -- this constructive proof is also an algorithm to produce
a solution.

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

  a < 0 ? pairs.first.map(&:-) : pairs.first
end
{% endhighlight %}
</div>

---
### testing

The `bezout` function is very simple to test since a solution must satisfy
the Bezout's identity.

{% highlight ruby %}
# ruby
def test_bezout(a, b)
  x, y = bezout(a, b)
  error = "`bezout` invalid for #{a}, #{b}"

  raise error unless a * x + b * y == gcd(a, b)
end
{% endhighlight %}

There are some edge cases that may add some complexity to your function
arising from how to handle negative inputs.  Inputs you may want to
specifically test might include
1. `(a, 0)` with `a < 0`
2. `(0, b)` with `b < 0`
3. `(a, b)` with `a < 0`
4. `(a, b)` with `b < 0`
5. `(a, b)` with `a < 0` and `a % b == 0`
6. `(a, b)` with `b < 0` and `a % b == 0`

