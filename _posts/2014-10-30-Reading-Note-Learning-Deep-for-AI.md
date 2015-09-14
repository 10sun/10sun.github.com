---
layout : post
category : ReadingNotes
tags : [DeepLearning, DBN]
---
{% include JB/setup %}

*"Learning Deep Architectures for AI"* <a href="http://www.iro.umontreal.ca/~bengioy/papers/ftml_book.pdf" target="_blank">link</a> gives a brief introduction about one main type of deep learning algorithms, *Deep Belief Networks (DBNs)*. It starts with the motivation for deep architecture, after which is the brief theoretical introduction of *DBNs*. This reading notes tries to summarize the arguments, theorems, proofs, fomulars and algorithms in chapter wise.

**Ch1. Introduction**

- *Concepts*
    + *Depth of architectures:* the number of levels of composition of non-linear operations in the function learned. (shallow architectures: 1, 2, or 3 levels). Mammal brain is in a deep architecture [<a href="http://serre-lab.clps.brown.edu/wp-content/uploads/2012/08/Serre_etal_PBR07_wfig.pdf" target="_blank">173</a>].
    + *Distributed representation [<a href="http://www.cogsci.ucsd.edu/~ajyu/Teaching/Cogs202_sp12/Readings/hinton86.pdf" target="_blank">68</a>,<a href="http://www.iro.umontreal.ca/~vincentp/ift3395/lectures/backprop_old.pdf" target="_blank">156</a>]:* the information is not localized in a particular neuron but distributed.
- *Arguments*
    + The *motivation of deep learning* is to *automatically discover abstractions from the lowest level features to the highest level abstract concepts*. The ideal learning algorithms are desired to *discover these features with as little human effort as possible*, without having to manually define all necessary abstractions or having to provide a huge set of relevant hand-labeled samples.
    + The *aim of deep learning methods* is to *learn feature hierarchies with features from higher levels of the hierarchy formed by the composition of lower level features*.
    + *Automatical feature learning at multiple levels of abstraction* allows a system to learn complex (non-linear) functions mapping the input to the output directly from data, without depending completely on human-crafted
<!--more-->
    features. *Important for high-level features*: since humans often do not know how to specify explicitly in terms of raw sensory input.
    + **Breakthrough in 2006**
        * <cite>Hinton et al [<a href="https://www.cs.toronto.edu/~hinton/absps/fastnc.pdf" target="_blank">73</a>], greedy layer-wise learning algorithm exploiting an unsupervised learning algorithm for each RBM layer [<a href="http://cseweb.ucsd.edu/~yfreund/papers/freund94unsupervised.pdf" target="_blank">51</a>]</cite>
        * <cite>auto-encoders proposed [<a href="http://papers.nips.cc/paper/3048-greedy-layer-wise-training-of-deep-networks.pdf" target="_blank">17</a>, <a href="http://papers.nips.cc/paper/3112-efficient-learning-of-sparse-representations-with-an-energy-based-model.pdf" target="_blank">153</a>]. guiding the training of intermediate levels of representation using unsupervised learning, which can be performed locally at each level.</cite>
        * <cite>deep convolutional neural network</cite>
    + Observation found with many successful experiment: once a good representation has been found at each level, it can be used to initialize and successfully train a deep neural network by supervised gradient-based optimization.
    + Brain has *sparse and *distributed representation* to process visual information.
    + Deep architectures natually provide *sharing* and *re-use components* for multi-task learning: low-level visual features and intermediate-level visual features are useful for a large group of visual tasks. *Deep learning algorithms are based on learning intermediate representations which can be shared across tasks*.
    + Learning about a large set of interrelated concepts might provide a key to the kind of broad generalizations that human appear able to do.
- *Bibliography*
    + <cite>[<a href="http://serre-lab.clps.brown.edu/wp-content/uploads/2012/08/Serre_etal_PBR07_wfig.pdf" target="_blank">173</a>] biological side of how human brain processes the information. The brain appears to process information through multiple stages of transformation and representation, especially in primate visual system.</cite>
    + <cite>[<a href="http://papers.nips.cc/paper/3048-greedy-layer-wise-training-of-deep-networks.pdf" target="_blank">17</a>, <a href="http://papers.nips.cc/paper/3112-efficient-learning-of-sparse-representations-with-an-energy-based-model.pdf" target="_blank">153</a>] auto-encoder based deep architecture learning algorithm</cite>
    + <cite>[<a href="http://ronan.collobert.com/pub/matos/2008_nlp_icml.pdf" target="_blank">37</a>] poverty of labeled data solved by dln.</cite>

**Ch2. Theoretical Advantages of Deep Architectures**

- *Concepts*
    + *Computational elements*: logical gates (AND, OR, NOT), affine transformation, kernel computation.
    + *Compact function*: the expression of a function is compact when it has few computational elements.
    + *artificial neuron*: an *affine transformation followed by a non-linearity*.
    + Monotone weighted threshold circuits: multi-layer neural networks with linear threshold units and positive weights.
- *Arguments*
    + The formal arguments for the power of deep architectures investigate into two directions:
        * **Computational Complexity of Circuits**: Deep architectures can **compactly represent** *highly varying functions* which would otherwise require a very large size to be represented with an inappropriate architecture, normally in *exponential times*.
        * A function which can be expressed by the composition of computational elements from a given set, can be pictured as a graph formalizing the composition with one node per computational element. *Depth of architecture refers to the depth of that graph*.
        * The composition of computational units in a small but deep circuit can actually be seen as an efficient factorization of a large but shallow circuit.
        * The *depth of architectures* is very *important* for *statistical efficiency*.
