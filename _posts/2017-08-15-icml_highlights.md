---
layout: post
title: ICML Highlights
---

A brief teaser of some of my favourite ICML papers. Highly biased selection. More to follow.

### [On Calibration of Modern Neural Networks](http://proceedings.mlr.press/v70/guo17a.html)
The authors make the simple yet striking observation that deep
   neural network classifiers do not output well calibrated
   probabilities. They demonstrate that the softmax output lacks 
   correspondence to the empirical
   classification probability. This does not apply to the previous
   generation of neural networks from the 90s which seem to be
   reasonably well calibrated.
   Three causes are identified and experimentally shown to contribute
   to miscalibration, (1) increased model capacity (2) batch normalisation and (3) a lack of weight decay.
   The authors speculate that this effect can be attributed to
   overfitting the likelihood but not the classification error.
   Several methods for retrospective calibration are investiaged, of
   which *Platt scaling* shows the most promise despite its
   simplicity. This techniques amounts
   to a simple rescaling of the network output that optimises the
   likelihood of a validation set.

### [Scalable Generative Models for Multi-Label Learning with Missing Labels](http://proceedings.mlr.press/v70/jain17a)
   Jain et al. introduce a probabilistic generative model
   for multi-label learning with a potentially large number of
   labels. Label applicability can be represented as a binary
   object-by-label matrix. As commonly done in this type of
   problem [[Bhatia et al., 2015](https://papers.nips.cc/paper/5969-sparse-local-embeddings-for-extreme-multi-label-classification.pdf), [Rai et al., 2015](http://papers.nips.cc/paper/5770-large-scale-bayesian-multi-label-learning-via-topic-based-label-embeddings.pdf)], the authors infer a continuous
   low rank embedding of this label matrix.
   In addition, they explictly model missing observations which are
   assumed to be indistinguisable from absent labels. Moreover, object-specific
   features can be encoded as prior on the object embedding.

   Inference becomes conjugate, using poly the Polia-gamma trick
   [[Polson et al., 2013](https://arxiv.org/pdf/1205.0310.pdf)]. The authors derive a Gibbs sampling algorithm for
   posterior inference as well as EM for point
   estimation. Interestingly, this allows for batch learning, making
   the model scalable. The model outperforms its competitors on a
   variety (but not all) benchmark datasets.
   

### [Discovering Discrete Latent Topics with Neural Variational Inference](http://proceedings.mlr.press/v70/miao17a.html)
   The authors start from latent Dirichlet allocation (LDA) [[Blei et al., 2003](http://jmlr.csail.mit.edu/papers/v3/blei03a.html)]
   where document-wise topic proportions are drawn from a Dirichlet (process) prior
   \begin{align} \theta_d \sim \text{Dir}(\alpha_0)\;. \end{align}
   The topic assignment for a word $$ \omega_n $$ is Mutlinomial
   and the actual word is drawn from a Multinomial conditional on
   parameters $$ \beta_{z_n} $$ (usually also Dirichlet)
   \begin{align} z_n \sim \text{Mult}(\theta_d) \end{align}
   \begin{align} \omega_n \sim \text{Multi}(\beta_{z_n})\;. \end{align}
   The novelty in the paper lies in replacing the Dirichlet prior by a Gaussian
   whose mean and variance are parametrised by multi-layer perceptrons.
   To generate draws from the simplex one of the following
   constructions can be applied to the Gaussian: (i) a softmax (ii) a
   stick-breaking construction, (iii) a recurrent stick-breaking
   construction. 

   Compared to previous work, the model provides a
   more flexible document-topic distribution and adds a nonparametric
   construction that enables a dynamic increase of the number of topics.
   It achieves state-of-the-art performance on several benchmark
   datasets. However, the softmax constructions seems to mostly
   outperform its nonparametric counterparts in
   perplexity.

   Inference is based on stochastic gradient descent on samples from a
   variational approximation of the posterior by an inference network [[Kingma and Welling, 2013](https://arxiv.org/abs/1312.6114)].
