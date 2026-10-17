# Analysis 1

## Introduction

This intro is probably going to be very sparse; most of it was course structure and basic definitions.
You'll notice me jump around a lot because there were periods of less information.

A couple hard one-liners from the first lecture:

- "The devil lies in the three dots $\cdots$"
- "Mathematicians often abstract things that are obvious in order to essentialise their features."
- "I explain never again."

## Important fields (not for drinking in)

Gracefully, we take $0 \notin \mathbb N$.

$m + x = n$ does not have an $x \in \mathbb N$ that solves it $\forall m, n \in \mathbb N$.
For that, we need $\mathbb Z$ to extend $\mathbb N$ with additive inverses (negative numbers).

Similarly, $m \cdot x = n$ does not have an $x \in \mathbb Z$ that solves it $\forall m, n \in \mathbb Z$.
For that, we need $\mathbb Q$ to extend $\mathbb N$ with multiplicative inverses (fractions).
The rationals are defined as $\left\\{\frac p q, \\ p, q \in \mathbb Z, \\ q \ne 0\right\\}$.

Again, $x^m = n$ (when $n > 0$) needs $\mathbb R$ to solve because it provides us with radicals.
When $n \in \mathbb R$, $x^m = n$ needs $\mathbb C$ to solve because we need complex numbers.

## Our first theorem 🤩

To nobody's surprise, we're going to prove that root 2 is irrational.

**Theorem.** There is no $x \in \mathbb Q$ s.t. $x^2 = 2$.

**Lemma.** If $n^2$ is even and $n \in \mathbb N$, $n$ is even.

**Proof.** We will show the contrapositive, that if $m$ is odd, then $m^2$ is odd.

$$
\begin{align}
m &= 2k + 1 \\\
m^2 &= \left(2k+1\right)^2 \\\
&= 4k^2 + 4k + 1 \\\
&= 2\left(2k^2 + 2k\right) + 1 \\\
&\implies m^2 \text{ is odd}
\end{align}
$$

I don't remember why contrapositives work, but trust me. $\square$

Now that we've proved our lemma, we can prove our actual statement.

**Proof.** Assume $\exists x \in \mathbb Q$ s.t. $x^2 = 2$. WLOG, $x = \frac p q$ uniquely, 
where $p, q \in \mathbb N$ and $p, q$ are coprime.

$$
\begin{align}
x^2 &= 2 \\\
\frac {p^2} {q^2} &= 2 \\\
p^2 &= 2 q^2 \\\
\end{align}
$$

$p^2$ is even $\implies$ $p$ is even by our lemma, so we can write $p = 2k$.

$$
\begin{align}
2q^2 &= p^2 \\\
2q^2 &= 4k^2 \\\
q^2 &= 2k^2 \\\
\end{align}
$$

So $q^2$ is also even, and then $q$ is even. However, if $p$ and $q$ are both even,
then they cannot be coprime; and so, there is no unique expression of the solution
to $x^2 = 2$ as a fraction $\frac p q$. $\square$ (idk how to do the contradiction symbol).

> This proof is pretty clearly generalisable to all $\sqrt p$ of primes, since
that's where our lemma applies. From there though, I don't know you would prove
the irrationality of other non-square numbers.

## If not, then oh well

$$\text{Car Seat Headrest --- Disjecta Membra}$$

We can't express $\sqrt 2$ as a rational, but we can have fun trying to get close.

If we want $\frac p q \approx \sqrt 2$, then our error/distance 
$\left|\frac{p^2}{q^2} - 2\right|$ 
should be minimised --- equivalently, we could minimise
$\left|p^2 - 2q^2\right|$.

We've now seen that with $p, q \in \mathbb N$, we cannot get $\left|p^2 - 2q^2\right| = 0$;
but can we get $\left|p^2 - 2q^2\right| = 1$? 

> This alternate "good enough" formula for the approximation of $\sqrt 2$ using
number theory is called **Pell's equation**.

We need a way to quantify the level of accuracy we get by approximating with a certain
$(p, q)$; what can we say about our error in terms of $p$ and $q$?
Watch closely, because I'm about to pull
the most bullshit rearrangements in the name of *analysis*.
We need to get an expression for $|\frac p q - \sqrt 2|$:

$$
\begin{align}
\left|p^2 - 2q^2\right| &= 1 \\\
p^2 - 2q^2 &= \pm 1 \\\
\frac{p^2}{q^2} - 2 &= \pm \frac 1 {q^2} \\\
( \frac p q - \sqrt 2 ) ( \frac p q + \sqrt 2 ) &= \pm \frac 1 {q^2} \\\
\text{(you remember difference} &\text{ of two squares, right?)} \\\
\frac p q - \sqrt 2 &= \pm \frac 1 { q^2 \left( \frac p q + \sqrt 2 \right)} \\\
\left| \frac p q - \sqrt 2 \right| &= \frac 1 { q^2 \left| \frac p q + \sqrt 2 \right| }
\end{align}
$$

Since $\frac 1 { \frac p q + \sqrt 2 } < \frac 1 {\sqrt 2} < 1$,
$\frac 1 { q^2 \left( \frac p q + \sqrt 2 \right) } < \frac 1 {q^2}$; this means

$$ \left| \frac p q - \sqrt 2 \right| \leq \frac 1 {q^2} $$

The larger we make our $q$, the smaller $\frac 1 {q^2}$ will be, and then
our error will be bounded to a smaller value.
Our goal then becomes to find solutions to $\left| p^2 - 2q^2 \right| = 1$ 
with larger and larger $q$.

We can define a sequence of pairs $(p_n, q_n)$ recursively, starting with
$(p_1, q_1) = (1, 1)$. We then iterate on them with these formulae:

$$
\begin{align}
p_{n+1} &= p_n + 2q_n \\\
q_{n+1} &= p_n + q_n
\end{align}
$$

**Proposition.** All pairs $(p_n, q_n)$ generated using this definition from $(1, 1)$
satisfy Pell's equation. In addition, $q_n \geq n$ ($q$ continues increasing as 
we iterate).

> A proposition is like a less important theorem. Also, how did we get those
equations? Don't ask.

**Proof.** We will prove this by induction. Define
$\mathcal P (k): |p_k^2 - 2q_k^2| = 1 \land q_k \geq k$.

First we show our basis $\mathcal P (1)$: $| 1^2 - 2(1)^2 | = 1$ and indeed $1 \geq 1$,
so it is true.

Now, to show our inductive step, assume $\exists (p_k, q_k)$ s.t. $\mathcal P (k)$.

$$
\begin{align}
p_{k+1} &= p_k + 2q_k \\\
q_{k+1} &= p_k + q_k > q_k > k \tag*{(part one!)} \\\
\end{align}
$$

$$
\begin{align}
&\left|(p_k + 2q_k)^2 - 2(p_k + q_k)^2\right| \\\
&= \left| p_k^2 + 4p_kq_k + 4q_k^2 - 2p_k^2 - 4p_kq_k - 2q_k^2 \right| \\\
&= |2q_k^2 - p_k^2| \\\
&= |p_k^2 - 2q_k^2| \\\
&= 1 \tag*{(part two!)}
\end{align}
$$

$$
\begin{align}
\therefore \mathcal P(k) \implies \mathcal P(k+1)
\end{align}
$$

We have that $\mathcal P(1)$, and $\mathcal P(k) \implies \mathcal P(k + 1)$;
as a result, $\mathcal P(n) \forall n \in \mathbb N$. $\square$

From this, we can get the nicer upper bound that

$$ \left| \frac {p_n} {q_n} - \sqrt 2 \right| \leq \frac 1 {n^2} $$

Sweet! Analysis. Now we know that our iteration is productive.

## Oops! All Algebra

We don't have very good definitions for $\mathbb Q$ or $\mathbb R$ yet.
Of course, there are axioms which these fields need to follow, and
assuming the existence of a set which has these properties is how we
produce the rationals and the reals.

The axioms come in three groups:

- The axioms of arithmetic (x9)
- The axioms of order (x5)
- The completeness axiom

We'll take $X$ to be our example field equipped with two closed binary operations
$(X, +, \cdot)$. In other words,

$$\forall x, y \in X, x+y \in X \land x \cdot y \in X$$

In order for $X$ to be considered a field, it must satisfy these axioms:

- $(A1)$ **Additive associativity.** $\forall a, b, c \in X, (a + b) + c = a + (b + c)$

- $(A2)$ **Additive commutativity.** $\forall a, b \in X, a + b = b + a$

- $(A3)$ **Additive identity.** $\exists 0 \in X: a + 0 = a  \; \forall a \in X$

- $(A4)$ **Additive inverse.** $\forall a \in X \; \exists b \in X: a + b = 0$; $b = -a$

- $(A5)$ **Multiplicative associativity.** $\forall a, b, c \in X, (a \cdot b) \cdot c = a \cdot (b \cdot c)$

- $(A6)$ **Multiplicative commutativity.** $\forall a, b \in X, a \cdot b = b \cdot a$

