---
title: "Jacaranda - PyTorch Hyper Tuning with Optuna"
date: 2022-09-22T18:45:06+10:00
draft: true
categories: ["python", "packages", "pytorch", "kaggle"]
tags:  ["python", "packages", "pytorch", "kaggle"]
markup: mmark
---

# Jacaranda - PyTorch Hyper Tuning with Optuna

<div style="text-align: center;">
<img src="/pytorch_optuna.png" alt="pytorch + optuna" width="700"/>
</div>

How many times have you looked through old repositories to find boiler-code for how you built your last MLP, CNN, VAE, etc. In this article, we showcase a Python package that leverages Optuna to build and tune PyTorch models.

Optuna is *"A hyperparameter optimization framework"* that can be used in a range of optimisation settings. It is particularity popular in machine learning as it offers an easy way to tune hyper parameters. If you frequent Kaggle, then chances are you have heard of Optuna before.

We combined Optuna with  PyTorch (and XGBoost)  to produce a framework to build standard PyTorch (and XGBoost) models. The over-arching idea is that each time we are required to use a new PyTorch mode, it can be generalised and included into this package. So that we save time when wanting to reuse the same type of model. That is where *jacaranda* comes in.

The repository can be found on [GitHub](https://github.com/jacaranda-analytics/jacaranda) under this website organizational [page](https://github.com/jacaranda-analytics).  Furthermore, our repository can be directly installed from  [PyPI](https://pypi.org/project/jacaranda/). 

## Overview

Jacaranda is a wrapper package around several Data Science and Machine Learning
librarys,  such as 

- [PyTorch](https://pytorch.org)
- [XGboost](https://xgboost.readthedocs.io/en/stable/)

which creates an easy interface to interact, and automatically tune models produced 
by these libraries. 

## Installation 

Currently, there are various ways this package can be installed. 
These include 

- GitHub 
- pip

### GitHub 

To install from GitHub there are two options, 
the first option is to clone the repository and do a local installation from the cloned directory. 

```sh
git clone git@github.com:jacaranda-analytics/jacaranda.git
cd jacaranda/ && pip install . 
```

The second option is to install from GitHub without first cloning the repository, 
to install the latest master branch, run the command. 

```sh
pip install https://github.com/jacaranda-analytics/jacaranda/archive/master.zip
```

### Pip 

To install through pip, simply run 

```python 
pip install jacaranda
```

## Examples 

Included below is a number of examples of pre-defined models that are ready to be tuned to your data.  For all the examples, we generate some sample data using numpy.  

Let's first build and train a multi layer perecptron (MLP). In order to do this we first need to define a loss function, metric function (a derivative of the loss function) and Jacaranda configuration file. These are all used to build and train an MLP.

<script 
src="https://emgithub.com/embed-v2.js?target=https%3A%2F%2Fgithub.com%2Fjacaranda-analytics%2Fjacaranda%2Fblob%2Fmain%2Fexamples%2Fjacaranda-mlp.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showFileMeta=on&showFullPath=on&showCopy=on&fetchFromJsDelivr=on">
</script>

As you can see, we used the MSE loss function and considered two tuning trials. If I wanted to instead build a CNN model on the same data (given the data is 1-dimensional, this would be a 1d-CNN) I could instead do the following (repeating code for completeness).

<script src="https://emgithub.com/embed-v2.js?target=https%3A%2F%2Fgithub.com%2Fjacaranda-analytics%2Fjacaranda%2Fblob%2Fmain%2Fexamples%2Fjacaranda-cnn1d.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showFileMeta=on&showFullPath=on&showCopy=on&fetchFromJsDelivr=on"></script>

Here we can see that the code to generate this is very similar, the only major difference is that we change the input *define_model* in the function *pytorch_general*. 

Similarly, we can also tune an XGBoost Regression Tree using *jacaranda* also. 

<script src="https://emgithub.com/embed-v2.js?target=https%3A%2F%2Fgithub.com%2Fjacaranda-analytics%2Fjacaranda%2Fblob%2Fmain%2Fexamples%2Fjacaranda-xgboost.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showFileMeta=on&showFullPath=on&showCopy=on&fetchFromJsDelivr=on"></script>

At present the package can also tune an autoencoder and a variational autoencoder in Pytorch as well. Examples for each of these (and the ones included above) can be on [GitHub](https://github.com/jacaranda-analytics/jacaranda/tree/main/examples).
