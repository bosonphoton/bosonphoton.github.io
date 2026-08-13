---
layout: page

title: RL stuff

description: 

img:

importance: 1
---

# Importance Sampling

Importance sampling is a way to estimate an average under one probability distribution using samples from another distribution.


## 1. Start with a PMF

Suppose `X` can take values:

```text
X ∈ {1, 2, 3, 4, 5}
```

and the target distribution is:

|  x | p(x) |
| -: | ---: |
|  1 | 0.50 |
|  2 | 0.20 |
|  3 | 0.15 |
|  4 | 0.10 |
|  5 | 0.05 |


```text
p(x)

0.50 | ████████████████████  x=1
0.20 | ████████              x=2
0.15 | ██████                x=3
0.10 | ████                  x=4
0.05 | ██                    x=5
```

All probabilities sum to 1.

## 2. Expected Value

If we care about:

```text
f(x) = x²
```

then:

```text
E_p[f(X)] = Σ p(x) f(x)
```

For our distribution:

|  x | p(x) | f(x)=x² | p(x)f(x) |
| -: | ---: | ------: | -------: |
|  1 | 0.50 |       1 |     0.50 |
|  2 | 0.20 |       4 |     0.80 |
|  3 | 0.15 |       9 |     1.35 |
|  4 | 0.10 |      16 |     1.60 |
|  5 | 0.05 |      25 |     1.25 |

So:

```text
E_p[f(X)] = 0.50 + 0.80 + 1.35 + 1.60 + 1.25 = 5.50
```

## 3. CDF and Inverse CDF Sampling


|  x | p(x) | F(x) |
| -: | ---: | ---: |
|  1 | 0.50 | 0.50 |
|  2 | 0.20 | 0.70 |
|  3 | 0.15 | 0.85 |
|  4 | 0.10 | 0.95 |
|  5 | 0.05 | 1.00 |

Visualized on the interval `[0, 1]`:

```text
0.00        0.50    0.70   0.85  0.95 1.00
|-----------|-------|------|-----|----|
     x=1       x=2    x=3   x=4  x=5
```

To sample from this distribution:

1. Draw a random number `u` uniformly from `[0, 1]`.
2. Find where it lands in the CDF intervals.
3. Output the corresponding `x`.

Example:

```text
u = 0.63
```

Since `0.63` lands between `0.50` and `0.70`, we output:

```text
x = 2
```

This is **inverse CDF sampling**.

## 4. Why Importance Sampling Exists

Sometimes sampling from the target distribution `p(x)` is hard or inefficient.

Maybe rare events matter a lot.

In our example, `x = 5` is rare under `p`, but `f(5) = 25`, so it contributes a lot to the expected value.

Instead of sampling from `p`, we choose another distribution `q`, called the **proposal distribution**.

Let:

|  x | p(x), target | q(x), proposal |
| -: | -----------: | -------------: |
|  1 |         0.50 |           0.20 |
|  2 |         0.20 |           0.20 |
|  3 |         0.15 |           0.20 |
|  4 |         0.10 |           0.20 |
|  5 |         0.05 |           0.20 |

Here, `q` is uniform. So we see rare large values like `x = 5` more often.

But now our samples are biased, because they come from `q`, not `p`.

So we correct them.

## 5. Importance Weights

The correction factor is:

```text
w(x) = p(x) / q(x)
```

This is called the **importance weight**.

|  x | p(x) | q(x) | w(x)=p(x)/q(x) |
| -: | ---: | ---: | -------------: |
|  1 | 0.50 | 0.20 |           2.50 |
|  2 | 0.20 | 0.20 |           1.00 |
|  3 | 0.15 | 0.20 |           0.75 |
|  4 | 0.10 | 0.20 |           0.50 |
|  5 | 0.05 | 0.20 |           0.25 |



## 6. The Key Formula


```text
E_p[f(X)] = Σ q(x) [p(x)/q(x)] f(x)
```

So:

```text
E_p[f(X)] = E_q[w(X) f(X)]
```


## 7. Concrete Sample Estimate

Suppose we sample from `q`, the uniform proposal distribution:

```text
samples: 1, 3, 5, 5, 2
```

If we naively average `x²`, we get:

```text
(1² + 3² + 5² + 5² + 2²) / 5
= (1 + 9 + 25 + 25 + 4) / 5
= 12.8
```

But that estimates the expectation under `q`, not under `p`.

So we weight each value:

| sample x | f(x)=x² | w(x) | w(x)f(x) |
| -------: | ------: | ---: | -------: |
|        1 |       1 | 2.50 |     2.50 |
|        3 |       9 | 0.75 |     6.75 |
|        5 |      25 | 0.25 |     6.25 |
|        5 |      25 | 0.25 |     6.25 |
|        2 |       4 | 1.00 |     4.00 |

Now average the weighted values:

```text
(2.50 + 6.75 + 6.25 + 6.25 + 4.00) / 5 = 5.15
```

The exact answer was:

```text
5.50
```

With more samples, the estimate gets closer.


## 8. Why It Matters in RL

In RL, we often collect trajectories from one policy but want to evaluate or train another policy.

Suppose:

```text
π_old(a | s) = policy that generated the data
π_new(a | s) = policy we care about now
```

Then the importance weight for an action is:

```text
w = π_new(a | s) / π_old(a | s)
```

If the new policy was more likely to take the action, we upweight it.

If the new policy was less likely to take the action, we downweight it.

For a trajectory, the weights across steps multiply together, which can become unstable. That is why RL algorithms often use clipping, normalization, or KL penalties.

## 9. The Main Danger

Importance sampling can have high variance.

If `q(x)` is tiny but `p(x)` is large, then:

```text
w(x) = p(x) / q(x)
```

can become huge.

Then one sample can dominate the whole estimate.

So a good proposal distribution should sample often from places that matter for the expectation.

Not just where `p(x)` is large.

Where `p(x)f(x)` is large.