- *Bibliography*
    + <cite>[<a href="http://www.iro.umontreal.ca/~vincentp/ift3395/lectures/backprop_old.pdf" target="_blank">156</a>]: multilayer neural network: putting artificial neurons into the set of computational elements.</cite>
    + <cite>[<a href="http://www.nada.kth.se/~johanh/montresholdcircuit.pdf" target="_blank">63</a>]: Theorem 2.1: monotone weighted threshold circuits </cite>
    + <cite>[<a href="http://yann.lecun.com/exdb/publis/pdf/bengio-lecun-07.pdf" target="_blank">19</a>, <a href="https://people.cs.umass.edu/~lrn/papers/neco-stl.pdf" target="_blank">191</a>]: discussion on the power of deep architectures and their potential for AI</cite>
    + <cite>[<a href="http://dl.acm.org/citation.cfm?id=640192" target="_blank">140</a>] an early survey of theoretical results in computational complexity relevant to machine learning algorithms.</cite>

**Ch3. Local vs. Non-local Generalization**

- *Concepts*
    + *Local in input space estimator*: an estimator obtains good generalization for a new input \\(x\\) by mostly *exploiting training samples in the neighborhood of \\(x\\)*.
    + *Parity function*: a boolean function whose value is 1 if and only if the input vector has an odd number of ones.
    + *Local kernel*: a kernel is locak when \\(k(x, x_i) > row\\) is true only for \\(x\\) in some connected region around \\(x_i\\) (for some threshold row). \\(x_i\\) is he training sample, while \\(x\\) is the input sample to be learned/classified.
    + *Distributed representation*: the input pattern is represented by *a set of features* that are *not mutually exclusive and might even be statistically independent*.
- *Arguments*
    + *Curse of dimension*: what matters for generalization *the number of "variations" of the function we wish to obtain* after learning.
    + Architectures based on matching local templates can be thought of as having two levels:
        * \\(1^{st}\\) level: input sample will be matched to a set of templates, with an output of a value indicating the degree of matching.
        * \\(2^{nd}\\) level: perform a kind of interpolation to predit with template the input sample mostly fits in.
        $$ f(x) = b + \sum_i {\alpha_i K (x, x_i)}$$
    + *Kernal machine is the prototypical example of local matching architecture*. It yields generalization by exploiting the *smoothness prior*.
    + For a maximally varying function such as the parity function, the number of examples necessary to achieve some error rate with a Gaussian kernel machine is *exponential* in the input dimension.
    + *Biggest disadvantage of supervised, semi-supervised learning algorithms based on neighbor graph*: they need *as many samples as there are variations of interest in the target function*, and they *cannot generalize to new variations not covered in the training set*.
    + Local representation for a vector can be represented in a much more compact way with the help of distributed representation (*exponentially*).
- *Bibliography*
    + <cite>[<a href="https://www.cs.toronto.edu/~hinton/absps/dbngp.pdf" target="_blank">160</a>] a Gaussian Process kernel machine can be improved using a Deep Belief Network to learn a feature space</cite>
    + <cite>[<a href="http://www.sciencedirect.com/science/article/pii/S0885064X99905198" target="_blank">41</a>] computational complexity literature tells that the number of training examples necessary to achieve a given error rate is exponential in the input dimension.</cite>
    
**Ch4. Neural Networks for Deep Architectures**

- *Concepts*
    + *Neural Network*: multilayer perceptron.
        * *equation of each layer*: 
        $$h^k = tanh(b^k + W^k h^{k-1})$$
        This equation performs an *additional nonlinear computation on top of the affine transformation*. The hyperbolic tangent non-linearity can be replaced by sign function, softamx function, etc..
        * *loss function*: 
        $$L(h^l, y) = -logP(Y = y\mid x) = -log h_{y}^{l}$$
        Loss function is typically *convex* in \\(b^l + W^l h^{l-1}\\).
        * *training rule*: The target is to *reduce the loss of the prediction*. By that, it means to *minimize the log-likelihood of the conditional probability of \\(y\\) given \\(x (P(y\mid x))\\)*.
    + Sigmoid belief network: *units in each layer are independent given the values of the units in the layer above*.
    + Deep belief network: similar to sigmoid networks, but top two layers are RBM.
    + LeCun's Convolutional neural networks: convolutional layers, subsampling layers, error gradient. Each neuron is associated with a fixed two dimenional position that corresponds to a location in the input image, along with a receptive field.
    + Auto-encoder: encode the input \\(x\\) into some representation \\(c(x)\\) so that *the input can be reconstructed from that representation*.
    + Training distribution: the *emperical distribution of the training set*, or the generating distribution for our training samples.
    + Model distribution: the *probability distribution of the trained model*.
