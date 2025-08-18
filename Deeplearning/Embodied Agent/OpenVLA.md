VLA(vision language action) Models
#### Characteristics
- it performs alignment of pretrained vision and language components on a large, Internetscale vision-language dataset
- the use of a generic architecture, not custom-made for robot control, allows us to leverage the scalable infrastructure underlying modern VLM training [75–77] and scale to training billion-parameter policies with minimal code modifications
- provides a direct pathway for robotics to benefit from the rapid improvements in VLMs.
#### How to generate actions thorough VLM
##### Action Tokenizer

When training(Generate gt):
converts continuous actions to tokens from the end of the vocabulary.
Continuous action --> (through digital bin(Integer boundary))action token id--> last 256 language token ids(Supervise) --> (tokenizer.decode)Text(Supervise)

When inferring:
convert token IDs to continuous action
The token_id is predicted as the last 256 vocab in the LLMA vocabulary list.
Language token id --> action token id --> continuous action in indexed bin centers
