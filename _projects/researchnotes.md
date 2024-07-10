---
layout: page

title: interpretability & causality

description: notes on causal & interpretable ML approaches

img: 

importance: 2

category: work
---


<h2><b> 1. LIME (local interpretable model agnostic explanations)</b> </h2>

<img src = "/assets/lime.png" width = 700px >
- Explains the local (zoomed-in) approximation for the overall complex model 
- Fits a linear model on this zoomed-in portion 
<br>

<img src = "/assets/limemath.png" width = 500px > <br>
- $$G$$ can be collection of interpretable models $$\{$$ Linear regression, Decision trees, Log Reg...$$\}$$ 
- $$\pi_{x}$$ represents the locality area around $$x$$
- minimize $$\mathcal{L}(f, g, \pi_{x})$$ which measures how bad the simple model $$g$$ approximates $$f$$ within the area of $$\pi_{x}$$
- minimize $$\Omega(g)$$ which is measure of complexity of the interpretable model $$g$$ such as (# of parameters in linear regression, depth of decision trees, etc.) 
<br><br>

<b>Implementation:</b> <br>
Step 1. Calculate the first loss term $$\mathcal{L}(f, g, \pi_{x})$$ <br><br>

<img src = "/assets/limeloss1.png" width = 500px > <br>

- Within the local area of query point, generate a bunch of random new datapoints
- Classify those datapoints according to the complex model $$f$$
- Use these new data & labels predicted by $$f$$ to train a simple model $$g$$
- Loss is then defined as the total deviation from complex model $$f$$ to simple model $$g$$ for each random generated datapoint
- Additionally, we should weight the errors based on distance from the query point
<br><br>

Step 2. Calculate the second loss term $$\Omega(g)$$<br>
- Ensures the model is as simple as possible
- So you can use something like lasso or ridge regression in a linear model
<br><br>

<b>Summary: LIME allows you to see which input features are most relevant for an output prediction, even if the model is black box </b><br>
<img src = "/assets/limeoutput.png" width = 300px > <br>

<br><br>
<h2><b> 2. SHAP (Shapley Additive Explanations)</b> </h2>
- Shapley values tells us the <b>weighted average of a features contribution to the output</b>
- Find marginal contributions of each subset of features (to account for interactions between features)
- So we need to iterate over all possible combinations of features and then average <b>(total of $$2^{n}$$ subsets)</b><br>

<br>
Example: 2 player game <br>
<img src = "/assets/coalition.png" width = 500px > <br><br>
Player 1 and Player 2 work together and generate $10,000 <br>
Player 1 alone can generate 7,500 <br>
Player 2 alone can generate 5,000 <br>
- Shapley(Player 1) = (total - p2 solo contribution) + p1 solo contribution / 2
- Shapley(Player 2) = (total - p1 solo contribution) + p2 solo contribution / 2
<br><br>

Example: 3 player game <br>
<img src = "/assets/player3.png" width = 500px > <br><br>
- Shapley(Player 1) = weighted average of all possible subsets that isolate player 1
- Weights --> expected marginal contributions

How do we get the weights? <br>
- Weights = number of ways in which Player 1 can join the different coalitions
<img src = "/assets/weights.png" width = 500px > <br><br><br>

<b> General Shapley Value Formula </b><br>
<img src = "/assets/shapform.png" width = 500px > <br><br>



<br>
<h2><b> 3. Counterfactual Explanations</b> </h2> 
- Person X has a 90% of stroke. <u>If they decrease BMI to 25</u>, then decrease prediction to 30% stroke. 
- <b>Counterfactual: The smallest change in input features that changes prediction to another output</b>

<center>
<img src = "/assets/counterfactual.png" width = 200px> <br>
</center>
- Find the minimum change from the original input $$x$$ to the counterfactual $$x'$$ st. the output class is changed $$f(x') = c$$
<br><br>

Generating counterfactuals <br>
1. White box approach: if we have access to the model (model-specific)
2. Black box approach: if we only have inputs and outputs (model-agnostic)

<br>
Output of a counterfactual explainer results in what features need to change by what value in order to output a designated class
<br><br><br>






<h2><b> 4. Causality and Graph Neural Networks</b> </h2>
<img src = "/assets/confound.png" width = 600px> <br><br>

<b><u>Def: Confounding Factors</u></b> are variables that influence both independent and dependent variables. The existence of them explains why correlation != causation.
- Let X be an ind. variable and Y be a dep variable. <b>We say that X and Y are confounded by Z if Z causally influences both X and Y.</b>
- Ex: Suppose we want to see if carb intake (X) affects cholesterol levels (Y). A confounding variable (Z) could be exercise level, as people who exercise more can eat more carbs and also impact cholesterol.
<br>

<b>Goal:</b> Isolate causal effects by reducing confounding factors by blocking paths (do-calculus)
<br>

<b>Pearls Causal Hierarchy and Do-Calculus</b>
1. Association (Seeing Patterns): Provides observational info and correlations
- Ex: Observing students who study more get higher test scores
2. Interventions (Doing Something): Approximating what happens if you change something and the effects of actions
- Ex: Making people study more to observe the effect on scores
4. Counterfactuals (Imagining What-Ifs): Imagining hypotheticals about what happens after-the-fact 
- Ex: Imagining what would happen if people did not study at all


<a href="https://www.bnlearn.com/">www.bnlearn.com</a> <br>
<a href="https://www.pywhy.org/dowhy/v0.11.1/">www.pywhy.org</a>
<br><br>

<b>Neural Causal Models</b><br>
- Goal is to approximate connections between variables by learning associational/interventional/counterfactual distributions
<br><br><br>

<h2><b> 5. Bayesian Networks</b> </h2>
<br><br>
<img src = "/assets/bayesnet.png" width = 500px> <br>
- Notice how we don't factor in the rain when calculating probability of slipping. All we care about is that the ground is wet. 
<br>

Inference:
Given a Bayesian Network describing P(X,Y,Z), what is P(Y)
1. Enumeration (brute force)









