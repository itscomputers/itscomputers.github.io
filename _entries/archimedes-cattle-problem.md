---
layout: entry
category: notebook
title: archimedes' cattle problem
permalink: archimedes-cattle-problem
---

Around 2300 years ago, Archimedes developed a "BigInteger" scheme in order to
express integers larger than supported by the Greek numeral system, ie, larger
than a myriad-myriad = $$ 10^8. $$ His system is described in a paper he wrote called
The Sand Reckoner, where he calculated an upper bound of $$ 10^{63} $$
for the number of grains of sand that could fit in the known universe.

It was around this time that Archimedes sent a letter to a colleague in Egypt
with a problem that would surely strain any BigInteger system.

---
### the letter

If thou art diligent and wise, O stranger, compute the number of cattle of the
Sun, who once upon a time grazed on the fields of the Thrinacian isle of
Sicily, divided into four herds of different colours, one milk white, another a
glossy black, a third yellow and the last dappled. In each herd were bulls,
mighty in number according to these proportions: Understand, stranger, that the
white bulls were equal to a half and a third of the black together with the
whole of the yellow, while the black were equal to the fourth part of the
dappled and a fifth, together with, once more, the whole of the yellow. Observe
further that the remaining bulls, the dappled, were equal to a sixth part of
the white and a seventh, together with all of the yellow. These were the
proportions of the cows: The white were precisely equal to the third part and a
fourth of the whole herd of the black; while the black were equal to the fourth
part once more of the dappled and with it a fifth part, when all, including the
bulls, went to pasture together. Now the dappled in four parts were equal in
number to a fifth part and a sixth of the yellow herd. Finally the yellow were
in number equal to a sixth part and a seventh of the white herd. If thou canst
accurately tell, O stranger, the number of cattle of the Sun, giving separately
the number of well-fed bulls and again the number of females according to each
colour, thou wouldst not be called unskilled or ignorant of numbers, but not
yet shalt thou be numbered among the wise.

But come, understand also all these conditions regarding the cattle of the Sun.
When the white bulls mingled their number with the black, they stood firm,
equal in depth and breadth, and the plains of Thrinacia, stretching far in all
ways, were filled with their multitude. Again, when the yellow and the dappled
bulls were gathered into one herd they stood in such a manner that their
number, beginning from one, grew slowly greater till it completed a triangular
figure, there being no bulls of other colours in their midst nor none of them
lacking. If thou art able, O stranger, to find out all these things and gather
them together in your mind, giving all the relations, thou shalt depart crowned
with glory and knowing that thou hast been adjudged perfect in this species of
wisdom.

---
### the cattle problem

Translating the letter, there are four colors of cattle: black, white, yellow,
and dappled. We label the bulls by the lower-case letters `b`, `w`, `y`, `d`
and the cows by the upper-case letters `B`, `W`, `Y`, `D`. The problem is given
in two parts.

#### part 1

The first paragraph translates to a system of 7 linear of equations in 8 variables.

| linear system                                                |
|:-------------------------------------------------------------|
| $$ w = \left( \dfrac{1}{2} + \dfrac{1}{3} \right) b + y $$   |
|--------------------------------------------------------------|
| $$ b = \left( \dfrac{1}{4} + \dfrac{1}{5} \right) d + y $$   |
|--------------------------------------------------------------|
| $$ d = \left( \dfrac{1}{6} + \dfrac{1}{y} \right) w + y $$   |
|--------------------------------------------------------------|
| $$ W = \left( \dfrac{1}{3} + \dfrac{1}{4} \right) (b + B) $$ |
|--------------------------------------------------------------|
| $$ B = \left( \dfrac{1}{4} + \dfrac{1}{5} \right) (d + D) $$ |
|--------------------------------------------------------------|
| $$ D = \left( \dfrac{1}{5} + \dfrac{1}{6} \right) (y + Y) $$ |
|--------------------------------------------------------------|
| $$ Y = \left( \dfrac{1}{6} + \dfrac{1}{7} \right) (w + W) $$ |

Clearing denominators results in a system of 7 linear integer equations.

| linear system         |
|:----------------------|
| $$ 6w = 5b + 6y $$    |
|-----------------------|
| $$ 20b = 9b + 20y $$  |
|-----------------------|
| $$ 42d = 13b + 42y $$ |
|-----------------------|
| $$ 12W = 7b + 7B $$   |
|-----------------------|
| $$ 20B = 9d + 9D $$   |
|-----------------------|
| $$ 30D = 11y + 11Y $$ |
|-----------------------|
| $$ 42Y = 13w + 13W $$ |

