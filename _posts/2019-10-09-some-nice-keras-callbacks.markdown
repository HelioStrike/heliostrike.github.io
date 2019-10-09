---
layout: post
title:  "Some Nice Keras Callbacks"
date:   2019-10-09 4:00:00 +0530
categories: machine learning
---
I started looking at kaggle again recently, after a few months' break. I noticed a few keras kernels using these neat ideas which were inbuilt as keras callbacks. I know this post is a bit oddly timed, considering they've been around for a while, but I'm pretty sure I'll forget about these soon, so here it goes.

## Early Stopping

When a model is repeatedly trained on some training data, sometimes it tends to fit to the statistical impurities in the training data. It tends to show a higher accuracy on the training data, but may not do as well on validation and test data. In such a case, it may be better stop training early, before the model starts badly overfitting. That is exactly what early stopping does.

#### Example

{% highlight python %}
keras.callbacks.callbacks.EarlyStopping(monitor='val_loss', min_delta=0.0001, patience=5, verbose=1, mode='min')
{% endhighlight %}

**monitor** - Its the parameter that will act as the criteria for stopping.

**min_delta** - If the difference between the criteria is greater than this value, the model is said to have gotten worse.

**patience** - It is the number of epochs for which the criteria value is monitored.

**mode** - Indicates whether the criteria value going up means a better model. Here, loss is to be minimized, so the mode is 'min'. For accuracy, mode would be 'max'.

## Reduce LR on Plateau

If the model's loss hits a plateau or stagnates, then lowering the learning rate may help the loss explore trenches in the loss space.

#### Example
{% highlight python %}
keras.callbacks.callbacks.ReduceLROnPlateau(monitor='val_loss', factor=0.2, patience=2, verbose=1, mode='min', min_delta=0.0001)
{% endhighlight %}

**monitor** - Its the parameter that will act as the criteria.

**factor** - The learning rate is multiplied by this factor.

**min_delta** - If the difference between the criteria is greater than this value, the model is said to not have hit a plateau.

**patience** - It is the number of epochs for which the criteria value is monitored.

**mode** - Indicates whether the criteria value going up means a better model. Here, loss is to be minimized, so the mode is 'min'. For accuracy, mode would be 'max'.

### References

<https://machinelearningmastery.com/early-stopping-to-avoid-overtraining-neural-network-models/>

<https://machinelearningmastery.com/how-to-stop-training-deep-neural-networks-at-the-right-time-using-early-stopping/>

<https://keras.io/callbacks/>