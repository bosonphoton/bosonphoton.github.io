---
layout: page

title: math proofs

description: notes from Transition to Higher Mathematics, Structure and Proof by Bob A. Dumas and John E. McCarthy. (excuse some lazy language)

img: 

importance: 3
---

<style>
    body {
      font-size: 14px; /* Adjust the font size as needed */
      line-height: 1; /* Adjust the line height as needed */
    }
    p {
      margin-bottom: 8px; /* Adjust the margin bottom for paragraphs as needed */
    }
    .math {
      font-size: 14px; /* Adjust the font size for math expressions as needed */
    }
</style>

<h5><b>Preliminary</b></h5>
Natural numbers $$\mathbb{N}$$ = {0,1,2,3...} <br>
Integers $$\mathbb{Z}$$ = {...,-1,0,1,...} <br>
Rational numbers $$\mathbb{Q}$$ = {$$\frac{p}{q}$$ where p,q $$\in$$ $$\mathbb{Z}$$ and q $$\neq$$ 0} <br>

A bounded interval must be either:
1. (a,b)
2. [a,b)
3. (a,b]
4. [a,b] 

Unbounded intervals are either:
1. (-$$\infty$$, b)
2. (-$$\infty$$, b]
3. (b,$$\infty$$)
4. [b,$$\infty$$)
5. R

Notice that $$\mathbb{R}$$ is both an open interval (noninclusive) and a closed interval (inclusive). <br><br>

<h6><b><u>Sets</u></b></h6>
Def: X is a proper subset $$\subsetneq$$ of Y if $$X \subset Y$$ and $$X \neq Y$$ <br><br>
Def: The empty set $$\emptyset$$ is the set with no elements; it is true that $$\emptyset \subset X$$ for any set X <br><br>
Def: X and Y are disjoint if $$X \cap Y = \emptyset$$ <br><br>
Def: The Cartesian product (direct product) of X and Y is the set of ordered pairs $$\{ (x,y) | x \in X$$ and $$y \in Y \}$$. More generally, $$\prod_{i=1}^{n} X_i$$ = $$\{ (x_1, x_2, \ldots, x_n) \mid x_i \in X_i, \ 1 \leq i \leq n\}$$. $$X^n$$ denotes the Cartesian product of a set X for n times.  <br><br>
Order of set operations matter: if X and Y are disjoint, $$(X \cap X) \cup Y \neq X \cap (X \cup Y)$$ <br><br>

<h6><b><u>Functions</u></b></h6>
Let $$f: X \rightarrow Y$$ be a function mapping elements from set $$X$$ to set $$Y$$. <br>
1. The same X cannot map to different Y
2. Different X can map to same Y 

For instance, Let $$f: \mathbb{Z} \to \mathbb{R}$$ be given by $$f(x) = x^2$$. <br>
Not every R is assigned to a number in Z. <br>
Tho different R can map to same Z (i.e., R = -2, 2).



