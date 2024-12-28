## Related work
**In-context Reinforcement Learning with Algorithm Distillation** proposed an algorithm distillation (AD) method to enable Transformers to learn from RL algorithms entirely in-context without 
having to update the network parameter. Following this work, **Supervised Pretraining Can Learn In-Context Reinforcement Learning** propose offline and online test-time deployment, which is 
an improvement to the AD algorithm. They also provided theoretical guarantee that posterior sampling is equivalent to Decision-Pretrained Transformer (DPT) in termns of policy making.
**Transformers as Decision Makers: Provable In-Context Reinforcement Learning via Supervised Pretraining** theoretically studied the two proposed algorithms: AD and DPT. They showed that the 
generalization error will scale with model capacity and a distribution divergence factor between the expert and offline algorithms, and that transformers with ReLU attention can efficiently 
approximate near-optimal online reinforcement learning algorithms like LinUCB and Thompson sampling for stochastic linear bandits, and UCB-VI for tabular Markov decision processes. More recently,
**Transformers Learn Temporal Difference Methods for In-Context Reinforcement Learning** presented the first proof by construction demonstrating that transformers with linear attention can 
implement temporal difference (TD) learning in the forward pass. The paper also demonstrated the emergence of in-context TD after training the transformer with a multi-task TD algorithm.

## Possible future directions:

1. A high level Bayesian point of view (Under what condition will ICRL succeed).

2. Algorithm selection in Reinforcement Learning (Pretrained on different RL algorithm samples).

3. Pretraining perspective analysis (How many pretraining tasks are needed for ICRL).
