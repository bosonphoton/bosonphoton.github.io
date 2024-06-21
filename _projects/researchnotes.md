---
layout: page

title: interpretability & causality

description: notes on causal & interpretable ML approaches

img: 

importance: 8

category: work
---


<h3> Interpretability Techniques </h3> <br>
<h5> 1. LIME (local interpretable model agnostic explanations) </h5>

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
<h5> 2. SHAP (Shapley Additive Explanations) </h5>
- Shapley values tells us the average contribution of each feature to the output
- Find marginal contributions of each subset of features (to account for interactions between features)
- So we need to iterate over all possible combinations of features and then average <b>(total of $$2^{n}$$ subsets)</b>




<br><br>
<h5> 3. Counterfactual Explanations </h5>