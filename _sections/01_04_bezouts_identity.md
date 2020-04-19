---
layout: section
title: bezout's identity
chapter: 1
section: 4
prev: greatest-common-divisor
next: least-common-multiple
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
integers could be found by brute force.  In this case you might land on
the simplest example $$ (x, y) = (-2, 9). $$  However, the brute force
search might not be so successful so quickly.

> **`proof`**:
> Instead of proving Bezout's identity directly, it will be proved that
> that every remainder that occurs in the Euclidean algorithm can be
> expressed as a linear combination of the two integers.
>
> The Euclidean algorithm can be thought of as a sequence of equations
> of the form $$ i = j q + r. $$  If $$ i $$ and $$ j $$ are both linear
> combinations of $$ a $$ and $$ b, $$ then so is $$ r. $$  In particular,
> if $$ i = ax_0 + by_0 $$ and $$ j = ax_1 + by_1, $$ then
> $$ r = a(x_0 - qx_1) + b(y_0 - qy_1). $$  In the first instance,
> $$ i = a $$ and $$ j = b, $$ which are both linear combinations, namely
> $$ a = a(1) + b(0) $$ and $$ b = a(0) + b(1). $$  Therefore, the next
> remainder is a linear combination, implying the one after is, and so on.
{: .proof}

This proof is probably best illustrated with an example, say $$ a = 322 $$
and $$ b = 70. $$

|   `i` |  `j` | `q` |   `r` | `(x, y)`  |
|------:|-----:|----:|------:|----------:|
|       |      |     | `322` | `(1, 0)`  |
|       |      |     |  `70` | `(0, 1)`  |
| `322` | `70` | `4` |  `42` | `(1, -4)` |
|  `70` | `42` | `1` |  `28` | `(-1, 5)` |
|  `42` | `28` | `1` |  `14` | `(2, -9)` |
|  `28` | `14` | `2` |   `0` | `(-5, 23)`|

Ignoring the first two rows and the last column, this table has the same
information as the Euclidean algorithm, namely `i = j * q + r` always
holds.  The last column is how to express `r` as a linear combination,
namely `r = 322 * x + 70 * y` is always true.  The first two
$$ (x, y) $$ pairs show how to express `322` and `70` as linear
combinations of themselves.  After that, each pair is deduced from the
previous two pairs using the recursive relationships $$ x_2 = x_0 - qx_1 $$
and $$ y_2 = y_0 - qy_1. $$  In other words, the `q` value along with the
previous two $$ (x, y) $$ pairs is used to produce the next pair.

The second to last row is the one which gives a solution to Bezout's
identity, that $$ 322(2) + 70(-9) = \gcd(322, 70). $$  The time complexity
for this algorithm grows logarithmically just like the gcd algorithm.

---
### in code

The power of Bezout's identity lies in relating two integers to their gcd.
However, finding an actual solution also has some utility.  Using the
[division with remainder](division-with-remainder#ruby-division-with-remainder)
function a solution to Bezout's identity might look something like this.

<span id="ruby-bezout" />
{% highlight ruby %}
# ruby
def bezout(a, b)
  pairs = [[1, 0], [0, 1]]
  while b != 0
    q, r = division_with_remainder(a, b)
    a, b = b, r

    next_pair = pairs.transpose.map { |(u0, u1)| u0 - u1 * q }
    pairs = [pairs.last, next_pair]
  end
  pairs.first
end
{% endhighlight %}

<span id="rust-bezout" />
{% highlight rust %}
// rust
fn bezout_helper(a: i32, b: i32, prev: (i32, i32), curr: (i32, i32)) -> (i32, i32) {
  if b == 0 {
    return prev;
  }
  let (q, r) = division_with_remainder(a, b);
  let x = prev.0 - curr.0 * q;
  let y = prev.1 - curr.1 * q;

  bezout_helper(b, r, curr, (x, y))
}

fn bezout(a: i32, b: i32) -> (i32, i32) {
  bezout_helper(a, b, (1, 0), (0, 1))
}
{% endhighlight %}

You may also use a language's built-in modulus operator: even though it
may return a negative remainder, the algorithm still terminates in finitely
many steps and the relations from the proof still hold.

---
### testing

The `bezout` function is very simple to test.

{% highlight ruby %}
# ruby
def test_bezout(a, b)
  x, y = bezout(a, b)
  message = "`bezout` invalid for #{a}, #{b}"

  raise message unless a * x + b * y == gcd(a, b)
end
{% endhighlight %}

---
### applications

> **`proposition 7`**:
> Every common divisor of $$ a $$ and $$ b $$ divides the greatest common
> divisor.
{: .proposition}

> **`proof`**:
> Bezout's identity says that $$ \gcd(a, b) $$ can be expressed as a linear
> combination of $$ a $$ and $$ b. $$  A common divisor of $$ a $$ and
> $$ b $$ must divide $$ \gcd(a, b) $$ since every common divisor
> [divides all possible linear combinations](divisibility#divides-linear-combinations)
> of $$ a $$ and $$ b. $$
{: .proof}