- *Arguments*
    + *Difficulties in training deep architectures*:
        * *random initialization of network parameters* often leads to "*apparent local minima or plateaus*"
        * the deeper the network goes, the worse the generalization we get.
    + *Greedy layer-wise unsupervised training* (RBM, auto-encoder) helps to *initialize the network's parameters*, which *improves the generalization performance*.
    + Possible explanation for the *improvements brought by unsupervised pre-training*.
        * These unsupervised training algorithms have layer-local unsupervised criteria. That helps *guide the parameters of that layer towards better regions in parameter space*.
        * Unsupervised pre-training can be seen as *a form of regularizer* (and prior): unsupervised pre-training amounts to *a constraint on the region in parameter space where a solution is allowed*.
        * The effect of unsupervised learning is mostly marked for the lower layers of a deep architecture, which means it is more in the "optimization" direction.
        * Unsupervised pre-training helps generalization by *allowing for a better tuning of lower layers a deep architecture*. With unsupervised pre-training, *the lower layers are constrained to capture regularities of the input distribution*.
        * The unsupervised pre-training does *not only* help to *regularize* the nework, *but also* helps to *optimize* the weights of the lower layers in the deep architecture.
        * The gradient descent criterion defined at the output layer becomes less useful as it propagates backwards to the lower layer. That's why the generalization error is poor with random parameter initialization. Because the criterion cannot help optimize the lower level layer parameters.
        * Generally speaking, *unsupervised learning could help reduce the dependency on the unreliable update direction given by the gradient of a supervised criterion*. It also helps to decompose the problem into sub-problems associated with different levels of abstraction.
    + *Convolutional neural networks is not difficult to train even without unsupervised pre-training*.
    + *One issue with auto-encoder: potential of learning the identiy function.* If there is no other constraint, the auto-encoder with n-dimensional inout and an encoding of dimension at least n could potentially just learn the identity function. (Is this problem a kind of overfitting problems?)
        * This might be *avoided by using the stochastic gradient descent with early stopping*, which is similar to an \\(l_2\\) regularization of the parameters. 
        * *adding noises to the encoding* may help avoid this problem as well.
    + *Denoising auto-encoder* not only tries to *encode the input* but also to *capture the statistical structure in the input, by approximately maximizing the likelihood of a generative model*. This *maximizes a lower bound on the log-likelihood of a generative model*.
- *Bibliography*
    + <cite>[73] initial experiments using RBM for each layer</cite>
    + <cite>[17,98,99] statistical comparisons to prove the advantage of unsupervised pre-training versus random initialization</cite>
    + <cite>[50] unsupervised pre-training acts more like a data dependent "regularizer".</cite>
    + <cite>[91] generative models can often be represented as graphical models</cite>
    + <cite>[83] convolutional nets were inspired by the visual system's structure.</cite>
    + <cite>[101,104] LeCun's state of art convolutional neural network on visual classification tasks. error-gradient</cite>
    + <cite>[45, 111] imported convolutonal structure into DBN, design of a generative version of pooling/subsampling units.</cite>

**Ch5. Energy based Models and RBM**

