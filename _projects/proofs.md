---
layout: page

title: math proofs

description: notes from Transition to Higher Mathematics, Structure and Proof by Bob A. Dumas and John E. McCarthy.

img: 

importance: 2
---

<style>
    body {
      font-size: 15px; /* Adjust the font size as needed */
      line-height: 1; /* Adjust the line height as needed */
    }
    p {
      margin-bottom: 8px; /* Adjust the margin bottom for paragraphs as needed */
    }
    .math {
      font-size: 14px; /* Adjust the font size for math expressions as needed */
    }
</style>

<h4><b>Preliminary</b></h4>
Natural numbers $$\mathbb{N}$$ = {0,1,2,3...} <br>
Integers $$\mathbb{Z}$$ = {...,-1,0,1,...} <br>
Rational numbers $$\mathbb{Q}$$ = {$$\frac{p}{q}$$ where p,q $$\in$$ $$\mathbb{Z}$$ and q $$\neq$$ 0} <br>
$$\mathbb{R}$$ is both an open interval (noninclusive) and a closed interval (inclusive). <br><br>

[//]: # (A bounded interval must be either:)

[//]: # (1. &#40;a,b&#41;)

[//]: # (2. [a,b&#41;)

[//]: # (3. &#40;a,b])

[//]: # (4. [a,b] )

[//]: # ()
[//]: # (Unbounded intervals are either:)

[//]: # (1. &#40;-$$\infty$$, b&#41;)

[//]: # (2. &#40;-$$\infty$$, b])

[//]: # (3. &#40;b,$$\infty$$&#41;)

[//]: # (4. [b,$$\infty$$&#41;)

[//]: # (5. R)

<h6><b><u>Sets</u></b></h6>
Def: X is a <b>proper subset</b> $$\subsetneq$$ of Y if $$X \subset Y$$ and $$X \neq Y$$ <br><br>
Def: The <b>empty set</b> $$\emptyset$$ is the set with no elements; it is true that $$\emptyset \subset X$$ for any set X <br><br>
Def: X and Y are <b>disjoint</b> if $$X \cap Y = \emptyset$$ <br><br>
Def: The <b>Cartesian product</b> (direct product) of X and Y is the set of ordered pairs $$\{ (x,y) | x \in X$$ and $$y \in Y \}$$. More generally, $$\prod_{i=1}^{n} X_i$$ = $$\{ (x_1, x_2, \ldots, x_n) \mid x_i \in X_i, \ 1 \leq i \leq n\}$$. $$X^n$$ denotes the Cartesian product of a set X for n times.  <br><br>
Def: <b>Floor/ceiling</b>. $$\lceil n \rceil$$ is the set of natural numbers (0,1,2..., n-1) less than n<br><br>
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
2. If f is injection, then for any $$b \in Ran(f), f^{-1}(b)$$ has a single element (bc injections = for every unique x $$\exists$$ unique y so the reverse mapping must have only a single element)<br><br>

Def: <b>Inverse Function</b>. If $$f: X \to Y$$ is a bijection, then the inverse function is  $$f^{-1}: Y \to X$$ with the graph $$\{(b,a) \in Y \times X \mid (a,b) \in graph(f)\}$$.<br><br>

Def: <b>Identity Function</b>. If f is a bijection, then $$f^{-1} \circ f = Id(X)$$ and $$f \circ f^{-1} = Id(Y)$$.<br><br>

Def: <b>Restricted Domain</b> (Considers a new function on smaller domain if non-invertible): Because some functions are not injections ($$f = x^{2}$$) and non-invertible (since one Y can map back to two different X's), we can first consider a new function $$g$$ equal to $$f$$ on a subset of the domain. For instance $$g(x) = x^{2}$$ with domain $$\{x \in R \mid x \geq 0\}$$.<br>
Ex: Let $$f: X \to Y$$ and $$W \subset X$$. The restriction of f to W is $$f\vert_W = f: W \to Y$$ <br>
$$graph(f\vert_{W}) = graph(f) \cap [W \times Y]$$<br><br>

<h6><b><u>Sequences</u></b> (a list of objects)</h6><br>

Def: A <b>Finite Sequence</b> $$\braket{a_n \mid n < N}$$ is a function with domain $$\lceil N \rceil$$ where $$N \in \mathbb{N}$$.<br> 
An <b>Infinite Sequence</b> is just $$\braket{a_n \mid n \in N}$$ (the domain is the infinite in $$\mathbb{N}$$)<br>
- Often denoted $$\braket{a_n}$$ <br><br>

Def: A finite <b>Binary Sequence</b> is a function $$f:\lceil N \rceil \to \lceil 2 \rceil$$, and infinite binary sequence is just $$f: \mathbb{N} \to \lceil 2 \rceil$$.<br><br>

Def: An <b>Infinite Union</b> is $$\bigcup_{n=1}^{\infty} X_n = \{x \mid \text{for some } n \in \mathbb{N^+}, x \in X_n\}$$
- collection of all elements that are in at least one of the sets $$X_n$$
- $$\mathbb{N^+}$$ is the <b>Index Set</b> for the union <br><br>

Def: <b>Family of Sets</b>. Let A be a set, for $$a \in A$$, let $$X_a$$ be a set ($$X_a$$ is a set indexed by A). $$F = \{X_a \mid a \in A \}$$ is the family of sets indexed by A. <br>
Ex: Let $$X_n = \{n+1, n+2,..., 2n\}$$ for $$n \in \mathbb{N^+}$$. Then
- $$\bigcap_{n=1}^{\infty} X_n = \emptyset$$ <br><br>


<h6><b><u>Exercises</u></b></h6><br>
1. Prove Demorgans Laws: $$(A \cap B)^c = A^c \cup B^c$$
- Let $$x \in (A \cap B)^c$$
- Then $$x \notin (A \cap B)$$
- $$x \notin A$$ and $$x \notin B$$
- So $$x \in A^c$$ and $$x \in B^c$$ <br><br>

2. Prove that $$A \cap (B \cup C) = (A \cup B) \cap (A \cup C)$$
- Let $$x \in A \cap (B \cup C)$$
- $$x \in A$$ and $$x \in (B \cup C)$$
- $$x \in A$$ and either $$(x \in B)$$ or $$(x \in C)$$
- either $$(x \in A$$ and $$x \in B)$$ or $$(x \in A$$ and $$x \in C)$$
- ($$x \in A$$ and $$B$$) or ($$x \in A$$ and $$C$$)
- So $$x \in (A \cap B) \cup (A \cap C)$$



<br><br>
<h4><b>Relations</b></h4>
Def: A <b>Relation</b> from X to Y is a subset of X $$\times$$ Y. Any set of ordered pairs is a relation.<br><br>
- <b>$$xRy$$</b> denotes that x bears a relation R to y, aka $$(x,y) \in R$$.
- X and Y can be the same set, then the relation is "on" rather than "between"
- A function $$f: X \to Y$$ can be thought of as a special relation from X to Y with the property that every X occurs exactly once as a first element of a pair in the relation (where no same X can map to a different Y). <br>

<h6><b><u>Properties of Relations</u></b></h6><br>
1. <b>Reflexive</b> implies $$(xRx)$$
2. <b>Symmetric</b> implies $$(xRy = yRx)$$
3. <b>Antisymmetric</b> implies $$(xRy$$ and $$yRx \to x = y)$$
4. <b>Transitive</b> implies $$(xRy$$ and $$yRz \to xRz)$$ <br><br>

<h6><b><u>Orderings</u></b></h6><br>