- $(A7)$ **Multiplicative identity.** $\exists 1 \in X: a \cdot 1 = a \; \forall a \in X$

- $(A8)$ **Multiplicative inverse.** $\forall a \in X, a \neq 0 \; \exists b \in X: a \cdot b = 1$; $b = a^{-1}$

- $(A9)$ **Distributive law.** $\forall a, b, c \in X, a \cdot (b + c) = a \cdot b + a \cdot c$

An ordered field also requires a relation $(X, \leq)$ satisfying these axioms:

- $(A10)$ **Totality.** $\forall a, b \in X, a \leq b \lor b \leq a$

- $(A11)$ **Antisymmetry.** $a \leq b \land b \leq a \implies a = b$

- $(A12)$ **Transitivity.** $a \leq b \land b \leq c \implies a \leq c$

- $(A13)$ $\forall c \in X, a \leq b \implies a + c \leq b + c$

- $(A14)$ $\forall c \in X, 0 \leq c, a \leq b \implies a \cdot c \leq b \cdot c$

**Proposition.** $(\mathbb Q, +, \cdot, \leq)$ is an ordered field.

**Proof.** Just check that it satisfies all the axioms lol.

## University level mathematics

It's time for some hardcore proof work. We'll take $X$ to be an abstract ordered
field in each proposition.

**Proposition.** $x \cdot 0 = 0 \\ \forall x \in X$.

**Proof.**

$$
\begin{align}
0 + 0 &= 0 \tag{A3} \\\
x \cdot 0 &= x \cdot (0 + 0) \\\
x \cdot 0 &= x \cdot 0 + x \cdot 0 \tag{A9} \\\
x \cdot 0 + - (x \cdot 0) &= x \cdot 0 + x \cdot 0 + - (x \cdot 0) \tag{A4} \\\
0 &= x \cdot 0 + 0 \\\
x \cdot 0 &= 0 \tag{A3} \\\
&\hfill \square
\end{align}
$$

**Proposition.** If $a, b \geq 0 \in X$, then $a \leq b \iff a^2 \leq b^2$

**Proof.** We start by proving it in the $\implies$ direction;
$a \leq b \implies a^2 \leq b^2$.

Assuming $a \leq b$, we know by $(A14)$ that $a \cdot a \leq b \cdot a$
and $a \cdot b \leq b \cdot b$, and we know by $(A6)$ that $b \cdot a
= a \cdot b$,
and so

$$ 
a^2 = a \cdot a \leq b \cdot a = a \cdot b \leq b \cdot b = b^2
$$

In the other direction, we can prove the contrapositive; $a > b \implies a^2 > b^2$.

> Can we?? **TODO**

**Proposition.** The triangle inequality!

$$\forall x, y \in X, |x + y| \leq |x| + |y|$$

**Lemma.** $-x \cdot -x = x \cdot x$. Prove maybe **TODO**??

**Lemma.** $x \leq |x| \; \forall x \in X$ $(*)$.

**Proof.** We will show that the triangle inequality is logically equivalent to our
lemma.

$$
\begin{align}
&|x + y| \leq |x| + |y| \\\
&\iff |x + y|^2 \leq (|x| + |y|)^2 \\\
&\iff x^2 + 2xy + y^2 \leq x^2 + 2|x||y| + y^2 \\\
&\iff 2xy \leq 2|x||y| \\\
&\iff 2xy \leq 2|xy|
\end{align}
$$

which is true by our lemma $(*)$. $\square$

**Proposition.** The inverse triangle inequality!

$$\forall u, v \in X, |u| - |v| \leq |u - v|$$

**Proof.** Let $x = u - v$ and $y = v$.

$$
\begin{align}
&|x + y| \leq |x| + |y| \\\
&\implies |u| \leq |u - v| + |v| \\\
&\implies |u| - |v| \leq |u - v| \\\
&\hfill \square
\end{align}
$$

Now we're done.

## The mysterious 15th axiom

**Definition(s).** Let $S \subset X$, our example ordered field.

- $S$ is *bounded above* if $\exists H \in X: x \leq H \; \forall x \in S$.
- $S$ is *bounded below* if $\exists h \in X: x \geq h \; \forall x \in S$.
- $S$ is *bounded* if it is both bounded below and bounded above.
- The *supremum* of $S$ written $\sup S$ is its least upper bound.
- The *infimum* of $S$ written $\inf S$ is its greatest lower bound.
I don't need to define the maximum and minimum of $S$, but a fun fact
to convince yourself of is:

**Proposition.** $\exists \max S \implies \sup S = \max S$, and $\exists \min S
\implies \inf S = \min S$.

