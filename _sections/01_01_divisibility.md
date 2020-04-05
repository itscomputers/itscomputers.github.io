---
layout: section
title: divisibility
chapter: 1
section: 1
next: division-with-remainder
permalink: divisibility
---

<span id="1.1.1" />
> **`definition 1.1.1`**:
> We say that a nonzero integer $$ b $$ *divides* an integer $$ a $$ if there exists some
> integer $$ n $$ such that $$ a = bn. $$
{: definition}

Here are a few examples:
- $$ 15 $$ divides $$ 45 $$ since $$ 45 = 15 \cdot 3 $$
- $$ 9 $$ divides $$ 45 $$ since $$ 45 = 9 \cdot 5 $$
- $$ 10 $$ does not divide $$ 45 $$ since $$ 45 $$ is between
$$ 40 = 10 \cdot 4 $$ and $$ 50 = 10 \cdot 5 $$

Notice that the above definition is synonymous with saying that $$ b $$ may be
expressed as a multiple of $$ a. $$  In fact, the following statements are
equivalent and mean that $$ a = bn. $$
- $$ b $$ divides $$ a $$
- $$ a $$ is divisible by $$ b $$
- $$ a $$ is a multiple of $$ b $$

Although the three phrases have the same meaning, we will often use the first phrase.
The notation for this is $$ b \mid a, $$ which reads "$$ b $$ divides $$ a $$".  Using
this notation, the examples above are expressed as
- $$ 15 \mid 45 $$ since $$ 45 = 15 \cdot 3 $$
- $$ 9 \mid 45 $$ since $$ 45 = 9 \cdot 5 $$
- $$ 10 \nmid 45 $$ since $$ 10 \cdot 4 < 45 < 10 \cdot 5 $$

Be careful!  This notation may sometimes be confused with the division operation.
If you see $$ 15 / 45, $$ it is the operation that results in one third.
If you see $$ 15 \mid 45, $$ it is the statement that $$ 15 $$ divides $$ 45, $$
ie, that $$ 45 $$ is divisible by $$ 15, $$ ie, that $$ 45 / 15 $$ is an integer.

Here are a couple of propositions about integers that can be proved from the
definition of divisibility.

<span id="1.1.2" />
> **`proposition 1.1.2`**:
> If $$ d $$ divides both $$ a $$ and $$ b, $$ then $$ d $$ divides their sum.
{: .proposition}

> **`proof`**:
> Since $$ d \mid a, $$ there is an integer $$ m $$ such that $$ a = dm. $$  Similarly,
> since $$ d \mid b, $$ there is an integer $$ n $$ such that $$ b = dn. $$  Therefore,
> the sum $$ a + b $$ is equal to $$ dm + dn = d (m + n). $$  Since $$ m + n $$ is
> an integer, this equation implies that $$ d \mid (a + b). $$
{: .proof}

<span id="1.1.3" />
> **`proposition 1.1.3`**:
> If $$ d $$ divides either $$ a $$ or $$ b, $$ then $$ d $$ divides their product.
{: .proposition}

> **`proof`**:
> If $$ d \mid a, $$ then there is an integer $$ m $$ such that $$ a = dm, $$ so the product is
> $$ ab = (dm)b = d(mb), $$ which is a multiple of $$ d. $$
> Otherwise, $$ d \mid b, $$ in which case there is an integer $$ n $$ such that $$ b = dn, $$ so
> the product is $$ ab = a(dn) = d(an), $$ which is also a multiple of $$ d. $$
> Either way, $$ ab $$ is divisible by $$ d. $$
{: .proof}

---
### think about it:

1. Why is $$ b $$ required to be nonzero in <a href="#1.1.1">definition 1.1.1</a>?

1. Does an integer exist which divides every other integer?  If so, find the integer(s).

---
<span id="exercises" />
### exercises:

1. Prove that every integer divides $$ 0. $$

1. Prove that every integer divides itself.

1. If $$ a $$ and $$ b $$ are positive integers and $$ b $$ divides $$ a, $$ prove that $$ b $$ is less
than or equal to $$ a. $$

1. If two positive integers divide each other, prove that they are equal.

1. Prove that the `divides` relation is *transitive*.  In other words, if $$ c \mid b $$
and $$ b \mid a, $$ prove that $$ c \mid a. $$

1. Prove that the converse of <a href="#1.1.2">proposition 1.1.2</a> is false by
providing a counter-example.

1. Prove that the converse of <a href="#1.1.3">proposition 1.1.3</a> is false by
providing a counter-example.

1. If $$ d $$ divides both $$ a $$ and $$ b, $$ prove that $$ d $$ divides
any integer linear combination of $$ a $$ and $$ b. $$
(Note that an *integer linear combination* of $$ a $$ and $$ b $$ is defined to
be any integer of the form $$ ax + by, $$ where $$ x $$ and $$ y $$ are integers.)

1. Show that propositions <a href="#1.1.2">1.1.2</a> and <a href="#1.1.3">1.1.3</a>
are special cases of the previous exercise.

1. Write a function in the language of your choice that takes a pair of positive
integers $$ b, $$ $$ a $$ and returns `true` if $$ b \mid a $$ and `false` otherwise.  This function
should only use addition, multiplication, and comparison.
In ruby, your function might look something like this:

{% highlight ruby %}
def divides?(b, a)
  i = 0
  while m < a
    m += b
  end

  m == a
end
{% endhighlight %}