- *Concepts*
    + *Energy based model*: The model associates *a scalar energy to each configuration of the variables of interst*. 
    $$P(x) = \frac{e^{-Energy(x)}}{Z} ,$$
    where \\(Z = \sum_x e^{-Energy(x)}\\) is the partition function as a sum running over the input space.
    + *Boltzmann machine*: Energy function of a BM is
    $$Energy(x,h) =  -b^{'}x - c^{'}h - h^{'}Wx - x^{'}Ux - h^{'}Vh$$.
    These parameters (offsets and weights) are collectively denoted by \\(\theta\\).
    + *Restricted Boltzmann Machine (RBM)*: Building block of the DBN. It shares parametrization with individual layers of a DBN.
        * *Hidden units are **independent** of each other*, when *conditioning on visible units \\(x\\)*. Likewise for visible units.
        * Energy function:
            $$Energy(x,h) = -b^{'}x - c^{'} - h^{'}Wx$$
          Free energy function:
            $$ FreeEnergy(x) = -b^{'}x - \sum_i log \sum_{h_i}e^{j_i (c_i + W_ix)}$$
        * Conditional probability: 
            $$P(h_i = 1|x) = \prod_{i} P(h_i | x) P(x | h) = \prod_{i}P(x_i | h) $$,
            in binary case:
            $$ P(h_i = 1 | x) = \frac{e^{c_i + W_ix}}{1 + e^{c_i + W_ix}} = sigm(c_i + W_ix)$$
            $$ P(w_i = 1 | h) = \frac{e^{b_i + W_ih}}{1 + e^{b_i + W_ih}} = sigm(b_i + W_ih)$$
    + *CD-K*: the idea of k-step contrastive divergence involves two approximations:
        * Replace average over all possible inputs by a simple sample
        * Run the MCMC (Monte Carlo Markov Chain) chain \\(x_1, x_2, ... , x_{k+1}\\) for only \\(k\\) steps starting from the observed example \\(x_1 = x\\).
        * Equation: \\( \Delta \theta \propto \frac{\partial{FreeEnergy(x)}}{\partial{\theta}} - \frac{\partial{FreeEnergy(\widetilde{x})}}{\partial{\theta}}\\)
    + *Persistent MCMC for Negative Phase*: instead of CD-k for updating parameters, an MCMC chain is kept in the background to obtain the negative phase samples \\((x,h)\\).
    + *Score matching*: the score function of a distribution is defined as \\(\Psi = \frac{\partial{logp(x)}}{\partial{x}}\\). This does not depend on the normalization constant. The idea is to *match the score function of the model with the score function of the empirical density*.
- *Arguments*
    + Boltzmann Machine is defined by an energy function \\(P(x)=e^{-E(x)/Z)}\\). Due to the quadratic interaction in \\(h\\), *an Monte Carlo Markov Chain sampling procedure can be applied to obtain a stochastic estimator of the gradient (log-likelihood gradient).* 
    $$ 
    \begin{aligned}
        \frac{\partial{logP(x)}}{\theta} &= \frac{\partial{log \sum_h e^{-Energy(x,h)}}}{\theta} - \frac{\partial{log\sum_{\widetilde{x},h}e^{-Energy(\widetilde{x},h)}}}{\theta} \\\\
        & = -\frac{1}{\sum_h e^{-Energy(x,h)}}\sum_h e^{-Energy(x,h)}\frac{\partial{Energy(x,h)}}{\partial{\theta}} + \frac{1}{\sum_{\widetilde{x},h}e^{-Energy(\widetilde{x},h}}\sum_{\widetilde{x},h}\frac{\partial{Energy(\widetilde{x},h)}}{\partial{theta}} \\\\
        & = -\sum_h P(h|x)\frac{\partial{Energy(x,h)}}{\partial{\theta}} + \sum_{\widetilde{x},h}\frac{\partial{Energy(\widetilde{x},h)}}{\partial{\theta}} 
        \end{aligned}
    $$
        * Derivatives are easy to compute. Hence *the only difficulty* here is to *propose a sampling procedure to sample from \\(P(h\mid x)\\) and one to sample from \\(P(x,h)\\), to approximate the log-likelihood gradient of Boltzmann machine*.
        * MCMC sampling approach is based on *Gibbs Sampling*. *Sampled sample of \\(x's\\) distribution converges to \\(P(x)\\) as the number of sampling step goes to infinity under some conditions.*
    + In a boltzmann machine, for binary sample units, \\(P(S_i\mid S_{-i})\\) can be expressed as a usual equation for a neuron's output in terms of other neurons \\(S_{-i}\\). (\\(sigm(d_i + 2a_{-i}^{'}s_{-i})\\))
    + *Two MCMC chains* are needed for each sample \\(x\\). *The positive phase*, in which *\\(x\\) is clamped and \\((h\mid x)\\) is sampled*; *the negative phase* in which *\\((x,h)\\) is sampled*. *The computation of the gradient can be very expensive and the training time will be very long*. These are why Boltzmann machine was replaced by back-propagation for multi-layer neural network in 1980s.
    + For *continous-valued inputs*, *Gaussian input units* are better than binomial units (binary units).
    + Adding a hidden unit can always improve the log-likelihood.
    + RBM can also seen as a multi-clustering. Each hidden unit creates a two-region partition of the input space. \\(n\\) hidden units make \\(2^n\\) components mapped from the input space. This doesn't mean that every possible configuration of hidden unit will have an associated region in the input sapce.
    + *Sampling from an RBM* is useful for several reasons:
        1. It obtains *the estimator of the log-likelihood gradient*.
        2. Inspection of examples generated from the model helps get an idea of what the model has captured or not captured about the data distribution.
    + *Contrastive divergence* is *an approximation of the log-likelihood gradient* that is successful for training RBMs.
        1. *Empirically, even \\(k=1\\) (CD-1) often gives good results.* Taking \\(k\\) larger than 1 gives more precise results.
        2. *CD-k corresponds to keeping the first \\(k\\) terms of a series that **converges to the log-likelihood gradient***.
        3. Gibbs sampling does not need to sample in the positive phase, since the free energy is computed analytically.
        4. Set of variables of \\((x,h)\\) can be sampled in two sub-steps in each step of the Gibbs chain.
        5. Traiing an energy-based model is to *make the energy of observed inputs smaller*, and *to shovel energy elsewhere*.
    + The *contrastive divergence* algorithm is fueled by *the contrast between the statics collected when the input data is a real training sample*, and *that when the input data is a chain sample*.
    + The Gibbs chain can be associated with an infinite directed graphical model, and the convergence of the chain justifies Contrastive Divergence.
    + The training of an energy-based model can also be considered to solve a series of classification problems, in which *one tries to discriminate training examples from samples generated by the model*. The expression for the log-likelihood gradient corresponds to the one obtained for energy-based models, where training examples from \\(P_1\\) as positive samples, model samples as negative examples.
- *Theorem*
    + Consider the converging Gibbs chain \\(x_1 \rightarrow h_1 \rightarrow x_2 \rightarrow h_2 ...\\) starting at data point \\(x_1\\). The log-likelihood gradient can be written:
        $$ \frac{\partial{P(x_1)}}{\partial{\theta}} = -\frac{\partial{FreeEnergy(x_1)}}{\partial{\theta}} + E[\frac{\partial{FreeEnergy(x_t)}}{\partial{\theta}}] + E[\frac{\partial{logP(x_t)}}{\partial{\theta}}] $$
        and the final term converges to 0 as \\(t\\) goes to infinity. (\\( E[\frac{\partial{logP(x_t)}}{\partial{\theta}}] \rightarrow 0, when t \rightarrow \infty\\))
