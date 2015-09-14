---
layout : post
category : LearningNote
tags : [DBN, Basis]
---
{% include JB/setup %}

The first time when I read the hinton tutorial slides was quite a bit while ago, namely in spring 2011 when I was doing my master probject. By then, I was quite new to this area and could not understand all of the pages. What I did was to follow the technique tricks and matlab code provided with the Science paper, to write my own DBN-based auto-encoder.

Recently, while starting to write my final PhD thesis, I reviewed these basic papers/tutorial slides and tried to derive all the mathematics again to verify if I understand them. After reading this slide again, there are a few points I would like to write down as a reminder, or memorial for further use.

- Training Tricks:
	+ Instead of following the gradient of log-likelihood of the energy model, DBN uses CD-1 method to follow the gradient of another objective function.
    + The Contrastive Divergence doesn't maximize the likelihood of the data under the model, but maximize the difference of two KL-divergences: \\(KL(q\mid p) - KL(p_k\mid p)\\).
    + page 23: The N dimension of the hidden layer (MxN) means that the RBM would grab N features for the input M data samples.
    + One can scale the input data to interval \\( [0,1] \\) and modeled by the probability of the visible variables to be one.
    + page 24: if we feed the network with only one type of images/signals, then the network only learns how to generate this specific type of input. anything else would be badly reconstructed.
    + page 94: why do we whiten data? Images have strong pair-wise correlations. Learning higher oder statistics is difficult when there are strong pair-wise correlations. So we remove the 2-nd statistics before trying to learn the higher-oder statistics.