This is an underdetermined system, so there are infinitely many integer solutions.
A solution can be found either using algebraic manipulations or by reducing the
following matrix to its reduced-row-echelon form.

{% highlight ruby %}
[[  6,  -5,   0,  -6,   0,   0,   0,   0],
 [  0,  20,  -9, -20,   0,   0,   0    0],
 [-13,   0,  42, -42,   0,   0,   0,   0],
 [  0,  -7,   0,   0,  12,  -7,   0,   0],
 [  0,   0,  -9,   0,   0,  20,  -9,   0],
 [  0,   0,   0, -11,   0,   0,  30, -11],
 [-13,   0,   0,   0, -13,   0,   0,  42]]
{% endhighlight %}

Reducing the matrix and computing the null-space will result in a vector with
one free parameter.  After clearing denominators to get integer solutions,
or after solving via algebraic manipulations, you will end up with the
the following solution.

| $$ k = $$  any integer        |
|:------------------------------|
| $$ w = 10355482 \cdot k $$    |
|-------------------------------|
| $$ b = 7460514 \cdot k $$     |
|-------------------------------|
| $$ d = 7358060 \cdot k $$     |
|-------------------------------|
| $$ y = 4149387 \cdot k $$     |
|-------------------------------|
| $$ W = 7206360 \cdot k $$     |
|-------------------------------|
| $$ B = 4893246 \cdot k $$     |
|-------------------------------|
| $$ D = 3515820 \cdot k $$     |
|-------------------------------|
| $$ Y = 5439213 \cdot k $$     |
|-------------------------------|
| Total $$ =50389082 \cdot k $$ |

The smallest solution has `50,389,082` cattle, but Archimedes is unimpressed. We
are, by his accounting, not entirely unskilled in mathematics!

#### part 2

In the second paragraph, Archimedes imposes two additional conditions. The
first condition is that $$ w + b $$ must a square number. Using the computed solution,
we know that

$$ w + b = 17826996 \cdot k = 2^2 \cdot 3 \cdot 11 \cdot 29 \cdot 4657 \cdot k. $$

In order for this to be a square number,
$$ k $$ must equal $$ 3 \cdot 11 \cdot 29 \cdot 4657 $$
multiplied by a square number, ie, there must be some integer $$ t $$ such that

$$ k = 957 \cdot 4657 \cdot t^2. $$

The second condition is that $$ d + y $$ must be a triangular number.  Using the
computed solutions above and the value of $$ k, $$ we get

$$ d + y = 2471 \cdot 4657 \cdot k = 957 \cdot 2471 \cdot (4657t)^2. $$

For this to be a triangular number, it must equal $$ m (m + 1) / 2 $$ for some
integer $$ m. $$  In other words,

$$ m^2 - m - 2 \cdot 957 \cdot 2471 \cdot (4657t)^2 = 0. $$

The quadratic formula implies that

$$ m = { -1 + \sqrt{1 + 2 \cdot 957 \cdot 2471 \cdot (9314t)^2} \over 2 }, $$

or equivalently, putting $$ v = 9314 t, $$

$$ m = { -1 + \sqrt{ 1 + 4729494 v^2 } \over 2 }. $$

In order for this to be an integer, the inside of the square root must be a
perfect square, say $$ u^2. $$  Therefore, we are left trying to find an
integer solution $$ (u, v) $$ to $$ u^2 - 4729494 v^2 = 1, $$ where $$ v $$ is
divisible by $$ 9314. $$

In modern mathematics, an equation of this sort is called Pell's equation.  It
was misattributed to John Pell, who never worked on the problem.  Long before
being misnamed though, these equations were studied by the Ancient Greeks and
then solved by Indian mathematicians.

---
### continued fractions

The continued fraction algorithm begins with a real number $$ \alpha, $$
computes its integer part called the quotient $$ q, $$ and its fractional part
$$ \beta = \alpha - q. $$  This $$ \beta $$ is between $$ 0 $$ and $$ 1, $$
so it's reciprocal is greater than $$ 1. $$

At each iteration of the algorithm, $$ \alpha $$ is replaced by the reciprocal
of $$ \beta $$ and the same process is applied.  This procdure is continued
indefinitely or until $$ \beta $$ is equal to $$ 0. $$ The pseudo-code for the
continued fraction algorithm is as follows.

