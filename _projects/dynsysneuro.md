---
layout: page

title: dynamical systems in neuroscience

description: notes from Dynamical Systems in Neuroscience, The Geometry of Excitability and Bursting by Eugene M. Izhikevich

img: 

importance: 3

category: work
---

<h5>4 Variables Describing Neuronal Dynamics</h5>
1. Membrane potential <br>
2. Excitation variables <br>
3. Recovery variables <br>
4. Adaptation variables <br>


<br>

**Neural Firing Rate Equation**  
   The firing rate of a neuron can be described by a simple linear model:<br><br>
   $$
   \begin{align}
   \frac{dR}{dt} = -\frac{R}{\tau} + I
   \end{align}
   $$ <br><br>
   where $$ R $$ is the firing rate, $$\tau$$ is the time constant, and $$I$$ is the input stimulus.

<br>
**Hodgkin-Huxley Model**  
   The Hodgkin-Huxley model is a set of nonlinear differential equations describing the ionic currents that contribute to the action potential in a neuron:<br><br>
   $$
   \begin{align}
   C_m \frac{dV}{dt} = I_{\text{ext}} - \bar{g}_{\text{K}} n^4 (V - V_{\text{K}}) - \bar{g}_{\text{Na}} m^3 h (V - V_{\text{Na}}) - \bar{g}_{\text{L}} (V - V_{\text{L}})
   \end{align}
   $$<br><br>

   where $$V$$ is the membrane potential, $$C_m$$ is the membrane capacitance, $$I_{\text{ext}}$$ is the external current, $$ \bar{g}_i $$ and $$V_i$$ are the maximal conductances and reversal potentials for the ion $$i$$, and $$n, m, h$$ are gating variables (the degree of opening of a certain ion channel).

<br>
**FitzHugh-Nagumo Model**  
   A simpler, qualitative model of neuronal spiking is given by the FitzHugh-Nagumo equations:<br><br>
   $$
   \begin{align}
   \frac{dV}{dt} &= V - \frac{V^3}{3} - W + I 
   \end{align}
   $$<br><br>
   $$
   \begin{align}
   \frac{dW}{dt} &= \epsilon (V + a - bW)
   \end{align}
   $$<br><br>
   where $$ V $$ represents the membrane potential, $$ W $$ represents a recovery variable, and $$ \epsilon, a, b $$ are parameters.

<br>
**Synaptic Dynamics**  
   The dynamics of a synapse can be described by:<br><br>
   $$
   \begin{align}
   \frac{dS}{dt} = \alpha (1 - S) H(V_{\text{pre}} - V_{\text{thresh}}) - \beta S
   \end{align}
   $$<br><br>

   where $$S$$ is the synaptic strength, $$ V_{\text{pre}} $$ is the presynaptic membrane potential, $$ V_{\text{thresh}} $$ is the threshold potential for synaptic activation, and $$ \alpha, \beta $$ are rate constants. $$ H $$ is the Heaviside step function (peicewise step function).

<br>
**Wilson-Cowan Model**  
   The Wilson-Cowan equations model the dynamics of populations of excitatory and inhibitory neurons:
   $$
   \begin{align}
   \frac{dE}{dt} &= -E + (1 - r_E E) F(c_{EE} E - c_{EI} I + P_E) 
   \end{align}
   $$<br><br>
   $$
   \begin{align}
   \frac{dI}{dt} &= -I + (1 - r_I I) F(c_{IE} E - c_{II} I + P_I)
   \end{align}
   $$
   where $$ E $$ and $$ I $$ are the average activities of excitatory and inhibitory populations, respectively, $$c_{XY} $$ are the connection strengths, $$ P_X $$ are external inputs, and $$r_X $$ are refractory parameters. $$ F $$ is a nonlinear response function.

