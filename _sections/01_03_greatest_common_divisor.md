---
layout: section
title: greatest common divisor
chapter: 1
section: 3
prev: division-with-remainder
permalink: greatest-common-divisor
---

<span id="greatest-common-divisor" />
> **`definition 1.3.1`**:
> A *common divisor* of two integers $$ a $$ and $$ b $$ is an integer
> $$ d $$ such that $$ d \mid a $$ and $$ d \mid b. $$  The *greatest
> common divisor* of $$ a $$ and $$ b $$ is their largest positive
> common divisor.
{: definition}

- The notation for the greatest common divisor of $$ a $$ and $$ b $$ is
$$ \gcd(a, b). $$

- By definition, the greatest common divisor of two integers is independent
of the sign of the two integers --- the gcd is the same if you replace
$$ a $$ with $$ -a $$ or $$ b $$ with $$ -b. $$

- The definition of gcd does not make sense if both $$ a $$ and
$$ b $$ are equal to 0.  The assumption for the rest of the section is
that at least one of them is nonzero.

The existence of a greatest common divisor stems from the following fact:
every pair of integers has at least one positive common divisor $$ 1, $$
and can only have finitely many positive common divisors since any
positive divisor of an integer is less than or equal to its absolute
value.

The greatest common divisor can be computed naively by computing all
divisors and then comparing.  For example, to compute $$ \gcd(154, 56) $$
- the positive divisors of $$ 154 $$ are
$$ \{ 1, 2, 7, 11, 14, 22, 77, 154 \} $$
- the positive divisors of $$ 56 $$ are
$$ \{ 1, 2, 4, 7, 8, 14, 28, 56 \} $$
- the positive common divisors of $$ 154 $$ and $$ 56 $$ are
$$ \{ 1, 2, 7, 14 \} $$
- the greatest common divisor is $$ \gcd(154, 56) = 14 $$

Programatically, this naive approach might look something like this.

<span id="ruby-naive-gcd" />
{% highlight ruby %}
# ruby
def gcd(a, b)
  divisor = nil
  maximum = [a.abs, b.abs].max

  (1..maximum).each do |d|
    if a % d == 0 && b % d == 0
      divisor = d
    end
  end

  divisor
end
{% endhighlight %}

This gcd algorithm is extremely slow, growing linearly in the size of the
smaller of the two integers.  The next proposition is instrumental in
developing a more efficient algorithm to compute the gcd.

<span id="division-algorithm-and-gcd" />
> **`proposition 1.3.2`**:
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
a simpler pair of numbers for computing the greatest common divisor.  By
repeatedly applying the division algorithm, the problem of computing the
gcd eventually becomes trivial.

- $$ 154 = 56(2) + 42 $$ implies that $$ \gcd(154, 56) = \gcd(56, 42) $$
- $$ 56 = 42(1) + 14 $$ implies that $$ \gcd(56, 42) = \gcd(42, 14) $$
- $$ 42 = 14(3) + 0 $$ implies that $$ 14 \mid 42 $$
- Working backwards, $$ 14 = \gcd(42, 14) $$ implies that
$$ 14 = \gcd(56, 42) $$ which, in turn, implies that
$$ 14 = \gcd(154, 56). $$

Repeated use of the division algorithm to compute the greatest common
divisor is called the **Euclidean algorithm**.  In words, the last
nonzero remainder is the gcd of the original pair of integers.

<span id="euclidean-algorithm" />
> **`Euclidean algorithm`**:
> To compute $$ \gcd(a, b) $$
> 1. If $$ b = 0, $$ return the absolute value of $$ a $$
> 2. Otherwise, compute $$ a = bq + r $$
> 3. Set $$ a = b $$ and $$ b = r $$ and return to step 1.

This algorithm will terminate in finitely many steps as long as the second
step results in a remainder such that $$ |r| < |b|. $$  Although this
algorithm been framed in terms of the division algorithm where the
remainder is always positive, even modulus operators in computing that
return negative remainders will satisfy $$ |r| < |b|. $$

The example from above can be reformulated purely in terms of remainders.

- `156 % 56 ~> 42` implies that $$ \gcd(156, 56) = \gcd(56, 42) $$
- `56 % 42 ~> 14` implies that $$ \gcd(56, 42) = \gcd(42, 14) $$
- `42 % 14 ~> 0` implies that $$ \gcd(42, 14) = 14 $$

This formulation could be used to write a greatest common divisor function
either iteratively or recursively.

{% highlight ruby %}
# ruby
def iterative_gcd(a, b)
  a, b = [b, a % b] while b != 0
  a.abs
end

def recursive_gcd(a, b)
  return a.abs if b == 0
  recursive_gcd(b, a % b)
end
{% endhighlight %}

This new algorithm to compute the gcd is very fast: the growth is
logarithmic in the smaller of the two integers.  In fact, It can be shown
that the number of steps is at most 5 times the number of its decimal
digits.

---
### think about it

1. Explain why $$ \gcd(a, 0) = \vert a \vert $$ if $$ a $$ is nonzero.

1. Explain why $$ \gcd(0, 0) $$ is undefined.

---
### exercises

1. Write a Euclidean algorithm function that prints each of the division
algorithm results used to compute the gcd.  When run on the inputs
`(154, 56)`, for example, it should print:
<pre>
154 == 56 * 2 + 42
56 == 42 * 1 + 14
42 == 14 * 3 + 0
</pre>
