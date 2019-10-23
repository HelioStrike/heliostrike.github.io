---
layout: post
title:  "ML Notes - The same output issue"
date:   2019-10-23 11:00:00 +0530
categories: machine learning
---

I've been encountering this issue a lot lately, where I get the same output from a DNN/ANN whatever input I pass. I encountered this issue again today and spent around 2-3 hours today trying to figure out what was going wrong. I fixed my issue now and here I am writing this post for my future self.

Here's what worked:

- **Reduce the learning rate** - Sometimes if the learning rate is too high, the loss may jump far and into an irrecoverable trench. 

- **Reduce the batch size** - Huge batch size coupled with high learning rate will propel the loss into what fits all of them.

- **Reduce the depth or number of parameters in your model** - This was what worked for me today. Usually the parameters in an initial model are pretty small (in the order to 1e-1 to 1e-3). If the inputs are small too, as they get passed via feed-forward propagation, they keep getting smaller and become less significant to the final output. Reducing the model's depth reduces the number of times that the inputs get diminished, and fixes the issue.

