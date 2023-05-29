## A Self-Organizing Neuro-Fuzzy Q-Network: Systematic Design with Offline Hybrid Learning [![DOI](https://zenodo.org/badge/605243965.svg)](https://zenodo.org/badge/latestdoi/605243965)

**TLDR:** A systematic design process for a self-organizing neuro-fuzzy Q-network by using two learning paradigms in tandem: unsupervised learning and an offline, model-free fuzzy RL algorithm called Fuzzy Conservative Q-learning (FCQL). 

**Abstract:** We propose a systematic design process for automatically generating self-organizing neuro-fuzzy Q-networks by leveraging unsupervised learning and an offline, model-free fuzzy reinforcement learning algorithm called Fuzzy Conservative Q-learning (FCQL). Our FCQL offers more effective and interpretable policies than deep neural networks, facilitating human-in-the-loop design and explainability. The effectiveness of FCQL is empirically demonstrated in Cart Pole and in an Intelligent Tutoring System that teaches probability principles to real humans.

![overview](https://github.com/johnHostetter/AAMAS-2023-FCQL/assets/35469358/e7e70547-0dd6-4629-97c7-4da77e1d5095)

**What is the contribution?** The primary novelty and contribution of this work is the proposal of a systematic design process for a neuro-fuzzy Q-network that works with a model-free offline fuzzy RL algorithm. To our knowledge, existing methods within fuzzy RL are either developed for online interaction due to their dependency on exploration, are unable to accommodate for distributional shift, or rely upon the existence of a simulation; furthermore, the only existing work capable of automatic design for offline fuzzy RL is fuzzy particle swarm RL, but this requires a simulation of real system dynamics that may be impractical for many real-world complex applications such as e-learning and healthcare.

### A Demonstration using Cart Pole

The systematic design process can run CLIP and ECM in parallel, but we will first look at CLIP.

![clip_highlighted](https://github.com/johnHostetter/AAMAS-2023-FCQL/assets/35469358/b5ebf024-62e6-423e-8478-fcaebeabc8fb)

**What is "CLIP"?** CLIP stands for "Categorical Learning Induced Partitioning" and is one way of generating Gaussian fuzzy sets dynamically and iteratively. It is inspired by human's behavior category learning and automatically discovers the appropriate number of fuzzy sets within each input dimension. Fuzzy sets must be defined in order to create a neuro-fuzzy Q-networks' knowledge base.

https://github.com/johnHostetter/AAMAS-2023-FCQL/assets/35469358/9388a511-e850-42eb-af4c-297dc2170ef8

Now, we will look at ECM.

![ecm_highlighted](https://github.com/johnHostetter/AAMAS-2023-FCQL/assets/35469358/dbbd6f50-e92e-4b48-b6de-1b6ba0f75c47)

**What is "ECM"?** ECM is the "Evolving Clustering Method". It was originally proposed with the intention of immediately using the resulting clusters as the fuzzy premise for fuzzy logic rules, resulting in _approximate fuzzy logic controllers_. Aapproximate fuzzy logic controllers are less interpretable as their semantics are local and they share no overlapping linguistic terms between the rules. Here, we have modified how its output is used. Specifically, we use the identified centers of the clusters produced by ECM as the _exemplars_. Exemplary data is the most "noteworthy" or "interesting" moments. As such, they are candidates for fuzzy logic rules, as it is in our interest to map exemplars to actions' Q-values.

https://github.com/johnHostetter/AAMAS-2023-FCQL/assets/35469358/6ef5fbd6-37ec-4662-8e87-17ceaa54fbee

The Gaussian fuzzy sets produced by CLIP and the candidate exemplary data from ECM are then given to the widely-used and famous Wang-Mendel Method for fuzzy logic rule generation. 

![wm_highlighted](https://github.com/johnHostetter/AAMAS-2023-FCQL/assets/35469358/79d72ee4-5ea3-4051-a292-93fcb6ed003a)

**What is the "Wang-Mendel Method"?** The Wang-Mendel Method is a common and famous technique for producing fuzzy logic rules in a very simple and straightforward way. That said, it is widely adopted not necessarily due to its effectiveness or efficiency, but because of its simplicity in implementation. Simply put, each data point is examined to see how strongly it belongs to each fuzzy set, and fuzzy rules are generated from the fuzzy sets with a maximum degree of membership. We used the Wang-Mendel Method to generate textual descriptions of the state environments.

https://github.com/johnHostetter/AAMAS-2023-FCQL/assets/35469358/e425b298-9cd2-4140-9bb4-d7613787903d

After completing the Wang-Mendel Method, each fuzzy logic rule only contains fuzzy premises in the form of textual descriptions, but have no associated Q-values for the available actions. These must be learned with FCQL.

![fcql_highlighted](https://github.com/johnHostetter/AAMAS-2023-FCQL/assets/35469358/3015b30a-690a-4fe4-9faf-6c5dede58df1)

**What is FCQL?** FCQL is primarily based on Fuzzy Q-Learning, which treats a fuzzy logic rule as a “state” in the environment —similar to how Tabular Q-Learning behaves —and trains Q-values for each of the rule’s possible actions. To prevent overestimating Q-values in the offline setting, we use the updated formula proposed in Conservative Q-Learning (CQL). 

![formula](https://github.com/johnHostetter/AAMAS-2023-FCQL/assets/35469358/df311f3d-3a4d-46a5-94ac-49e257424f8c)

**Did this paper or code help you?** Please consider citing the [paper](https://www.researchgate.net/publication/368714866_A_Self-Organizing_Neuro-Fuzzy_Q-Network_Systematic_Design_with_Offline_Hybrid_Learning) or [code](https://zenodo.org/badge/latestdoi/605243965). Your support helps ensure the authors can continue researching efficient and robust systematic design of neuro-fuzzy Q-networks!

**Would you like to contact us?** If you wish to reach out to the authors, we would love to hear from you and discuss neuro-fuzzy networks with you! Please reach us at: jwhostet@ncsu.edu

Stay tuned for code updates! :smile:

If you have any issues with the code, please report them via the [Issues](https://github.com/johnHostetter/AAMAS-2023-FCQL/issues) tab.