- *Bibliography*   
    * <cite>[<a href="https://www.ics.uci.edu/~welling/publications/papers/GenHarm3.pdf" target="_blank">200</a>] general formulation where x and h can be in any of the exponential family distributions.</cite>
    * <cite>[<a href="http://www.gatsby.ucl.ac.uk/aistats/fullpapers/217.pdf" target="_blank">31</a>] extensive numerical comparison of training with CD-k vs. exact log-likelihood gradient.</cite>
    * <cite>[<a href="http://www.iro.umontreal.ca/~lisa/pointeurs/cd_expansion_nc_final.pdf" target="_blank">12</a>] demonstrates Theorem 5.1 which shows how one can expand the log-likelihood gradient for any t >= 1. Demonstration of the expansion of the log-likelihood of P(x_1) in a Gibbs chain.</cite>
    * <cite>[<a href="http://www.cs.toronto.edu/~hinton/science.pdf" target="_blank">75</a>] unfold the deep auto-encoder to form a very deep auto-encoder and fine tune the global reconstruction error.</cite>
    * <cite>[<a href="http://www.enterrasolutions.com/media/docs/2013/08/cogscibm.pdf" target="_blank">1</a>,<a href="https://www.cs.toronto.edu/~hinton/absps/pdp7.pdf" target="_blank">76</a>,<a href="http://www.cs.utoronto.ca/~hinton/absps/bmtr.pdf" target="_blank">77</a>] papers about Boltzmann Machine.</cite>
    * <cite>[<a href="http://www.cs.princeton.edu/courses/archive/spr06/cos598C/papers/AndrieuFreitasDoucetJordan2003.pdf" target="_blank">4</a>] Monte Carlo Markov Chain.</cite>
    * <cite>[<a href="http://www.stat.cmu.edu/~acthomas/724/Geman.pdf" target="_blank">57</a>] gibbs sampling</cite>
    * <cite>[<a href="http://papers.nips.cc/paper/2275-self-supervised-boosting.pdf" target="_blank">201</a>] understand the value of these samples from the model in improving the log-likelihood.</cite>

**Ch6. Greedy Layer-wise Training of Deep Architectures**

- *Concepts*
    + *Deep Belief Networks (DBNs)*: a **generative model** (generative path with \\(P\\) distributions) and a mean to extract multiple levels of representation of the input (recognition path with \\(Q\\) distributions).
     ![Deep Belief Network as a generative model](/images/DBN.png "DBN network")
- *Arguments*
    + Deep Belief Network with \\(l\\) layers *models the joint distribution between observed vector \\(x\\) and \\(l\\) hidden layers \\(h^k\\)* as follows:
    $$ P(x, h^1, ... , h^l) = (\prod_{h^k}^{h^{k+1}}P(h^k|h^{k+1}))P(h^{l-1}, h^l)$$
    + *Distribution \\(P(h^{k-1}\mid h^k)\\) and \\(P(h^{l-1}, h^l)\\) define the generative model.*
    + *Training of the DBN*:
        * *Recognition phase*:
            - first sample \\(h^1 ~ Q(h^1\mid x)\\) from first level RBM, or alternatively with a mean-field approach using \\(\overline{h^1} = E[h^1\mid x]\\).
            - take the output of first-level RBM as the input for the second-level RBM and compute the \\(h^2\\).
            - repeat this until the last layer.
            - once all the layers' parameters are learned, these parameters can be used to initialize a deep multi-layer neural network, which can be fine tuned with the help of supervised learning.
        * *generative phase*:
            - sample a visible vector \\(h^{l-1}\\) from top-level RBM. Use CD-k (Gibbs chain in the RBM alternating between \\(h^l ~ P(h^l \mid h^{l-1})\\) and \\(h^{l-1} ~ P(h^{l-1}\mid h^l)\\)).
            - for \\(k=l-1\\) down to 1, sample \\(h^{k-1}\\) given \\(h^k\\) according to the level-k hidden-to-visible conditional distribution \\(P(h^{k-1}\mid h^k)\\).
            - \\(x=h^0\\) is the DBN sample.
    + Training of stacked auto-encoder: it just changes the RBM to auto-encoder. So the initialization of parameters are done by reconstruction error minimization.
    + In general, the DBN has an edge over stacked auto-encoders. However, denoising auto-encoder is comparable to DBN, which performs the stochastic approximation.
- *Bibliography*
    + <cite>[<a href="https://www.cs.toronto.edu/~hinton/absps/fastnc.pdf" target="_blank">73</a>] learning algorithm for DBN by G.Hinton.</cite>
    + <cite>[<a href="http://papers.nips.cc/paper/2979-efficient-sparse-coding-algorithms.pdf" target="_blank">109</a>, <a href="http://www.cs.stanford.edu/people/ang//papers/icml07-selftaughtlearning.pdf" target="_blank">148</a>] self-taught learning</cite> 

**Ch7. Variants of RBMs and Auto-encoders**

- *Concepts*
    + sparse deep architecture
    + *Denoising auto-encoders*: stochastic version of the auto-encoder where *the input is stochastically corrupted*, however *the uncorrupted input is still used as target for the reconstruction*.
        * Training criterion: a *reconstruction log-likehood* \\(-logP(x\mid c(x^{\overline{x}}))\\), where \\(x\\) is the uncorrupted input, \\(\overline{x}\\) is the corrupted one, and \\(c(\overline{x})\\) is the code obtained from \\(\overline{x}\\).
    + Lateral connections: introduce lateral connections between visible units.
    + Conditional RBMs: some of the parameters are not free, but instead parametrized functions of a conditioning random variable. Generalizing RBMs to conditional RBMs allows building deep architectures in which the hidden variables at each level can be conditioned on the value of other variable.
    + Temporal RBMs: an extension of conditional RBM. The parameters (offsets and weights) are not only conditional on past inputs, but also past values of the state (units). it explores the temporal dependencies of the signal in time domain. 
    + Factorized RBMs: for probabilistic language models.
