---
title: Asymptotic behaviors (O, Ω, Θ)
description: How different algorithms costs behave when compared to each other
tags:
  - big-o
  - algorithms
---
the mathematic function to represent the estimated cost of an algorithm is $f(n)$

some considerations:
1. where $n$ is the input, an algorithm analysis must be made for great (big) values of $n$;
2. the asymptotic behavior of $f(n)$ is the cost limit as $n$ grows in size;

a function $f(n)$ asymptotically **dominates** another $g(n)$ function when there are two positive constants $c$ and $m$ where $n >= m$ we got: $|g(n)| ⩽ c × |f (n)|$

![[Pasted image 20250423175940.webp]]

1. $n$ is the input so we are measuring the asymptotic behavior as it grows in size;
2. $m$ is the exact input ($n$) where from that on ($n>=m$), $f(n)$ dominates $g(n)$;
3. we can say that at $m$ the function $f(n)$ asymptotically dominates $g(n)$;
4. $c$ is a constant that must be taken into consideration.

we can find $m$ by testing out numbers. let's say $g(n) = n^2$ and $f (n) = 2^n$:

$n = 2$: $g(n) = 4$ and $f(n) = 4$

$n = 3$: $g(n) = 9$ and $f(n) = 8$

$n = 4$: $g(n) = 16$ and $f(n) = 16$

$n = 5$: $g(n) = 25$ and $f(n) = 32$

we find out that $m = 4$ is the value of the constant that makes $f(n)$ dominates $g(n)$.

## big-o notation
the O notation (reads big oh notation) is used to compare asymptotic behaviors, it represents the speed a function tends to infinity.

we say $g(n) = O(f (n))$ to express that $f(n)$ asymptotically dominates $g(n)$. if we write down a $T(n)$ function and state that it runs at $O(n^2)$ we are saying for constants $c$ and $m$ we have $T(n) ⩽ cn^2$.

that's because if $O(n^2)$ is the runtime of the function then $cn^2$ dominates it.

the big-o notation specifies a superior limit of a function. in other words, if a function $f(n)$ runs at $O(g(n))$ then $f(n) ⩽ c×g(n)$ must be true, meaning that $c×g(n)$ is the superior limit of the $f(n)$ function.

![[Pasted image 20250423181815.webp]]

important operations with this notation are:

![[Pasted image 20250423181928.webp]]

## omega notation
the Ω (omega) notation defines the inferior limit for a function, it is the opposite of $O(n)$.

that being said, we can state that, for constants $c$ and $m$, for every $n >= m$ we have $g(n) ⩾ c × f (n)$.

in other words, $g(n) = Ω(f(n))$.

![[Pasted image 20250423182259.webp]]

# theta notation
the Θ (theta) notation is a asymptotic limit for both $f(n)$ and $g(n)$ functions when compared, it stablishes both the superior limit for one and inferior limit for the other.
this can only happen when we have two constants $c1$ and $c2$ taken into account, e.g.:

![[Pasted image 20250423184108.webp|611]]

this is the representation of $g(n) = Θ(f(n))$ . the $g(n)$ is dominated both superiorly and inferiorly by $f(n)$ when there are three $c1$, $c2$ and $m$ constants.