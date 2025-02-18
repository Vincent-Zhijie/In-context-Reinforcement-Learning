# _Title:_ [Transformers Learn Temporal Difference Methods for In-Context Reinforcement Learning](https://arxiv.org/abs/2405.13861) (ICLR 2025 668)

_Author:_ Jiuqi Wang, Ethan Blaser, Hadi Daneshmand, Shangtong Zhang (University of Virginia, MIT LIDS/Boston University)

## Abstract

In-context learning refers to the learning ability of a model during inference time
without adapting its parameters. The input (i.e., prompt) to the model (e.g., transformers) consists of both a context (i.e., instance-label pairs) and a query instance.
The model is then able to output a label for the query instance according to the
context during inference. A possible explanation for in-context learning is that
the forward pass of (linear) transformers implements iterations of gradient descent
on the instance-label pairs in the context. In this paper, we prove by construction that transformers can also implement temporal difference (TD) learning in
the forward pass, a phenomenon we refer to as in-context TD. We demonstrate
the emergence of in-context TD after training the transformer with a multi-task
TD algorithm, accompanied by theoretical analysis. Furthermore, we prove that
transformers are expressive enough to implement many other policy evaluation
algorithms in the forward pass, including residual gradient, TD with eligibility
trace, and average-reward TD.


## Theory

The following theorem shows that a Transformer can learn TD in-context:

<p align="center">
      <img src="img/zhijie wang/4-1.png" width="800" />
</p>

Experimental results to show that Transformers do learn TD in-context:

<p align="center">
      <img src="img/zhijie wang/4-2.png" width="800" />
</p>

Also, Transformers can implement other RL algorithms:

<p align="center">
      <img src="img/zhijie wang/4-3.png" width="800" />
</p>

<p align="center">
      <img src="img/zhijie wang/4-4.png" width="800" />
</p>

<p align="center">
      <img src="img/zhijie wang/4-5.png" width="800" />
</p>

<br>By <i>Zhijie Wang</i><br>

---

# _Title:_ [Transformers as Decision Makers: Provable In-Context Reinforcement Learning via Supervised Pretraining](https://arxiv.org/abs/2310.08566) (ICLR 2024)

_Author:_ Licong Lin, Yu Bai, Song Mei (UC Berkeley, Salesforce AI Research)

## Abstract

Large transformer models pretrained on offline reinforcement learning datasets have demonstrated
remarkable in-context reinforcement learning (ICRL) capabilities, where they can make good decisions
when prompted with interaction trajectories from unseen environments. However, when and how transformers can be trained to perform ICRL have not been theoretically well-understood. In particular, it is unclear which reinforcement-learning algorithms transformers can perform in context, and how distribution mismatch in offline training data affects the learned algorithms. This paper provides a theoretical framework that analyzes supervised pretraining for ICRL. This includes two recently proposed training
methods — algorithm distillation and decision-pretrained transformers. First, assuming model realizability, we prove the supervised-pretrained transformer will imitate the conditional expectation of the expert algorithm given the observed trajectory. The generalization error will scale with model capacity and a
distribution divergence factor between the expert and offline algorithms. Second, we show transformers
with ReLU attention can efficiently approximate near-optimal online reinforcement learning algorithms
like LinUCB and Thompson sampling for stochastic linear bandits, and UCB-VI for tabular Markov
decision processes. This provides the first quantitative analysis of the ICRL capabilities of transformers
pretrained from offline trajectories.


## Theory

The following theorem provides the cumulative reward bound:

<p align="center">
      <img src="img/zhijie wang/3-1.png" width="800" />
</p>

Transformers can also approximate the soft LinUCB in linear bandits:

<p align="center">
      <img src="img/zhijie wang/3-2.png" width="800" />
</p>

<p align="center">
      <img src="img/zhijie wang/3-3.png" width="800" />
</p>

Similarly, the paper also showed the bound for UCB-VI in linear bandits.

<br>By <i>Zhijie Wang</i><br>

---

# _Title:_ [Supervised Pretraining Can Learn In-Context Reinforcement Learning](https://arxiv.org/abs/2210.14215) (NeurIPS 2023)

