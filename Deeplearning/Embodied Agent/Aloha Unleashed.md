
ALOHA Unleashed, a general imitation learning system for training dexterous policies on robots.
ALOHA Unleashed consists of a framework for scalable teleoperation that allows users to collect data to teach robots, combined with a Transformer-based neural network trained with Diffusion Policy, which provides an expressive policy formulation for imitation learning.
In this paper, we demonstrate that by choosing the appropriate learning architecture combined with a suitable data collection strategy, it is possible to push the frontier of dexterous manipulation with imitation learning.
The data alone is insufficient. The other key ingredient in our approach is a transformer-based learning architecture trained with a diffusion loss
![[Aloha_unleashed.png]]
## [[Deeplearning/Embodied Agent/Diffusion Policy]] in Aloha Unleashed
#### Training
During training, input images and Proprioception(consists of the joint positions and gripper values for each of the arms, for a total of 1201 latent feature dimensions) states are both projected and encoded into latent features, then served as condition to transformer decoder, noisy actions with gt noise serve as input and the transformer decoder outputs noise, the model is then supervised to predict the noise. 
#### Testing
During testing, images and proprioception also serve as condition, first a noise is sampled then the decoder portion runs 50 times to iteratively denoise an action chunk.

## Data Collection
5个真实世界任务（包括系鞋带、挂衬衫、替换机器人手指、插入齿轮和随机厨房堆叠）和3个模拟任务（包括单插、双插和将杯子放在盘子上）
**大规模数据收集**：
在ALOHA 2平台上进行超过26,000个真实机器人演示和2,000个模拟任务演示的数据收集。
开发一个可扩展的遥操作框架，允许用户收集数据来教导机器人，通过详细的协议文档，让非专业用户也能提供高质量的遥操作演示。

## Important Ablation

#### Data quantity in ShirtClean and ShirtMessy tasks
The percentage of data doesn't influence ShirtClean data and has high influence on ShirtMessy data.
#### Data filtering(High quality and low quality both count)
Shorter episodes collected by operators tend to have less mistakes during the trajectory. We see on ShirtEasy that performance improves after some amount of data filtering, improving from 30% success when trained on all episodes, to 55% success when trained on the shortest 50% of episodes. However, when using the shortest 25% of episodes (only 541 episodes, though usually mistake-free demonstrations), performance dips to 40%. 
High quality demonstrations are important for modeling the best behaviors, some amount of suboptimal data may also be necessary to recover from behaviours.

#### Vs ACT
Have over 50% success rate than ACT on shirtmessy