- *Arguments*
    + why the sparse representation?
        1. if one is to have fixed-size representations, *sparse representations are more efficient than non-sparse ones in an information-theoretic sense*, allowing for varying the effective number of bits per example.
        2. the fixed-length representation is going to be used as input for further processing so that it should be easy to interpret. A highly compressed encoding is usually highly entangled so that no subset of bits in the code can really be interpreted unless all the other bits are taken into account. But *sparse representation allows a subset or an individual bit can interpret some features of the data*, which might be sufficient for some particular prediction tasks.
    + In compressed sensing, sparsity is achieved with the \\(l_1\\) penalty on the codes. Given bases in matrix \\(W\\), we look for codes \\(h\\) such that the input signal \\(x\\) is reconstructed with low \\(l_2\\) reconstruction error while \\(h\\) is sparse: \\( min_h \left \| x- Wh \right \|_2^2 + \lambda \left \|h \right \|_1 \\), where \\(\left \|h \right \|_1 = \sum_i \left \|h_i \right \|\\)
    + *sparse coding performs a kind of explaining away*: it chooses one configuration among many of the hidden codes that could explain the input.
        1. advantage: if a cause is much more probable than the other, then it is the one that we want to highlight.
        2. disadvantage: 
            1. it makes *the resulting codes somewhat unstable*. small perturbations of the input x could give rise to very different values of the optimal code h.
            2. optimizing equation 7.1 is efficient, it can be hundreds of time slower than the kind of computation involved in computing the codes in ordinary auto-encoders or RBMs, making both training and recognition very slow.
            3. *joint optimization of the bases \\(W\\) with higher levels of a deep architecture is another stability issue*.
    + sparse auto-encoders and sparse RBMs do not suffer from any of these sparse coding issues. This is because *sparse coding systems only parametrize the decoder*, while *the encoder is defined implicitly as the solution of an optimization*. Instead, an ordinary auto-encoder or an RBM has **an encoder part \\((P(h\mid x))\\)** and **a decoder part \\((P(x\mid h))\\).**
    + middle ground between ordinary auto-encoders and sparse coding. Let the codes \\(h\\) be free but include a parametric encoder and a penalty for the difference between the free non-parametric codes \\(h\\) and the outputs of the parametric encoder.
    + Lateral connections capture pairwise dependencies that can be more easily captured this way than using hidden units, saving the hidden units for capturing higher-oder dependencies.
        1. advantage: the higher level factors represented by the hidden units do not have to encode all the local "details" that the lateral connections at the levels below can capture.
    + Contrastive Divergence for RBMs can be easily generalized to the case of conditional RBMs.
    + Generalisation of RBM: *a generalized RBM is an energy-based probabilistic model with input vector \\(x\\) and hidden vector \\(h\\) whose energy function is such that \\(P(h\mid x)\\) and \\(P(x\mid h)\\) both factorise.* Complementary priors allow the posterior distribution \\(P(h\mid x)\\) to factorize by a proper choice of \\(P(h)\\).

    
    > Proposition 7.1 The energy function associtated with a model of the form of Equation (5.5) such that \\(P(h\mid x) = \prod_i P(h_i\mid x)\\) and \\(P(x\mid h)=\prod_j P(x_j\mid h)\\) must have the form \\(Energy(x,h) = \sum_j \phi_j(x_j) + \sum_i \xi_i(h_i) + \sum_{i,j} \eta_{i,j}(h_i, x_j) (7.7)\\).
    >
    
    + Contrastive divergence update in this generalized RBM:
        $$ FreeEnergy(x) = -log\sum_h exp(-\sum_{i,j} \eta_{i,j}(h_i, x_j))$$
        The gradient of the free energy of a sample \\(x\\) is thus
        $$ 
        \begin{aligned}
            \frac{\partial{FreeEnergy(x)}}{\partial{\theta}} & = \sum_h\frac{exp(-\sum_{i,j}\eta_{i,j}(h_i, x_j))}{\sum_h exp(-Í\sum_{i,j}\eta_{i,j}(\widetilde{h_i}, x_j))}\sum_{i,j}\frac{\partial{\eta_{i,j}(h_i, x_j)}}{\partial{\theta}} \\\\
            & = \sum_h P(h|x)\sum_{i,j}\frac{\partial{\eta_{i,j}(h_i, x_j)}}{\partial{\theta}}\\\\
            & = E_h[\sum_{i,j}\frac{\partial{\eta_{i,j}(h_i, x_j)}}{\partial{\theta}}|x]
        \end{aligned}
        $$
