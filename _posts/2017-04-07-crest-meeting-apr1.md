---
layout: post
title: CREST-Deep Weekly Meeting
excerpt: "2017-04-07"
categories: [Meeting]
comments: true
pinned: false
icon: fa-clock-o
---

# 2017-04-07 / CREST-Deep Weekly Meeting

## <i class="fa fa-file-text"></i> Literature Update

This week we focus on the plan for April. As planned, our goal for April
is to be able to confirm existing methods' effectiveness and re-create their
results. For literature update, we have several observations as follow:

- Network distillation showed that a fully connected neural network doesn't necessary
to be deep. A shallow network can do as good as a deep network.
- Distilling a convolutional layer is another problem. A network doesn't need to be deep in the fully connected layers, but its convolutional layers _need_ to be deep.
- We can investigate methods for convolutional layers distillation.
- Using auto-encoder to learn the latent representation of each convolutional layers. This approach is inspirational to WSBM.

## <i class="fa fa-flask"></i> Research Update

There is no new result for this week.

## <i class="fa fa-bullseye"></i> Next Week Objectives

Next week we will update our experimental result on distilling AlexNet and compressing the trained
network as JPEG.
