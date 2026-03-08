# Semantic Search with Transformers and FAISS

## What this project does

This project builds a simple **semantic search engine**.

Instead of matching exact keywords, semantic search tries to understand the **meaning of a query** and finds the most relevant documents based on that meaning.

The system searches through GitHub issue comments from the Hugging Face Datasets repository and returns the most relevant answers to a user’s question.

---

## First Principles

Traditional search works like this:

* A query is broken into keywords
* Documents containing those keywords are returned

This approach fails when the **same idea is expressed using different words**.

Semantic search solves this by representing text as **vectors (embeddings)**.
Texts with similar meaning produce **similar vectors**.

The system then finds the **nearest vectors** to a query vector.

Query → Embedding → Vector similarity → Relevant documents

---

## How the system works

1. **Load Dataset**

A dataset of GitHub issues is loaded using the Hugging Face `datasets` library.

2. **Clean the Data**

* Pull requests are removed
* Issues without comments are removed
* Very short comments are filtered out

3. **Prepare Text**

For each entry we combine:

* issue title
* issue body
* comment

This gives the model more context.

4. **Generate Embeddings**

We use the transformer model:

`sentence-transformers/multi-qa-mpnet-base-dot-v1`

The model converts text into **768-dimensional embeddings**.

5. **Build FAISS Index**

FAISS is used to store embeddings and perform **fast similarity search**.

6. **Search**

A user query is converted into an embedding and the FAISS index returns the **most similar comments**.

---

## Technologies

* Python
* Hugging Face Transformers
* Hugging Face Datasets
* PyTorch
* FAISS

---

## Example Query

Example question:

How can I load a dataset offline?

The system returns the most relevant GitHub comments that answer the question.

---

## Notebook

The full implementation is available in the Colab notebook:

`semantic_search_faiss.ipynb`

---

## Learning Goal

This project demonstrates the core idea behind modern retrieval systems used in:

* AI assistants
* documentation search
* question answering systems
* retrieval-augmented generation (RAG)

---

## Author

Created while studying the Hugging Face LLM Course.