{% highlight ruby %}
loop do
  beta = alpha - alpha.floor
  if beta == 0
    break
  else
    alpha = beta.reciprocal
  end
end
{% endhighlight %}

If $$ \alpha $$ is a rational number, the algorithm is essentially equivalent
to the Euclidean algorithm and terminates after finitely many steps.  Otherwise,
the algorithm is infinite.

The name continued fraction stems from the fact that the quotients in the
algorithm can be used to express $$ \alpha $$ as an "infinite fraction". In
particular, indexing the quotients as $$ q_0, q_1, q_2,... $$ results in

$$ \alpha = q_0 + \cfrac{ 1 }{ q_1 + \cfrac{ 1 }{ q_2 + \cfrac{ 1 }{ \ddots } } }. $$

When $$ \alpha = \sqrt{R} $$ for some non-square integer $$ R, $$ it turns out
that the sequence of quotients in periodic.  For example, the continued fraction
algorithm for $$ \alpha = \sqrt{33} $$ is the following.

|                      $$ \alpha $$ |  $$ q $$ |                        $$ \beta $$ |
|----------------------------------:|---------:|-----------------------------------:|
|                   $$ \sqrt{33} $$ |  $$ 5 $$ |               $$ -5 + \sqrt{33} $$ |
|-----------------------------------|----------|------------------------------------|
| $$ \frac58 + \frac18 \sqrt{33} $$ |  $$ 1 $$ | $$ -\frac38 + \frac18 \sqrt{33} $$ |
|-----------------------------------|----------|------------------------------------|
|       $$ 1 + \frac13 \sqrt{33} $$ |  $$ 2 $$ |       $$ -1 + \frac13 \sqrt{33} $$ |
|-----------------------------------|----------|------------------------------------|
| $$ \frac38 + \frac18 \sqrt{33} $$ |  $$ 1 $$ | $$ -\frac58 + \frac18 \sqrt{33} $$ |
|-----------------------------------|----------|------------------------------------|
|               $$ 5 + \sqrt{33} $$ | $$ 10 $$ |               $$ -5 + \sqrt{33} $$ |

The $$ \beta $$ in the last row shown is the same as the $$ \beta $$ in the
first row.  This implies that these last 4 rows will repeat indefinitely.
The quotients will be $$ 5, 1, 2, 1, 10, 1, 2, 1, 10, 1, 2, 1, 10, \dots $$
which we abbreviate as $$ \sqrt{33} = [5; 1, 2, 1, 10] $$  The semicolon
separates the initial part from the periodic part.

The same pattern holds in general: for $$ \alpha = \sqrt{R}, $$ the algorithm
only needs to run until $$ \alpha = q_0 + \sqrt{R}. $$  The proof of this fact
can be found in many elementary number theory books.

In order to do this programatically, we need to track the arithmetic of
subtracting floor and then inverting a quadratic rational number.  In order to
take the reciprocal, the denominator must be rationalized and the result must
be reduced by any common factors.  We will represent the quadratic rational
$$ (a + b \sqrt{R}) / c $$ by the tuple $$ (a, b, c). $$

Subtracting the quotient:

$$ { a + b \sqrt{R} \over c } - q = { (a - qc) + b \sqrt{R} \over c } $$

Inverting:

$$ { c \over (a - qc) + b \sqrt{R} }
  = { c(a - qc) - bc \sqrt{R} \over (a - qc)^2 - b^2R } $$

$$ { c \over (a - qc) + b \sqrt{R} }
  = { c(qc - a) + bc \sqrt{R} \over b^2R - (qc - a)^2 } $$

Therefore, the transformation on the tuple $$ (a, b, c) $$ is the following.

| transformation                                  |
|:------------------------------------------------|
| $$ a \mapsto (q \cdot c - a) \cdot c $$         |
|-------------------------------------------------|
| $$ b \mapsto b \cdot c $$                       |
|-------------------------------------------------|
| $$ c \mapsto b^2 \cdot R - (q \cdot c - a)^2 $$ |

The only thing left is to reduce by any common factors.  The pseudo-code for
the continued fraction algorithm might look something like this.

{% highlight ruby %}
def continued_fraction(root) do
  q0 = sqrt(root).floor
  alpha = (0, 1, 1)
  quotients = []

  while alpha != (q0, 1, 1) do
    a, b, c = alpha
    q = ((a + b * q0) / c).floor
    a = q * c - a
    b = b * c
    c = b**2 * root - (q * c - a)**2
    d = gcd(a, b, c)

    alpha = (a/d, b/d, c/d)
    quotients.push(q)
  end

  return quotients
