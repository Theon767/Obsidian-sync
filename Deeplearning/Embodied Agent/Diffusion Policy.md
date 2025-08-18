
![[Diffusion_policy_development.png]]
A Survey on Diffusion Policy for Robotic Manipulation: Taxonomy, Analysis, and Future Directions
[[Diffusion models]] is originally developped for image generation.




## Key Advantages
1. In terms of multi-modal distribution modeling, diffusion models are excellent at capturing multi-modal action distributions. This enables robots to represent multiple valid strategies for the same task (Modeling on conditional data distribution generation, not on data distribution like Behaviour Cloning)
2. With respect to sample efficiency, diffusion policies can reduce data requirements compared to traditional reinforcement learning approaches by learning from demonstrations or limited interactions( NO need get data through trials, instead just directly add noise on gt trajectories to get gt condition trajectories)
3. In relation to generalization capabilities, the flexible representation capabilities of diffusion models allow for better generalization across task variations , object appearances, and environmental conditions. (Modeling on conditional data distribution generation, not on data distribution like Behaviour Cloning)
4. For long-horizon planning, recent advancements have demonstrated that diffusion policies can generate coherent long-horizon action sequences


## How conditioning works?
Observation, states, environments, timesteps, are regarded as conditions. They are encoded and concatenated through dedicated encoder and then serve as combined features for FILM conditioning.
## Models
TO DO
#### Training

#### Testing


