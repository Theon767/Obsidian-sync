## ODE
P_init --> Pfinal (using ODE)
using NN to simulate vector field 
Goal: Build a flow using the simulated vector field(Distribution of P_data)
X0 ~ P_init ~N(0,1)

Flow is a collection of the ODE with different initial conditions

Training Target: Marginal vector field
## SDE(Stochastic differential equation)
Diffusion models

Training Target: Marginal Score function
Conditional means select one latent variable point $z$ 
Marginal means Across distribution of all latent variable data points (In this case $z$ ingegral) .
The starts of conditional and marginal probability paths are 
both Gaussian distribution.
Terminology: 
1. Conditonal probability Path P_t(.|z) (One sampling)
   Gaussian probability path: P(.|Z)~N(alpha z, $beta$ I_d)
2. Marginal pro path:
   Z ~ $P_{data}$ X ~$P_{t}(.|z)$ -->X~$P_{t}$ (Margilnize)
3. Conditional Vector field
   $u_{t}^{target}(x|z)$ 
   This vector field describes an ODE with $X_t$  ~ $P_t(.|Z)$ (A conditional path)
4.  Marginal vector field
   This marginal vector field describes a marginal path.

Loss: conditional flow matching loss
Q: How to get u_t from z and t.
A: If we assume the Conditional probability path to be Gaussian probability path, then conditional vector field has an analytical solution with respect to conditional probability path.


L_fm=L_cfm+ C