end
{% endhighlight %}

Back to the cattle problem, using this or some equivalent continued fraction
algorithm implementation, we can compute the continued fraction for $$
\sqrt{4729494}. $$  It turns out to have a period of 92.  The first ten
quotients are $$ [2174, 1, 2, 1, 5, 2, 25, 3, 1, 1, ...]. $$

---
### convergents

The convergents of a continued fraction are the rational numbers obtained using
finitely many of the quotients.  The first few convergents for the example
above are the following.

|                                                     $$ \sqrt{33} = [5; 1, 2, 1, 10] $$ |
|---------------------------------------------------------------------------------------:|
|                                                                 $$ 5 = \dfrac{5}{1} $$ |
|----------------------------------------------------------------------------------------|
|                                                  $$ 5 + \cfrac{1}{1} = \dfrac{6}{1} $$ |
|----------------------------------------------------------------------------------------|
|                                  $$ 5 + \cfrac{1}{1 + \cfrac{1}{2}} = \dfrac{17}{3} $$ |
|----------------------------------------------------------------------------------------|
|                   $$ 5 + \cfrac{1}{1 + \cfrac{1}{2 + \cfrac{1}{1}}} = \dfrac{23}{4} $$ |
|----------------------------------------------------------------------------------------|
| $$ 5 + \cfrac{1}{1 + \cfrac{1}{2 + \cfrac{1}{1 + \cfrac{1}{10}}}} = \dfrac{247}{43} $$ |

These rational numbers are approximations to $$ \sqrt{33}. $$  The
approximations alternate between under- and over-estimates and grow more
accurate as we go.

---
### pell's equation

Finding integer solutions to an equation of the form $$ u^2 - R v^2 = 1 $$ is
known as solving Pell's equation.

The Indian mathematician Brahmagupta (~600 CE) developed an identity to derive
infinitely many solutions of Pell's equation from a single solution. He was
also able to find solutions to some notoriously difficult examples.

Bhaskara II (~1150 CE) extended Brahmagupta's techniques to develop his "Circle
Method", which was capable of solving any instance of Pell's equation.

But it wasn't until 1768 that Lagrange proved that Bhaskara's method will always
terminate after finitely many steps and yield a solution. Lagrange used
continued fractions for his proof.

In particular, Lagrange was able to prove that the convergent right before the
end of the period of quotients can be used to produce a solution to Pell's
equation.

In the example above, the convergent of interest is $$ 23 / 4 $$.  The
numerator and denominator $$ (23, 4) $$ form a solution to
$$ u^2 - 33 v^2 = 1. $$  In the general case, the convergent may form a
solution to $$ u^2 - 33 v^2 = -1, $$ in which case the convergent at the end of
the second period will form a solution to Pell's equation itself.

In order to calculate the convergents efficiently, we use another property of
the continued fraction of $$ \sqrt{R}, $$ namely that the numerators and
denominators of the convergents both satisfy the same recurrence relation:
`next_value = quotient * current_value + previous_value`.

Here is a modified version of the pseudo-code for the continued fraction
algorithm that also records convergents as we go.

{% highlight ruby %}
def continued_fraction(root) do
  q0 = sqrt(root).floor
  alpha = (0, 1, 1)
  quotients = []
  convergents = [(0, 1), (1, 0)]

  while alpha != (q0, 1, 1) do
    a, b, c = alpha
    q = ((a + b * q0) / c).floor
    a = q * c - a
    b = b * c
    c = b**2 * root - (q * c - a)**2
    d = gcd(a, b, c)

    alpha = (a/d, b/d, c/d)

    prev_conv = convergents[-2]
    curr_conv = convergents[-1]
    next_conv = (q * curr_conv[0] + prev_conv[0], q * curr_conv[1] + prev_conv[1])

    quotients.push(q)
    convergents.push(next_conv)
  end

  return (quotients, convergents)
end

{% endhighlight %}

---
### producing all solutions from a first

The last ingredient we need to solve Archimedes' cattle problem is the identity
that Brahmagupta found to produce more solutions from a single solution.  This
identity can be framed in modern terms as follows: if $$ (a, b) $$ is the
smallest integer solution (found using the continued fraction convergents) to
$$ u^2 - R v^2 = 1, $$ then **every** solution is of the form $$ (A, B), $$
where $$ (a + b \sqrt{R})^n = A + B \sqrt{R} $$ for a positive integer $$ n. $$