- *Bibliography*
    + <cite>[<a href="http://www.cs.toronto.edu/~ranzato/publications/ranzato-nips07.pdf" target="_blank">150</a>] justify the sparsity of the representation in the context of models based on auto-encoders. how one might get good models even though the partition function is not explicitly minimized, or only minimized approximately as long as other constraints are used on the learned representation.</cite>
    + <cite>[<a href="http://ai.stanford.edu/~ang/papers/nips07-sparsedeepbeliefnetworkv2.pdf" target="_blank">110</a>] training sparse DBN.</cite>
    + <cite>[<a href="http://www.iro.umontreal.ca/~vincentp/Publications/denoising_autoencoders_tr1316.pdf" target="_blank">195</a>]shows how the strategy is highly successful as unsupervised pre-training for a deep architecture, and links the denoising auto-encoder to a generative model.</cite>
    + <cite>[<a href="http://www.cs.toronto.edu/~osindero/PUBLICATIONS/OsinderoHinton_ModelingImagePatchesWithDHMRFs_NIPS07_final.pdf" target="_blank">141</a>] model based on lateral connected RBMs, proves that DBN based on this model generates more realistic image patches than DBN based on ordinary RBMs.</cite>
    + <cite>[<a href="http://redwood.berkeley.edu/bruno/papers/VR.pdf" target="_blank">139</a>] whitening is useful for image processing systems.</cite>
    + <cite>[<a href="https://www.cs.toronto.edu/~hinton/absps/fastnc.pdf" target="_blank">73</a>] energy function associated with a model of the the form of Equation 5.5 such that P(h\mid x) and P(x\mid h) must have the form.</cite>
    
**Ch8. Stochastic Variational Bounds for Joint Optimization of DBN Layers**

- *Concepts*
    + *KL Divergence*: a.k.a. *relative entropy*. a non-symmetric *measure of the difference between two probability distributions \\(P\\) and \\(Q\\)*. Specially, *KL divergence of \\(Q\\) from \\(P\\) is to measure the information lost when the \\(Q\\) is used to approximate the \\(P\\).*  
    + *wake-sleep algorithm*: wake phase & sleep phase
      1. *wake phase updates for the weights of the top RBM.* sample \\(x\\) from the training set generate \\(h ~ Q(h\mid x)\\) and use this \\((h,x)\\) as fully observed data for training \\(P(x\mid h)\\) and \\(P(h)\\).
      2. sleep phase: sample \\((h,x)\\) from model \\(P(x,h)\\) and use that pair as fully observed data for training \\(Q(h\mid x)\\).
- *Arguments*
    + The *log-likelihood of a DBN* can be *lower bounded* using *Jensen's inequality*, and can *justify the greedy layer-wise training strategy.*</br>
    \begin{align} 
    logP(x) &= (\sum_h Q(h|x))logP(x) = \sum_hQ(h|x)log\frac{P(x,h)}{P(h|x)}\\\\
            & = \sum_hQ(h|x)log\frac{P(x,h)}{P(h|x)}\frac{Q(h|x)}{Q(h|x)}\\\\
            & = \sum_hQ(h|x)logP(x,h) - \sum_hQ(h|x)logQ(h|x) + \sum_hQ(h|x)log\frac{Q(h|x)}{P(h|x)} \\\\
            & = \sum_hQ(h|x)logP(x,h) + H_{Q(h|x)} + KL(Q(h|x)||P(h|x))\\\\
            & = KL(Q(h|x)||P(h|x)) + H_{Q(h|x)} + \sum_hQ(h|x)lop(P(h)P(x|h))\\\\
            & = KL(Q(h|x)||P(h|x)) + H_{Q(h|x)} + \sum_hQ(h|x)(logP(h) + logP(x|h))
    \end{align}
    \\(H_{Q(h\mid x)}\\) is the entropy of distribution \\(Q(h\mid x)\\).</br>
    Due to the *non-negativity of the KL divergence*:
    $$ logP(x) \geq H_{Q(h\mid x)} + \sum_hQ(h|x)(logP(h) + logP(x|h)) ,$$ which becomes an equity when \\(P\\) and \\(Q\\) are identical.
    + There exists a DBN whose \\(h^1\\) marginal equals the first RBM's \\(h^1\\) marginal, as long as the dimension of \\(h^2\\) equals the dimension of \\(h^0 = x\\). By symmetry of the roles of visible and hidden units in an RBM joint distribution, the marginal distribution over the visible vector of the second RBM is equal to the marginal distribution of the hidden vector of the first RBM.
    + *Further training of an additional RBM increases a lower bound on the log-likelihood inequality.*
    + As the lower bound continues to increase, the actual log-likelihood could start decreasing. 
    + Another argument to explain why the greedy procedure works is that: *training distribution for the second RBM looks more like data generated by an RBM than the original training distribution.*
    + a good *criterion for training the first RBM is the **KL divergence between the data distribution and the distribution of the stochastic reconstruction vectors** after one step of the Gibbs chain*. This criterion yields better optimization of the DBN.
        * disadvantage: *this criterion is intractable since it involves summing over all configurations of the hidden vector \\(h\\).*
    + In the Wake phase, we consider \\(Q\\) fixed and do a stochastic gradient step towards maximizing the expected value of \\(F(x)\\) over samples \\(x\\) of the training set, with respect to parameters \\(P\\). In the Sleep phase, make \\(Q\\) as close to \\(P\\) as possible in the sense of minimizing \\(KL(Q(h\mid x)\mid\mid P(h\mid x))\\). However, instead of minimizing \\(KL\\), take \\(P\\) as the reference because \\(KL\\) is intractable.
