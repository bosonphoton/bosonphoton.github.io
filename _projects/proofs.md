---
layout: page

title: math proofs

description: notes from Transition to Higher Mathematics, Structure and Proof by Bob A. Dumas and John E. McCarthy. (excuse some lazy language)

img: 

importance: 2
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
Ex: the empty function is the function with empty graph (a graph that is the empty set of f). So $$f: \emptyset \to Y$$. <br>
Let $$f: X \rightarrow Y. Z \subset X \times Y$$. Z is a the graph of f if: <br>
1. for any $$x \in X, \exists y \in Y \mid (x,y) \in Z$$ (i.e., every vertical line through X cuts the graph at least once) <br>
2. if (x,y) is in Z, and (x,z) is in Z, then y = z (i.e., every vertical line through X cuts the curve at most once) <br><br>

Def: X is the <b>domain</b>, Y is the <b>codomain</b> (which accounts for all <i>possible</i> outputs, different than the <b>range</b> which is what <i>actually</i> comes out) <br>
Ex: Let $$f: \mathbb{N}\to \mathbb{N}$$ be defined by $$f(n) = n^2$$. Let $$g: \mathbb{N}\to \mathbb{R}$$ be defined by $$g(x) = x^2$$. <br>
Then graph(f) = graph(g), but f and g are different functions. <br>
Let $$h: \mathbb{R}\to \mathbb{R}$$ be defined by $$h(x) = x^2$$. <br>
Then graph(f) $$\subsetneq$$ graph(h). <br><br>

Def: The <b>range</b> (basically the function's outputs) is the set of images of elements in X under f; it is a subset of the codomain. <br><br>

Def: f is a <b>real-valued function</b> if Ran(f) $$\subset \mathbb{R}$$ <br><br>

<h6><b><u>Injections, Surjections, Bijections</u></b></h6> <br>
<img src="/assets/img/injection.jpeg" alt="inj,surj,bij" width = "600"><br><br>

<b>1. Injections (one to one)</b>: Every unique x maps to a unique y; but not every y may be assigned an x <br>
1. f is an injection if x & y are distinct elements $$\in$$ X, f(x) $$\neq$$ f(y). <br>
2. or if f(x) = f(y) then x = y <br>

Counterexample: $$f(x) = x^2$$ is not an injection bc f(-2) = f(2) <br><br>
Let $$f: X \to Y$$ and $$g: Y \to Z$$. <br>
Prove that if f & g are injective, then g $$\circ$$ f is injective. <br>
<b>Proof</b>: Suppose $$g \circ f(x) = g \circ f(y)$$. If g is injective, then f(x) = f(y). If f is injective, then x = y. So g $$\circ$$ f is injective. 
<br><br>


<b>2. Surjections (onto)</b>: All y must be assigned some x; even if different x maps to same y<br>
1. f is a surjection if Ran(f) = Y (i.e., the range captures ALL of the codomain)<br>

Let $$ Y = \{x \in \mathbb{R} \mid x \geq 0 \}$$ and $$f: \mathbb{R} \to Y$$ be defined by $$f(x) = x^2$$. Prove that f is a surjection. <br>
<b>Proof</b>: We need to prove that Ran(f) = Y. Since Ran(f) is always $$\subset$$ Y, we also want to show Y $$\subset$$ Ran(f). Let y $$\in$$ Y, so y is a non-negative real number. Then $$\sqrt{y} \in \mathbb{R}$$ and f($$\sqrt{y}$$) = y. So y $$\in$$ Ran(f). Since y is an arbitrary element of Y, then Y $$\subset$$ Ran(f). <br>
<b>Explanation</b>: We start with the definition of a surjection, which is Y = ran(f). To prove equivalence, we can show that they are subsets of each other. Using the known fact that the range is always a subset of the codomain, we additionally need to show that this given codomain Y is a subset of the range. We choose some input $$\sqrt{y}$$ that satisfies $$\in \mathbb{R}$$, and the output image is y. So y is an element of Ran(f). Since y is arbitrary, this shows that <b>every</b> element in Y is in Ran(f), so Y $$\subset$$ Ran(f).
<br><br>

<b>3. Bijections (both inj + surj)</b>: All elements of y must have a unique x<br>
1. Bijective functions preserve key structural features of the domain, and we can treat domain and codomain as the same set. <br><br>

Def: A <b>permutation</b> of set X is a bijection $$f: X \hookrightarrow X$$ 
<br><br>

<h6><b><u>Images and Inverses</u></b></h6> <br>
Def: <b>Inverse (Pre) Image</b>. Let $$f: X \to Y$$ and $$b \in Y$$. The inverse image $$f^{-1}(b) = \{x \in X \mid f(x) = b\}$$ (Sort of like a reverse mapping) <br>
1. If $$b \notin Ran(f)$$ then $$f^{-1}(b) = \emptyset$$ 
2. If f is injection, then for any $$b \in Ran(f), f^{-1}(b)$$ has a single element (bc injections = for every unique x $$\exists$$ unique y so the reverse mapping must have only a single element)





