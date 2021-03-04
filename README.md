# Sentence Bert for Question-Answering on COVID-19 Open Research Dataset (CORD-19) 

Here I developed a document retrieval system to return the titles and the relevant passages of scientific papers containing the answer to a given user question. 

For example, for the question *“What are the coronaviruses?”*, your system can return the paper title *“Distinct Roles for Sialoside and Protein Receptors in Coronavirus Infection”*, since this paper contains the answer to the asked question.

To achieve the goal of this exercise, I needed first to read the paper [Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks](https://arxiv.org/pdf/1908.10084.pdf), in order to understand how I can create sentence embeddings.

## In these notebooks you will find:
1.  Preprocess the provided dataset.
2.  The implementation of 2 different sentence embedding approaches, in order for my model to retrieve the titles and the relevant passages of the papers related to a given question. 
3.  Comparison of 2 models based on 4 different criteria of my choice.

## 1st Model of sentence embeddings
My first attempt was to take the SBERT model ***nli-roberta-base*** of the library Sentence Tranformers. Then, I searched for the answer only in abstract and body texts of each paper. Finally, I ask the model for answers using semantic search, which performs a cosine similarity search between a list of query embeddings and a list of corpus embeddings.

Unfortunately, the results isn't so satisfactory and it turns out that the Brute Force Method, to compare the queries with each sentence of papers, isn't such a good strategy. There is more explanations in the notebook.

***Note***: I used the first version of the [COVID-19 Open Research Dataset (CORD-19)](https://ai2-semanticscholar-cord-19.s3-us-west-2.amazonaws.com/historical_releases.html) in my work (articles in the folder ***comm_use_subset***). This includes 9000 articles.


## 2nd Model of sentence embeddings
