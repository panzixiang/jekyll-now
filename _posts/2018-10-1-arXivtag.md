---
layout: post
title: Building the arXiv classifier
---

# Project: arXivtag

The following few posts are a short documentation of a pet project I did since graduating from college. I named it "arXivtag" because it is essentially a Latent Dirichlet Allocation (LDA) based article classifier. The goal is to classify (return the subject) when given an abstract of a new arXiv submission.

The motivation for the project stems largely from a slight frustration because of the thousands of articles in [arXiv](https://arxiv.org/), many span across disciplines and they almost always have abstracts/content that is hard to understand on first parse. Thus a natural problem when searching the arXiv is when one doesn't know that similar article might be classified in a completely different branch in the website. This can be extended to cross-check articles for misclassification (if the algorithm performs better than an average human scientist) and also a built-in recommendation system.

The arXiv dataset is also large, structured, and well documented (more on that later) and provides us with just enough data to be manageable (in terms of training time) on a single computer and meaningful enough to be bigger than a toy problem.

I chose LDA because it is a popular algorithm for topic modeling with excellent implementations in python and is well documented/widely used (more on that later). 

I'm planning to divide this into a few logical parts:
1. Getting, cleaning, wrangling with data (takes way more time than you think)
2. The real NLP work, more on the LDA model
3. Some cool visualizations
4. Building and testing various ML models 
5. Possible future work


## Part I: Getting the dataset
### The arXiv dataset
The [arXiv](http://arxiv.org/) is a online repository of preprints of scientific papers in the fields of astronomy, physics, mathematics, computer science, quantitative biology, quantitative finance and statistics. To date it has more than a million papers and more are being added every day. This dataset I focused on is a relatively recent (2007-17) sample totaling approximately 800,000 pieces of metadata which I curated via a data dump using the arXiv APIs. They contain a significant number of papers from every category (>5000) submitted in the past decade. 


The parts of interest of this paper is the abstract and the category tag(s) of the papers. The goal here is to classify a new abstract correctly into one of the categories.
