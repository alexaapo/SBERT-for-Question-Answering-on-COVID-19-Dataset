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

Unfortunately, the results isn't so satisfactory and it turns out that the Brute Force Method, to compare the queries with each sentence of papers, isn't such a good strategy. There are more explanations in the notebook.

***Note***: I used the initial version of the [COVID-19 Open Research Dataset (CORD-19)](https://ai2-semanticscholar-cord-19.s3-us-west-2.amazonaws.com/historical_releases.html) in my work (articles in the folder ***comm_use_subset***). This includes 9000 articles.


## 2nd Model of sentence embeddings
This time I selected to tokenize only the abstract of each paper, since I wanted to search for the answer firstly with criterion these parts and not in the title and the body texts. I wanted to save more time and memory. Then, I select a model provided by gsarti for ranking purposes [covidbert-nli](https://huggingface.co/gsarti/covidbert-nli), a fine-tuned version of Deepset's CovidBERT.

This model is trained on SNLI and MultiNLI using the sentence-transformers library to produce universal sentence embeddings. Embeddings are subsequently used to perform semantic search on CORD-19.

In this notebook I follow this strategy:

* I rank the abstract of each article.
* I rank the paragraphs (body texts) of the best (most similar) abstracts.
* Comprehened the top paragraphs of the retrieved documents using ***HuggingFace*** question-answering pipeline.

For comprehension I used the [CovidBERT](https://huggingface.co/deepset/covid_bert_base) model on [SQuAD](https://rajpurkar.github.io/SQuAD-explorer/) question answering data [covid_squad](https://huggingface.co/graviraja/covid_squad), a fine-tuned version of Deepset's CovidBERT on SQuAD dataset.


I start by looking for the top 20 most similar articles to a given question (based only in abstracts). Though I retrived the top related articles, each paper contains a lot of body text content. Finding the relevant paragraphs in the article will help in narrow down the amount of data needs to comprehended for finding the answer to the given query. After I have in my hands the top 20 articles, I started to encode the body texts of each articles. So we understant that there is a big different with the previous notebook, as here I encode the body texts of only 20 articles, while in the other notebook I encode the body texts of 9000 articles!

I already have top 20 articles and in each document top 20 most relevant body texts. Comprehension will help even more finetuned details up to a sentence level. So, in the end, I used my comprehension model to find the appropriate answer with the biggest score.

In general, I have to admit that I was more satisfied with my second model. The answers that it gives are more relevant and right (in most cases) than the first pretrained model. There are more explanations in the notebook. 

***Note***: I used the second version of the [COVID-19 Open Research Dataset (CORD-19)](https://ai2-semanticscholar-cord-19.s3-us-west-2.amazonaws.com/historical_releases.html) in my work (articles in the folder ***comm_use_subset***). This includes 9118 articles.
