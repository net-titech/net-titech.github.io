---
layout: post
title: CREST-Deep Independent Meeting - Yokota Lab \& Murata Lab
excerpt: "2017-05-26"
categories: [Meeting]
comments: true
pinned: false
icon: fa-clock-o
---

# 2017-05-26 / Low Rank Approximation in Deep Neural Network

## <i class="fa fa-file-text"></i> Meeting Summarization

The main purpose of this meeting is to have a broader view on the Deep Neural
Network compression problem. In Murata lab, our most promising direction results
in 30 times compression ratio without accuracy loss while preserving the ability
to load the compressed model using conventional software (or hardware). Our
compression scheme aim to deploy compressed models on mobile phones and
commercial embedded systems. In Yokota lab, the main topic is low-rank
approximation and they are applying this technique to speed up and compress
Deep Neural Networks. Both labs have shared their work and discussed the
possibility for collaboration.

**Murata Lab**: We shared our current work flow for DNN pruning, quantization,
and encoded model storing. We discussed some possibility to use low-rank
approximation in our scheme. There are three main points: 1. The effect of
sparsity on low-rank approximation, 2. The sensitivity of low-rank approximation
on the accuracy of a DNN, 3. A research direction on the encoding scheme.

**Yokota Lab**: They shared their research on performance impact of low-rank
approximation and insight about our 3 main points above.

## <i class="fa fa-flask"></i> Conclusion

We think that this meeting is a good start for future collaboration among labs
in the project. We have agreed to:

- Communication and collaboration on [Slack](crest-deep.slack.com) \#low-rank
- We will share our GitHub repositories and tools
- Monthly two groups meetings and join each others' meetings.

## <i class="fa fa-bullseye"></i> Next Week Objectives

Now we have some basic understanding of low-rank decomposition, we continue to
think about our tasks:

- **Choong**: Investigate methods for lossy neural network compression.
- **Kaushalya**: Investigate methods for effective pruning.
- **Arie**: Study and design experiments to quantify weights sensitivity.
- **Hoang**: Software Inference Engine.