Now, I did promise you 15 axioms of a complete ordered field. Here is the elusive
axiom of completeness.

$(A15)$ **Completeness.** In a complete ordered field $X$, $\forall S \subset X$:

- $S$ bdd. above $\implies$ $\sup S \in S$
- $S$ bdd. below $\implies$ $\inf S \in S$

That's it. The idea is, any subset you can define of the real numbers has its bounds
inside the set itself.

Another way to put it is that if you have a least upper bound $H = \sup S$, if you 
try to pick a lower upper bound $H' < H$, $\exists x \in S: x > H$.

**Example.** Consider the set $S = \\{x \in \mathbb Q: 0 < x \land x^2 < 2 \\}$.
It's definitely bounded; $0 < x < 2 \; \forall x \in S$. Its infimum is $0$;
its supremum isn't actually *in* the rationals, and there is no maximum element;
you just get closer and closer to $\sqrt 2$.

**Remark.** If a set has no maximum, then it is infinite. Cool fact in a quiz question.

In the wisest warnings of Professor Hadzic, "here comes a fundamental theorem which I will
not prove":

**Theorem.** $\mathbb R$ is the only complete ordered field up to isomorphism.

So like, whatever.

**Theorem.** $\mathbb N$ is not bounded above; this is called the Archimedean Property.

**Proof.** Assume $\mathbb N$ *is* bounded above. By $(A15)$, $\exists H
\in \mathbb R = \sup \mathbb N$.

$H - 1 < H$, so $\exists n \in \mathbb N: n > H - 1 \implies n + 1 > H$. But
by the axioms of the naturals, surely $n + 1 \in \mathbb N$, which contradicts
$H$ being an upper bound. $\square$ (You're going to get *really* tired of these
"trivial" proofs).

Let's go back to our set $S$, but in the reals this time:
$\\{ x \in \mathbb R: 0 < x \land x^2 < 2 \\}$.

**Proposition.** $(\sup S)^2 = 2$

**Proof.** S is bounded, so let's label $M = \sup S$. Assume $M^2 \neq 2$.
Then either $M^2 < 2$ or $M^2 > 2$.

In the case that $M^2 < 2$, consider $M' = M + \frac 1 n, n \in \mathbb N$.
$(M')^2 = M^2 + \frac {2M} n + \frac 1 {n^2} < M^2 + \frac {2M + 1} n$,
so we can use that as an upper bound on the upper bound.

Let's set $(M')^2 < 2$ and see if we get anything. 

$$
\begin{align}
M^2 + \frac {2M + 1} n &< 2 \\\
\frac {2M + 1} n &< 2 - M^2 \\\
n &> \frac {2M + 1} {2 - M^2}
\end{align}
$$

By the Archimedean property, $\exists n \in \mathbb N: n > \frac {2M + 1} {2 - M^2}$, so
$(M')^2 = (M + \frac 1 n)^2 < 2$. This means if $M^2 < 2$, there will always be another
$M': M^2 < (M')^2 < 2$, so $M' \neq \sup S$.

Similarly, in the case that $M^2 > 2$, we can consider $M' = M - \frac 1 n, n \in
\mathbb N$. $(M')^2 = M^2 - \frac {2M} n + \frac 1 {n^2} > M^2 - \frac {2M} n$.

> **Remark.** I absolutely despise the random denominators we can just ignore in the
name of bounds.

Let's set $(M')^2 > 2$ and see if we get anything. $(\times 2 \text{ combo!})$.

$$
\begin{align}
M^2 - \frac {2M} n &> 2 \\\
M^2 - 2 &> \frac {2M} n \\\
n &> \frac {2M} {M^2 - 2}
\end{align}
$$

Again, by the Archimedean property, $\exists n \in \mathbb N : N > \frac {2M} {M^2 - 2}$.
If $M^2 > 2$, there will in fact always be an $M' : 2 < (M')^2 < M^2$, so 
$M' \neq \sup S$ in this case either.

We've contradicted it in both cases; that means $M^2 = (\sup S)^2 = 2$! $\square$

That's enough about the square root of $2$.

## Intervals

A reminder on intervals because why not: 
$$
a, b \notin (a, b) \\\
a, b \in [a, b]
$$

**Definition.** For a given $a \in \mathbb R, \epsilon > 0$, the $\epsilon$-neighbourhood
of $a$ is the set $\\{x \in \mathbb R: a - \epsilon < x < a + \epsilon\\}$,
or equivalently $(a - \epsilon, a + \epsilon)$ or $|x - a| < \epsilon$.

