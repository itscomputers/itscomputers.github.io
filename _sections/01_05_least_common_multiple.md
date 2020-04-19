---
layout: section
title: least common multiple
chapter: 1
section: 5
prev: bezouts-identity
permalink: least-common-multiple
---

<span id="least-common-multiple" />
> **`definition`**:
> A *common multiple* of two integers $$ a $$ and $$ b $$ is an integer
> $$ m $$ such that $$ a \mid m $$ and $$ b \mid m. $$  The *least
> common multiple* of $$ a $$ and $$ b $$ is their smallest positive
> common multiple.
{: .definition}

- The notation for the least common multiple of $$ a $$ and $$ b $$ is
$$ \operatorname{lcm}(a, b). $$

- By definition, the least common multiple of two integers is independent
of the sign of the two integers --- the lcm is the same if you replace
$$ a $$ with $$ -a $$ or $$ b $$ with $$ -b. $$

- The definition of lcm does not make sense if either $$ a $$ or $$ b $$
are is equal to $$ 0. $$

The existence of a least common multiple stems from the fact that the
absolute value of the product of the two integers is a common multiple.

---
### naive computation

The least common multiple can be computed naively by checking every
multiple of one of them up to their product to see if it is divisible
by the other.  For example, to compute
$$ \operatorname{lcm}(154, 56) $$
- start with $$ 154 $$ and keep adding $$ 154 $$ until it is divisible by
$$ 56 $$
- $$ 56 $$ does not divide $$ 154, $$ $$ 154(2), $$ or $$154(3) $$
- however, $$ 154(4) = 616 = 56(11) $$ is divisible by $$ 56 $$
- the least common multiple is $$ \operatorname{lcm}(154, 56) = 616 $$

Programatically, this naive approach might look something like this.

{% highlight ruby %}
# ruby
def lcm(a, b)
  return if a == 0 || b == 0
  smaller, larger = [a, b].map(&:abs).sort

  multiple = larger
  while multiple % smaller != 0
    multiple += larger
  end

  multiple
end
{% endhighlight %}

The time complexity of this algorithm, similar to the naive gcd algorithm,
grows linearly in the smaller of the two arguments.

---
### relation to greatest common divisor

<span id="least-common-multiple" />
> **`proposition 5`**:
> If $$ a $$ and $$ b $$ are nonzero integers, then
> $$ \gcd(a, b) \cdot \operatorname{lcm}(a, b) = \vert ab \vert. $$
{: .proposition}

> **`proof`**:
> For simplicity, assume that $$ a $$ and $$ b $$ are positive.  Define
> $$ d = \gcd(a, b) $$ and $$ m = \operatorname{lcm}(a, b). $$ The goal
> is to prove $$ md = ab. $$
>
> Since the integer $$ ab/d $$ can be expressed as $$ (a/d) \cdot b $$
> or $$ a \cdot (b/d), $$ it must be a common multiple of $$ a $$
> and $$ b. $$  By definition of least common multiple, this means that
> $$ m \le ab/d. $$
>
>
{: .proof}