_Author:_ Jonathan N. Lee, Annie Xie, Aldo Pacchiano, Yash Chandak, Chelsea Finn, Ofir Nachum, Emma Brunskill (Stanford University, Microsoft Research, Google DeepMind)

## Abstract

Large transformer models trained on diverse datasets have shown a remarkable
ability to learn in-context, achieving high few-shot performance on tasks they were
not explicitly trained to solve. In this paper, we study the in-context learning capabilities of transformers in decision-making problems, i.e., reinforcement learning
(RL) for bandits and Markov decision processes. To do so, we introduce and study
Decision-Pretrained Transformer (DPT), a supervised pretraining method where
the transformer predicts an optimal action given a query state and an in-context
dataset of interactions, across a diverse set of tasks. This procedure, while simple,
produces a model with several surprising capabilities. We find that the pretrained
transformer can be used to solve a range of RL problems in-context, exhibiting both
exploration online and conservatism offline, despite not being explicitly trained to
do so. The model also generalizes beyond the pretraining distribution to new tasks
and automatically adapts its decision-making strategies to unknown structure. Theoretically, we show DPT can be viewed as an efficient implementation of Bayesian
posterior sampling, a provably sample-efficient RL algorithm. We further leverage
this connection to provide guarantees on the regret of the in-context algorithm
yielded by DPT, and prove that it can learn faster than algorithms used to generate
the pretraining data. These results suggest a promising yet simple path towards
instilling strong in-context decision-making abilities in transformers.

<p align="center">
      <img src="img/zhijie wang/2-1.png" width="800" />
</p>

## Algorithm

Let $D_j=\lbrace(s_1,a_1,s_1',r_1'),\cdots,(s_j,a_j,s_j',r_j')\rbrace$. The expected loss (eq. 2):

$$
\min_{\theta}\mathbb{E}\_{P_{\text{pre}}}\sum_{j\in[n]}-\log M_{\theta}(a^*\mid s_{\text{query}},D_j).
$$

<p align="center">
      <img src="img/zhijie wang/2-2.png" width="800" />
</p>

## Theory

The equivalence of posterior sampling (PS) and Decision-Pretrained Transformer (DPT):

<p align="center">
      <img src="img/zhijie wang/2-3.png" width="800" />
</p>

<br>By <i>Zhijie Wang</i><br>

---

# _Title:_ [In-context Reinforcement Learning with Algorithm Distillation](https://arxiv.org/abs/2210.14215) (ICLR 2023)

_Author:_ Michael Laskin, Luyu Wang, Junhyuk Oh, Emilio Parisotto, Stephen Spencer, Richie Steigerwald, DJ Strouse, Steven Stenberg Hansen, Angelos Filos, Ethan Brooks, maxime gazeau, Himanshu Sahni, Satinder Singh, Volodymyr Mnih (DeepMind)

## Abstract

We propose Algorithm Distillation (AD), a method for distilling reinforcement
learning (RL) algorithms into neural networks by modeling their training histories with a causal sequence model. Algorithm Distillation treats learning to
reinforcement learn as an across-episode sequential prediction problem. A dataset
of learning histories is generated by a source RL algorithm, and then a causal
transformer is trained by autoregressively predicting actions given their preceding
learning histories as context. Unlike sequential policy prediction architectures that
distill post-learning or expert sequences, AD is able to improve its policy entirely
in-context without updating its network parameters. We demonstrate that AD can
reinforcement learn in-context in a variety of environments with sparse rewards,
combinatorial task structure, and pixel-based observations, and find that AD learns
a more data-efficient RL algorithm than the one that generated the source data.

<p align="center">
      <img src="img/zhijie wang/1-1.png" width="800" />
</p>

## Algorithm

The NLL loss (Eq. 6):

$$
\mathcal{L}(\theta) = -\sum_{n=1}^N\sum_{t=1}^{T-1}\log P_{\theta}(A=a_t^{(n)}|h_{t-1}^{(n)},o_t^{(n)}).
$$

<p align="center">
      <img src="img/zhijie wang/1-2.png" width="800" />
</p>



<br>By <i>Zhijie Wang</i><br>

---