- *Bibliography*
    + <cite>[<a href="http://www.gatsby.ucl.ac.uk/~dayan/papers/hdfn95.pdf" target="_blank">72</a>] train sigmoidal belief networks with Wake-Sleep algorithm</cite>
    + <cite>[<a href="https://www.cs.toronto.edu/~hinton/absps/fastnc.pdf" target="_blank">73</a>] wake-sleep algorithm for DBN.</cite>
    + <cite>[<a href="http://www.cs.toronto.edu/~fritz/absps/dbm.pdf" target="_blank">161</a>] transform DBN to a Boltzmann Machine by halving the RBM weights when initializing the deep Boltzmann machine from the layer-wise RBM. In positive phase, a variational approximation corresponding to a mean-field relaxation is proposed. In the negative phase, a persistent MCMC chain is proposed to use. It edges DBN on the MNIST dataset, both in terms of the data log-likelihood and in terms of classification error.</cite>
    + <cite>[<a href="http://web.eecs.umich.edu/~honglak/icml09-ConvolutionalDeepBeliefNetworks.pdf" target="_blank">111</a>] convolutional structure DBN is transformed into a deep Boltzmann machine.</cite>

**Ch9. Looking Forward**

- *Arguments*
    + Connections between the existing training methods and approaches help to deal with difficult optimization problems based on the principle of continuation methods:
        * Firstly solve an easier and smoothed version of the problem
        * Gradually consider less smoothing with the intuition that a smooth version of the problem reveals the global picture.
    + Greedy layer-wise training algorithm for DBNs is an approximate continuation method. Instead of a continuum of training criteria, a discrete sequence of presumably gradually more difficult optimization problems is dealt with. 
    + **Why unsupervised pre-training helps?**
        1. *regularization effect of the learning*: *direct the parameter to a region from which gradient descent can yield good solutions.* (empirically demonstrated)
        2. *better optimization of the lower layers of the deep architectures.*
    + The use of stochastic gradient (such as the one obtained from CD-k) and small initial weights is close to a continuation method.
    + *Controlling the magnitude of the offsets and weights in an RBM is equivalent to controlling the temperature in a Boltzmann machine (a scaling coefficient for the energy function).*
    + Unsupervised or semi-supervised learning is crucial to deep architectures in several aspects:
        1. *scarcity of labeled examples* and *availability of many unlabeled examples*
        2. unknown future task.
        3. Once a good high-level representation is learned, other learning tasks (e.g., supervised or reinforcement learning) could be much easier.
        4. *layer-wise unsupervised learning*. Much of the learning could be done using information available locally in one layer or sublayer of the architecture, thus avoiding the hypothesized problems with supervised gradients propagating through long chains with large fan-in elements.
        5. The extra constraints imposed on the optimization by requiring the model to *capture* not only the *input-to-target dependency* but also *the statistical regularities of the input distribution* might be helpful in *avoiding some poorly generalizing apparent local minima.*
- *Bibliography*
    + <cite>[<a href="http://epubs.siam.org/doi/book/10.1137/1.9780898719154" target="_blank">3</a>] approaches based on the principle of continuation methods to deal with difficult optimization problems.</cite>
    + <cite>[<a href="https://www.ri.cmu.edu/pub_files/2008/12/differentiableSparseCoding.pdf" target="_blank">6</a>, <a href="http://machinelearning.org/archive/icml2008/papers/601.pdf" target="_blank">97</a>, <a href="http://www.di.ens.fr/~fbach/nips2008_sdl.pdf" target="_blank">121</a>] start training from an unsupervised representation learning algorithm (e.g. sparse coding), fine-tuning the representation with a discriminant criterion or combining the discriminant and unsupervised criteria.</cite>
    + <cite>[<a href="http://ronan.collobert.com/pub/matos/2004_links_icml.pdf" target="_blank">36</a>, <a href="http://moodle.technion.ac.il/pluginfile.php/195968/mod_resource/content/0/OCP_ICML03.pdf" target="_blank">211</a>] mathimatical connection between early stopping and l2 regularization.</cite>
    + <cite>[<a href="http://ronan.collobert.com/pub/matos/2009_curriculum_icml.pdf" target="_blank">20</a>] training with a curriculum. showing better performance on vision and language tasks, compared to training only with the target distribution.</cite>
    + <cite>[<a href="http://www.cs.stanford.edu/people/ang//papers/icml07-selftaughtlearning.pdf" target="_blank">148</a>] scarcity of labeled examples and availability of many unlabeled examples</cite>
    + <cite>[<a href="http://www.thespermwhale.com/jaseweston/papers/deep_embed.pdf" target="_blank">202</a>] online procedure for training deep architectures that preserves an unsupervised component all along.</cite>
    + <cite>[<a href="http://www.machinelearning.org/archive/icml2008/papers/638.pdf" target="_blank">187</a>, <a href="http://dl.acm.org/citation.cfm?id=1553506" target="_blank">188</a>] improve upon Contrastive Divergence taking computation time into account.</cite>
    + <cite>[<a href="http://www.cs.utoronto.ca/~rsalakhu/papers/eval_latents.pdf" target="_blank">133</a>, <a href="http://www.cs.toronto.edu/~rsalakhu/papers/dbn_ais.pdf" target="_blank">163</a>] instead of using reconstruction error to monitor the learning progress of RBMs and DBNs, use other  tractable approximations of the partition functions. (Annealed Importance Sampling)</cite>
    + <cite>[<a href="http://www.cnbc.cmu.edu/~tai/papers/lee_mumford_josa.pdf" target="_blank">112</a>] cortex working principle</cite>

 [^1]: 