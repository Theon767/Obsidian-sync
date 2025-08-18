## Training
Actions are sampled from gt and interpolated with time-step-relevant noise, encoded by mlp. Other observations and states are also encoded individually by mlps and concatenated together to Gemmapaliwithexpert. Then Gemmapali yields v_t, the model is supervised on difference between u_t(noise - actions) and v_t

## Testing
Actions are initially set to noise. Gemmapaliwithexpert uses encoded observations and states (Actions embeds set tot None instially) to generate v_t  and add to noise to gradually refine action(during refinement the actions are once again embed).Integrate the flow field (ODE solving)d1111

### Flow matching and diffusion policy
Flow Matching
use noise to interpolate between actions and noise, then use models to predict velocity(direction) of the noise added.

![[Pasted image 20250606172405.png]]
First expectation: over all possibilities of observation and action(Implemented through: Dataset)
Second expectation: over all possible interpolation combinations of noise and action(Implemented through: random sample $\tau$)
Diffusion Policy
use noise to add to actions, then use models to predict the noise added
