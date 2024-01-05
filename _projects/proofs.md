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
Def: X is a <b>proper subset</b> $$\subsetneq$$ of Y if $$X \subset Y$$ and $$X \neq Y$$ <br><br>
Def: The <b>empty set</b> $$\emptyset$$ is the set with no elements; it is true that $$\emptyset \subset X$$ for any set X <br><br>
Def: X and Y are <b>disjoint</b> if $$X \cap Y = \emptyset$$ <br><br>
Def: The <b>Cartesian product</b> (direct product) of X and Y is the set of ordered pairs $$\{ (x,y) | x \in X$$ and $$y \in Y \}$$. More generally, $$\prod_{i=1}^{n} X_i$$ = $$\{ (x_1, x_2, \ldots, x_n) \mid x_i \in X_i, \ 1 \leq i \leq n\}$$. $$X^n$$ denotes the Cartesian product of a set X for n times.  <br><br>
Order of set operations matter: if X and Y are disjoint, $$(X \cap X) \cup Y \neq X \cap (X \cup Y)$$ <br><br>

<h6><b><u>Functions</u></b></h6>
Let $$f: X \rightarrow Y$$ be a function mapping elements from set $$X$$ to set $$Y$$. <br>
1. The same X cannot map to different Y
2. Different X can map to same Y 

For instance, Let $$f: \mathbb{Z} \to \mathbb{R}$$ be given by $$f(x) = x^2$$. <br>
Not every R is assigned to a number in Z. <br>
Tho different R can map to same Z (i.e., R = -2, 2). <br><br>

Def: The <b>image</b> of x, f(x) for $$x \in X$$ is the element of Y that f assigns to x. <br><br>
Def: The <b>graph of a function</b> is just the domain paired with it's range (but not every element of Y is used up) $$\{ (x,y) | x \in X$$ and $$f(x) = y \}$$. graph(f) $$\subset X \times Y$$ <br>
Ex: the empty function is the function with empty graph (a graph that is the empty set of f). So $$f: \emptyset \to Y$$. <br><br>
Let $$f: X \rightarrow Y. Z \subset X \times Y$$. Z is a the graph of f if: <br>
1. for any $$x \in X, \exists y \in Y \mid (x,y) \in Z$$ (i.e., every vertical line through X cuts the graph at least once) <br>
2. if (x,y) is in Z, and (x,z) is in Z, then y = z (i.e., every vertical line through X cuts the curve at most once) <br><br>

Def: X is the <b>domain</b>, Y is the <b>codomain</b> (which accounts for all <i>possible</i> outputs, different than the <b>range</b> which is what <i>actually</i> comes out)






