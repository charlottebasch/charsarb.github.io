---
layout: post
title:      "Trying to Make a Neural Network for NLP"
date:       2020-10-30 23:48:57 -0400
permalink:  trying_to_make_a_neural_network_stable
---


Neural networks are unpredictable and their complexity sometimes impedes one’s ability to identify what is causing problems with them. The goal of my project was to build a model to classify tweets about Apple and Google products as positive or negative. I used a Long Short Term Memory network to accomplish this task. As I began to try and tune this model, add additional parameters and layers, and compare different results, it became clearly that the fluctuations would be an impediment to refining a model. 

This data initially had four types of tweets: positive, negative, neutral, and unknown. I narrowed this down to just the positive and negative classes as it would be easier to build my neural network this way. This narrowed the datset to approximately 3,500 tweets. In addition, the remaining tweets were severely imbalanced; almost 85% of the tweets were rated as positive. Initially I tried to use sklearn’s compute_class_weight when modeling but it became clear quite quickly that the neural network was merely predicting the majority class for all observations regardless of the balanced weights. In the end I decided to undersample the majority class in my training set. This meant going from having over 2,000 positive tweets in my training set to around 400. This brought the total amount of tweets in my training set to a little over 800. While this did raise concerns, having a neural network that only predicts the majority class is of little use. In the future I would want to have much more data when building a network like this. 

However preceding the data imbalance problem was data cleaning. I initially planned to use a pretrained GloVe vector because it had been trained on 2 billion tweets. However it did not contain some of the product words relevant to my specific problem. Therefore I decided to create my own embedding layer using word2vec. I used the tweet-preprocessor to get rid of irrelevant words related to tweets. This included removing emojis, the abbreviation ‘rt’that indicates retwteeting, urls, and mentions. In addition I used gensim’s decode_htmlentities to replace the html character entity references (e.g. &quot; for “). I then proceeded to create the word2vec model. In order to check how well the model learned, I looked at the words it deemed similar to ‘iphone’. It gave the following result:

> [('android', 0.9464272856712341),
>  ('got', 0.9347250461578369),
>  ('thanks', 0.9280915856361389),
>  ('download', 0.9060229063034058),
>  ('our', 0.8940656185150146),
>  ('app', 0.8835204243659973),
>  ('check', 0.8732641339302063),
>  ('free', 0.8621795773506165),
>  ('awesome', 0.8597784638404846),
>  ('market', 0.8520791530609131)]

While some of the words did not relate as well to the iphone, most captured something about what the iphone was (i.e. similarity to android), what it is used for (i.e. download), or what is a part of it (i.e. app). Therefore I proceeded to modeling. 

After doing the train-test-validation split, it was time to use keras’s tokenizer to prepare the data for the neural network. I first fit the training data then transformed the X training, testing, and validation sets into sequences. Since the sequences must all be the same length, padding was added to all of the shorter than maximum sequences. After setting up early stopping, I was ready to move on to modeling. This is where my issues began. 

I initially thought that by setting a tensorflow random seed and numpy random seed at the top of my Jupyter notebook and random seeds in my train-test splits, I would be able to see stable results. However this did not come to pass. 

My first attempt to solve this problem was provided by a stackoverflow post. The first thing this commenter suggested was to set the PYTHONHASHSEED to a fixed value to eliminate randomness from the environment. In addition, a second, graph-level tensorflow random seed was set. This resulted in the following code at the top of my notebook:

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

I experimented with multiple random seed values but I was still having problems with my networks. I proceeded to try setting the shuffle parameter in my layers to false. Once again this attempt failed and model performance was consistently worse. Removing the batch size argument from the network compiling and using all samples did seem to improve performance. However this did not address stability. 

Lastly I attempted to initialize the kernel and bias in the layers. While I did not have the time to try all of the various combinations, the kernel initializers and bias initializers again proved fruitless. In the end I decided to save the model with the best performance to be loaded in as described here. My data had other issues, including the size and perhaps some of the cleaning choices so in the future I would try different cleaning methods and bigger datasets. While none of these methods for getting consistent results worked for me, they may make an impact in other situations. In the future I would also look deeper into the kernel and bias initializers.



