# word2vec on CORD-19
Training a word embedding model on COVID-19 Open Research Dataset (CORD-19) using word2vec.

## Overview
A simple exercise that builds and visualizes word embeddings on the CORD-19 dataset. This is a resource of now over 141,000 scholarly articles, including over 65,000 with full text, about COVID-19, SARS-CoV-2, and related coronaviruses. This dataset was first released March 13, 2020 intended to mobilize researchers to apply recent advances in NLP to generate new insights in support of the fight against COVID-19.

## About Word Embeddings
Briefly, word embedding is one of the more popular representation of a document vocabulary capable of capturing context of a word in a document facilitating numerous semantic and syntactic similarity related tasks.
Word2Vec, one of the more popular technique to learn word embeddings, was used here to generate the word embeddings on this medical corpus (other ways to train word vectors include Doc2Vec and FastText which is not covered in this example).

## Functionality
The accompanying notebook implements the following: 

- Parses each JSON document extracting the content from body_text section. Refer to [schema](https://www.kaggle.com/allen-institute-for-ai/CORD-19-research-challenge?select=json_schema.txt)
- Simple pre-processing of the body content using Gensim’s utility function (converts document into lowercase tokens and removing any accent marks) NOTE: no stemming and/or lemmatization was done.  
- Trains a Word2Vec model using Gensim’s implementation. Skip-gram architecture along with hierarchical softmax is used during training. However these parameters can be switched to use CBOW (continuous bag of words) and negative sampling for experimentation.
- Saves the trained model to a user provided dir path on disk for future use
- Loads the most recently trained model from disk (assuming multiple models have been trained)
- Perform some semantic word tasks, such as find the most similar & dissimilar token to a given token
- Visualizing the most similar & dissimilar tokens (vector representations) on a 2-D scatter plot using  PCA to reduce dimension and t-SNE for visualization
- Simple user interactivity that allows user to enter a word into a ipywidget textbook and view 10 most similar and 10 most dissimilar token in the scatter plot  

## Performance
There are variety of shallow semantic/syntactic/retrieval tasks that serve as a basis for evaluating word embedding. Some of these include: word similarity, document classification task, and document re-ranking and retrieval task .

For this exercise, the focus is word similarity. Given the medical domain of the dataset, below are some select examples of simple words across different medical concepts. The model was also evaluated on non-medical words. Word in blue is entered by user. Green highlighted words are the 10 most similar words to  entered word whereas red words are 10 most dissimilar words.

* Medical (disease)
Word: mers
![Alt Text](https://github.com/shanerai/word2vec-cord19/blob/master/images/disease%20example%20mers.jpg "mers")

*mers* is a type of *cov* (coronavirus) with *dromedary* *camels* recognized as a major reservoir host for MERS-CoV



* Medical (disease)
Word: diabetes
![Alt Text](https://github.com/shanerai/word2vec-cord19/blob/master/images/disease%20example%20diabetes.jpg "diabetes")

*hypertension* often occurs alongside *diabetes* whereas *obesity* is known to play a role in causing this disease

* Medical (protein)
Word: spike
![Alt Text](https://github.com/shanerai/word2vec-cord19/blob/master/images/protein%20example%20spike.jpg "spike")

*spike* is a large type of transmembrane protein. Whereas, association of viral capsid proteins with viral nucleic acid is called a *nucleocapsid*


* Medical (chemical)
Word: chloroquine
![Alt Text](https://github.com/shanerai/word2vec-cord19/blob/master/images/chemical%20example%20chloroquine.jpg "chloroquine")

*amodiaquine* and *chloroquine* are both used as treatment therapies of malaria. Whereas chloroquine is regarded as a classic *lysosomotropic* compound.



* Non- medical (country)
Word: colombia
![Alt Text](https://github.com/shanerai/word2vec-cord19/blob/master/images/country%20example%20colombia.jpg "colombia")
 
Other countries like *venezuela* and *mexico* are clustered around *colombia*


## Dataset
A subset of the CORD-19 dataset as of March 20, 2020 was used for this exercise.
Details:
* Document count: 9,117
* Format: JSON
* Includes: primarily COVID-19 and coronavirus-related research from PubMed's PMC open access corpus
* Excludes: bioRxiv and medRxiv

For more information on this unique dataset, refer to AI2’s [website](https://www.semanticscholar.org/cord19) for more details.
The latest and daily updated corpus can be found [here](https://www.semanticscholar.org/cord19/download)

## Known Limitations
* Only unigram tokens are included in the corpus used for model training. It would be useful to train a model on bigrams and tri-grams.
* Alphanumeric tokens are excluded in the corpus. e.g. h1n1. This might be a result of preprocessing using gensim’s utility function for this purpose.

## References
* Word2Vec: Introduction to word embedding and Word2Vec [link](https://towardsdatascience.com/introduction-to-word-embedding-and-word2vec-652d0c2060fa)
* Gensim Word2Vec: module documentation [link](https://radimrehurek.com/gensim/models/word2vec.html)
* Parsing CORD-19 JSON files [source](https://www.kaggle.com/xhlulu/cord-19-eda-parse-json-and-generate-clean-csv)
