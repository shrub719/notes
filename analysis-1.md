# Analysis 1

## Introduction

This intro is probably going to be very sparse; most of it was course structure and basic definitions.
You'll notice me jump around a lot because there were periods of less information.

A couple hard one-liners from the first lecture:

- "The devil lies in the three dots $\cdots$"
- "Mathematicians often abstract things that are obvious to essentialise their features."
- "I will explain once, then I explain never again."

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

Watch closely, because I'm about to pull
the most bullshit rearrangements in the name of *analysis*.

$$
\begin{align}
\left|p^2 - 2q^2\right| &= 1 \\\
p^2 - 2q^2 &= \pm 1 \\\
\frac{p^2}{q^2} - 2 &= \pm \frac 1 {q^2} \\\
( \frac p q - \sqrt 2 ) ( \frac p q + \sqrt 2 ) &= \pm \frac 1 {q^2} \\\
\frac p q - \sqrt 2 &= \pm \frac 1 { q^2 \left( \frac p q + \sqrt 2 \right)} \\\
\left| \frac p q - \sqrt 2 \right| &= \frac 1 { q^2 \left| \frac p q + \sqrt 2 \right| }
\end{align}
$$

Since $\frac 1 { \frac p q + \sqrt 2 } < \frac 1 {\sqrt 2} < 1$,
$\frac 1 { q^2 \left( \frac p q + \sqrt 2 \right) } < \frac 1 {q^2}$;
this means the larger we make our $q$, the smaller $\frac 1 {q^2}$ will be, and the
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

> A proposition is like a less important theorem.

**Proof.** We will prove this by induction. Define
$\mathcal P (k): |p_k^2 - 2q_k^2| = 1$.

First we show our basis $\mathcal P (1)$: $| 1^2 - 2(1)^2 | = 1$ and indeed $1 \geq 1$,
so it is true.

Now, to show our inductive step, assume $\exists (p_k, q_k)$ s.t. $\mathcal P (k)$.

$$
\begin{align}
p_{k+1} &= p_k + 2q_k \\\
q_{k+1} &= p_k + q_k > 1\\\
\end{align}
$$

$$
\begin{align}
&\left|(p_k + 2q_k)^2 - 2(p_k + q_k)^2\right| \\\
&= \left| p_k^2 + 4p_kq_k + 4q_k^2 - 2p_k^2 - 4p_kq_k - 2q_k^2 \right| \\\
&= |2q_k^2 - p_k^2| \\\
&= |p_k^2 - 2q_k^2| \\\
&= 1
\end{align}
$$

$$
\begin{align}
\therefore \mathcal P(k) \implies \mathcal P(k+1)
\end{align}
$$

We have that $\mathcal P(1)$, and $\mathcal P(k) \implies \mathcal P(k + 1)$;
as a result, $\mathcal P(n) \\ \forall n \in \mathbb N$. $\square$
