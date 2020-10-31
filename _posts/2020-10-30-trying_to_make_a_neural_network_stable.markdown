---
layout: post
title:      "Trying to Make a Neural Network Stable"
date:       2020-10-31 03:48:56 +0000
permalink:  trying_to_make_a_neural_network_stable
---


Neural networks are unpredictable and their complexity sometimes impedes one’s ability to identify what is causing problems with them. The goal of my project was to build a model to classify tweets about Apple and Google products as positive or negative. I used a Long Short Term Memory network to accomplish this task. As I began to try and tune this model, add additional parameters and layers, and compare different results, it became clearly that the fluctuations would be an impediment to refining a model. I initially thought that by setting a tensorflow random seed and numpy random seed at the top of my Jupyter notebook and random seeds in my train-test splits, I would be able to see stable results. 
My first attempt to solve this problem was provided by a stackoverflow [post](https://stackoverflow.com/questions/50659482/why-cant-i-get-reproducible-results-in-keras-even-though-i-set-the-random-seeds/) . The first thing this commenter suggested was to set the PYTHONHASHSEED to a fixed value to eliminate randomness from the environment. In addition, a second, graph-level tensorflow random seed was set. This resulted in the following code at the top of my notebook:

> #set random seeds
> seed_value = 42
> import os
> os.environ['PYTHONHASHSEED']=str(seed_value)
> 
> import numpy as np
> import tensorflow as tf
> np.random.seed(seed_value)
> tf.random.set_random_seed(seed_value)
> tf.compat.v1.set_random_seed(seed_value)  

I experimented with multiple random seed values but I was still having problems with my networks. I proceeded to try setting the shuffle parameter in my layers to false. Once again this attempt failed and model performance was consistently worse. 

