Learning Fine-Grained Bimanual Manipulation with Low-Cost Hardware
## Behavioral Cloning

One of the simplest imitation learning algorithms, casting imitation as supervised learning from observations to actions.
A major shortcoming of BC is compounding errors, where errors from previous timesteps accumulate and cause the robot to drift off of its training distribution, leading to hard-to-recover states. 累积误差是模仿学习中的一个主要问题，其中前期的错误会在时间上累积，导致机器人偏离训练分布(The expert never shows)。解决方法包括允许额外的策略交互和专家纠正（例如DAggger算法）。

## Action Chunking
![[Action_chunking.png]]
Predict the Action in next K step and do this at every timestep, ensemble the corresponding prediction at every timestep and ensemble them. This reduces the effective horizon of the task by k-fold, mitigating compounding errors. 
ACT ensemble: Code(modeling_act.py)


## ACT trained as CVAE(Conditional VAE)
![[ACT_arch.png]]
![[Act_code_structure.png]]

Left is CVAE Encoder which has a transformer encoder that encodes joints and action sequence(Human Operation) into style variable $Z$ (CVAE implies that the CVAE encoder yields mean and variance of style variable $Z$ ). 
Notice: the distribution of Style variable $Z$ is fixed once training is finished(Dialognal Gaussian), during testime the $Z$ is set to $diag(0)$. 
Right is the CVAE Decoder, which takes observations, current joint states and style variable $Z$ as input into a transformer encoder and then feed to a transformer decoder.  
![[Pasted image 20250609104212.png]]
%% ## Positonal Embedding in ACT

It uses the most common adopted positional embeding, e.g. [[Learned positional embeding]] and [[Sinosioudal Positional Embedding]].
Fixed means if using [[Learned positional embeding]], then the parameters are fixed during test time, while [[Sinosioudal Positional Embedding]] has no relationship with training or testing %%.

## Loss
Reconstruction loss + Regularization loss(For Style variable $Z$, KL divergence with respect to standard normal distribution)

## Code(Lerobot)



