---
layout: section
title: greatest common divisor
chapter: 1
section: 3
prev: division-with-remainder
permalink: greatest-common-divisor
---

<span id="greatest-common-divisor" />
> **`definition`**:
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
$$ b $$ are equal to $$ 0. $$  The assumption for the rest of the section is
that at least one of them is nonzero.

The existence of a greatest common divisor stems from the following fact:
every pair of integers has at least one positive common divisor $$ 1, $$
and can only have finitely many positive common divisors since any
positive divisor of an integer is less than or equal to its absolute
value.

The greatest common divisor can be computed naively by finding the positive
divisors of each number and taking the intersection.  For example, to
compute $$ \gcd(154, 56) $$
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
  max = [a.abs, b.abs].max

  (1..max).each do |d|
    if a % d == 0 && b % d == 0
      divisor = d
    end
  end

  divisor
end
{% endhighlight %}

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
a simpler pair of numbers for computing the greatest common divisor.  The
**Euclidean algorithm** is repeated application of the division algorithm,
replacing $$ a, b $$ with $$ b, r $$ until reaching a remainder of $$ 0, $$
at which point the gcd is trivial to compute.

- $$ 154 = 56(2) + 42 $$ implies that $$ \gcd(154, 56) = \gcd(56, 42) $$
- $$ 56 = 42(1) + 14 $$ implies that $$ \gcd(56, 42) = \gcd(42, 14) $$
- $$ 42 = 14(3) + 0 $$ implies that $$ \gcd(42, 14) = 14, $$ since
$$ 14 \mid 42. $$

The series of equalities shows that $$ \gcd(154, 56) = 14 $$ without
explicitly computing any divisors.  In the Euclidean algorithm, the last
nonzero remainder is the gcd of the original two integers.

Here is another formulation of the Euclidean algorithm.

<span id="euclidean-algorithm" />
> **`Euclidean algorithm`**:
> To compute $$ \gcd(a, b) $$
> 1. If $$ b = 0, $$ return the absolute value of $$ a $$
> 2. Otherwise, compute $$ a = bq + r $$
> 3. Set $$ a = b $$ and $$ b = r $$ and return to step 1.

The Euclidean algorithm terminates after finitely many steps.  Since the
remainders form a decreasing sequence of positive integers, there are
can only be finitely many of them.

This new algorithm to compute the gcd is very fast: the growth is
logarithmic in the smaller of the two integers.  In fact, it can be shown
that the number of steps is at most 5 times the number of its decimal
digits.

In most programming languages, the modulus operator may return a negative
remainder when dealing with negative values.  However, the result of
`a % b` is still smaller than $$ b $$ in absolute value, so repeated
applications of the modulus operator will also terminate after finitely
many steps.  Since the proposition above applies regardless of whether
$$ a = bq + r $$ comes from the division algorithm, the Euclidean
algorithm may be implemented using only the modulus operator.

- `154 % 56 == 42` implies that $$ \gcd(154, 56) = \gcd(56, 42) $$
- `56 % 42 == 14` implies that $$ \gcd(56, 42) = \gcd(42, 14) $$
- `42 % 14 == 0` implies that $$ \gcd(42, 14) = 14 $$

The following are an iterative and a recursive implementation of the
Euclidean algorithm to compute the gcd.

{% highlight ruby %}
# ruby
def iterative_gcd(a, b)
  while b != 0
    a, b = [b, a % b]
  end
  a.abs
end

def recursive_gcd(a, b)
  return a.abs if b == 0
  recursive_gcd(b, a % b)
end
{% endhighlight %}

---
### think about it

1. Explain why $$ \gcd(0, 0) $$ is undefined.

---
### exercises
1. If $$ a $$ is nonzero, prove that $$ \gcd(a, 0) = \vert a \vert. $$

1. If $$ b \mid a, $$ prove that $$ \gcd(a, b) = \vert b \vert. $$

1. If $$ k $$ is nonzero, prove that $$ \gcd(ka, kb) = \gcd(a, b). $$

1. Write a Euclidean algorithm function that prints the division algorithm
result from each step used.  When run on the inputs `(154, 56)`, for
example, it should print:
<pre class="console">
154 == 56 * 2 + 42
56 == 42 * 1 + 14
42 == 14 * 3 + 0
</pre>
