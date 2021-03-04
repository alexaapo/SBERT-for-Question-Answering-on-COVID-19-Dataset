# Sentence Bert for Question-Answering on COVID-19 Open Research Dataset (CORD-19) 

Here I developed a document retrieval system to return the titles and the documents of scientific papers containing the answer to a given user question. 

For example, for the question *“What are the coronaviruses?”*, your system can return the paper title *“Distinct Roles for Sialoside and Protein Receptors in Coronavirus Infection”*, since this paper contains the answer to the asked question.

To achieve the goal of this exercise, I needed first to read the paper [Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks](https://arxiv.org/pdf/1908.10084.pdf), in order to understand how I can create sentence embeddings.

In the notebooks you will find:
1.  Preprocess the provided dataset.
2.  I implement 2 different sentence embedding approaches, in order for your model to retrieve the titles and the specific documents of the papers related to a given question. 
3.  Compare your 2 models based on at least 2 different criteria of your choice.  Explainwhy you selected these criteria, your implementation choices, and the results.  Somequestions you can pose are included here. You will need to provide the extra questionsyou posed to your model and the results of all the questions as well.

***Note***: I used the first version of the [COVID-19 Open Research Dataset (CORD-19)](https://ai2-semanticscholar-cord-19.s3-us-west-2.amazonaws.com/historical_releases.html) in my work (articles in the folder ***comm_use_subset***).
