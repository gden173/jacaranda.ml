---
title: "Frazer Gehrig - Web Scraping AFL Data using Python"
date: 2022-09-22T18:45:06+10:00
draft: true
tags: ["preview", "math", "python"]
categories: ["math", "python", "packages"]
markup: mmark
---

# Frazer Gehrig - Web Scraping AFL Data using Python



<div style="text-align: center;">
<img src="/frazer_gehrig.png" alt="Frazer Gehrig" width="700"/>
</div>

## Installation 

Currently, there are various ways this package can be installed. 
These include 

- GitHub 
- pip

### GitHub 

To install from GitHub there are two options, 
the first option is to clone the repository and do a local installation from the cloned directory. 

{{< gist gden173 fe166f3d76b16cd18bdc4af5cd4ad52c "01_clone.sh" >}}

The second option is to install from GitHub without first cloning the repository, 
to install the latest master branch, run the command. 

{{< gist gden173 fe166f3d76b16cd18bdc4af5cd4ad52c "02_pip_install_git.sh" >}}

### Pip 

To install through pip, simply run 

{{< gist gden173 fe166f3d76b16cd18bdc4af5cd4ad52c "03_pip_install.sh" >}}

## Kaggle 

A kaggle dataset of the entire set of scraped table data, using this package, is available [here](https://www.kaggle.com/datasets/gabrieldennis/afl-player-and-game-data-and-statistics18972022). 
The script which was used to scrape the set of tables and package up the dataset for kaggle is located [here](examples/kaggle_data.py). 

