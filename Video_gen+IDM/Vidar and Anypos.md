## Vidar(Generalist Bimanual Manipulation via Foundation Video Diffusion Models)

Video Generation(Foundation model pretraining) --> Test-time scaling --> Masker IDM(supervised way) --> Action

## Anypos(AnyPos: Automated Task-Agnostic Actions for Bimanual Manipulation)

Automated Task-Agnostic Random Actions (RL-based EE to rpos to generate Training Dataset)--> using the generated Dataset to train a image-conditioned IDM-solver(Input: Image Output: qpos)(Model Architecture: Arm decopled estimation + Direction Aware Decoder)

训练时：
use reasoning as instructions 是用细颗粒度标注作标签生成动作,action expert 的condition是只有reasoning的，不包含task的(labels 是None)
generate reasoning 监督用vlm生成和标注一样的内容，并且action expert的condition也是基于task+reasoning的(labels不是None)，也可以通过causal mask将resoning去掉

推理时：
use reasoning as instructions 是pi0的forward