# jump_diffusion

The Jump Diffusion Model is an extension of the classical Black-Scholes model for option pricing. The Black-Scholes model assumes that the price of a financial asset follows a continuous process driven by Brownian motion (i.e., Geometric Brownian Motion, GBM). However, in reality, asset prices often exhibit sudden and large changes due to events like earnings announcements, economic news, etc. The Jump Diffusion Model incorporates these sudden jumps by adding a jump component to the standard diffusion process.


Geometric Brownian Motion (GBM): The basic model for asset prices under Black-Scholes is:
dS(t) = S(t) * [mu * dt + sigma * dW(t)]
Where:
S(t) is the asset price at time t.
mu is the drift rate (average return).
sigma is the volatility of the asset.
dW(t) is the increment of a Wiener process (standard Brownian motion).

Poisson Process for Jumps: The model assumes that the number of jumps follows a Poisson process:
dN(t) ~ Poisson(lambda * dt)
Where:
N(t) is the counting process representing the number of jumps up to time t.
lambda is the average number of jumps per unit time.

Jump Size Distribution: The size of the jumps is typically modeled by a log-normal distribution:
Y ~ LogNormal(m, v)
Where:
Y is the relative jump size, i.e., after a jump, the new price is S(t) * Y.
m is the mean of the logarithm of the jump size.
v is the variance of the logarithm of the jump size.

Combined Model: Jump Diffusion Process
The asset price under the Jump Diffusion Model is described by the following stochastic differential equation (SDE):
dS(t) = S(t) * [mu * dt + sigma * dW(t)] + S(t) * (Y - 1) * dN(t)

Breaking it down:
The first part, S(t) * [mu * dt + sigma * dW(t)], represents the continuous part of the process (as in GBM).
The second part, S(t) * (Y - 1) * dN(t), represents the discontinuous jumps in the price:
(Y - 1) represents the percentage change in the asset price due to a jump.
dN(t) is 0 most of the time but equals 1 when a jump occurs, according to the Poisson process.


The expected value and variance of the asset price under the Jump Diffusion Model are influenced by both the continuous diffusion and the jumps. Specifically:

Expected Return: The drift term mu must be adjusted to account for the jumps:
mu' = mu - lambda * (E[Y] - 1)
where E[Y] is the expected value of the jump size Y.

Variance: The variance will have contributions from both the continuous diffusion and the jump components:
Var(S(t)) = (sigma^2 + lambda * (E[Y^2] - E[Y]^2)) * t

To price options under the Jump Diffusion Model, the classic Black-Scholes formula is modified to include the jump component. However, there is no closed-form solution like in the Black-Scholes model; instead, numerical methods such as Monte Carlo simulation or Fourier transform techniques are typically used.