Using the example of $$ R = 33 $$ again, we can compute powers to find new
solutions to Pell's equations.

|                      power |                  computation |            solution |
|---------------------------:|-----------------------------:|--------------------:|
| $$ (23 + 4 \sqrt{33})^1 $$ |       $$ 23 + 4 \sqrt{33} $$ |       $$ (23, 4) $$ |
|----------------------------|------------------------------|---------------------|
| $$ (23 + 4 \sqrt{33})^2 $$ |   $$ 1057 + 184 \sqrt{33} $$ |   $$ (1057, 184) $$ |
|----------------------------|------------------------------|---------------------|
| $$ (23 + 4 \sqrt{33})^3 $$ | $$ 48599 + 8460 \sqrt{33} $$ | $$ (48599, 8460) $$ |

Computing powers programatically will rely on the arithmetic of multiplying two
quadratic integers.

$$ (a + b \sqrt{r}) \cdot (c + d \sqrt{r})
  = (ac + rbd) + (ad + bc) \sqrt{r} $$

Using this, the pseudo code for exponentiation might look something like this.

{% highlight ruby %}
def multiply(root, (a, b), (c, d)) do
  return (a * c + b * d * root, a * d + b * c)
end

def power(root, (a, b), exponent) do
  if exponent == 0
    return (1, 0)
  elseif exponent == 1
    return (a, b)
  else
    half_power = power(root, (a, b), exponent/2)
    half_power_squared = multiply(root, half_power, half_power)

    if exponent % 2 == 0
      return half_power_squared
    else
      return multiply(root, (a, b), half_power_squared)
    end
  end
end
{% endhighlight %}

---
### the solution to the cattle problem

Recall that we need to find a solution to $$ u^2 - 4729494 v^2 = 1 $$ such that
$$ v $$ is divisible by 9314.  Using the continued fraction (which has a period
of 92) and its convergents, we arrive at a first solution $$ (a, b) $$ with

$$ a = 109931986732829734979866232821433543901088049 $$

$$ b = 50549485234315033074477819735540408986340 $$

Amthor in fact computed this by hand in 1880.  He was also able to prove that
the 2329th power of $$ a + b \sqrt{4729494} $$ is the one where $$ v $$ is
finally divisible by 9314.

In particular, if $$ (a + b \sqrt{4729494})^{2329} = A + B \sqrt{4729494}, $$
Amthor used logarithms to show that $$ A $$ has `103,273` digits and $$ B $$
has `103,270` digits.  Setting $$ t = B / 9314, $$ we have

$$ k = 957 \cdot 4657 t^2 = { 957 \cdot B^2 \over 2 \cdot 9314 } $$

so the total number of cattle is

$$ 50389082 \cdot k = { 50389082 \cdot 957 \cdot B^2 \over 18628 } $$

which has `206,545` digits!!

The first and last fifty digits of the smallest solution to Archimedes' cattle
problem are

$$ 77602714064868182695302328332138866642323224059233 \dots $$

$$ \dots 05994630144292500354883118973723406626719455081800 $$

---
### epilogue

As mentioned, Amthor was able to find the exact solution by hand in 1880, but
was unable to compute the solution.  He correctly computed the number of digits
and calculated the first four digits to be `7766`.  The first three of his
digits were correct.

In 1965, mathematicians Williams, German, and Zarnke at the University of
Waterloo used an IBM 7040 and an IBM 1620 to compute the full solution.  It
took 7:49 hours.  They published their methods in the Mathematics of Computation.
The number itself was deposited in the unpublished mathematical tables of the
journal.

In 1981, Harry Nelson used a Cray-1 computer at Livermore National Laboratory
to compute and verify the solution in about 10 minutes.  He published the
result with 1/3 font size on 47 pages of the Journal of Recreational
Mathematics.

---
### bang bang con west (feb 2020)

I gave a 10-minute soap opera version of this as a talk at !!con west in
februrary of 2020.  At the end of the talk, I used a 2017 13in MacBook Pro to
compute the solution in a tenth of a second using some ruby code that I wrote.

- <a href="https://github.com/itscomputers/archimedes-cattle-problem/blob/master/cattle.rb">
    ruby code on github</a>
- <a href="https://youtu.be/BVYotbZuiDY">
    video of my !!con west talk</a>

