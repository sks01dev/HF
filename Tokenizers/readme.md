
# Training a New Tokenizer from an Old One

## 📌 Goal

Train a **new tokenizer specialized for code** using an **existing tokenizer (GPT-2)** and a **code dataset**.

---

## 🧠 Core Idea

```
Existing Tokenizer (GPT-2)
        ↓
Code Dataset (CodeSearchNet - Python)
        ↓
Train new tokenizer with code vocabulary
        ↓
Better tokenization for programming code
```

---

## 📦 Setup

Install required libraries:

```
datasets
evaluate
transformers[sentencepiece]
git-lfs
```

Login to Hugging Face:

```
from huggingface_hub import notebook_login
notebook_login()
```

---

## 📚 Dataset

Dataset used:

```
CodeSearchNet (Python)
```

Load dataset:

```
load_dataset("code_search_net", "python")
```

Important field:

```
whole_func_string
```

Contains the **actual Python functions** used for tokenizer training.

---

## 🔄 Preparing Training Data

Instead of loading everything into memory:

```
Use a generator
Yield data in chunks (1000 samples)
```

Purpose:

* Memory efficient
* Works for large datasets

---

## 🤖 Load Base Tokenizer

Base tokenizer:

```
GPT-2 tokenizer
```

```
AutoTokenizer.from_pretrained("gpt2")
```

This tokenizer is used as the **starting point**.

---

## 🏋️ Training the New Tokenizer

Train tokenizer from dataset iterator:

```
tokenizer = old_tokenizer.train_new_from_iterator(
    training_corpus,
    vocab_size=52000
)
```

Result:

* Vocabulary adapted for **Python code**
* Better token segmentation

---

## 🔍 Testing Tokenization

Example code snippet:

```
def add_numbers(a, b):
    return a + b
```

Compare:

```
old_tokenizer.tokenize()
vs
new_tokenizer.tokenize()
```

Purpose:

* Check token efficiency
* Verify improvements

---

## 💾 Save Tokenizer

Save locally:

```
tokenizer.save_pretrained("code-search-net-tokenizer")
```

---

## ☁️ Upload to Hugging Face Hub

Push tokenizer to the hub:

```
tokenizer.push_to_hub("code-search-net-tokenizer")
```

Then load it anytime:

```
AutoTokenizer.from_pretrained("username/code-search-net-tokenizer")
```

---

## 📊 Pipeline Overview

```
Install libraries
      ↓
Login to Hugging Face
      ↓
Load CodeSearchNet dataset
      ↓
Create training generator
      ↓
Load GPT-2 tokenizer
      ↓
Train new tokenizer on code
      ↓
Test tokenization
      ↓
Save & push tokenizer to Hub
```

---

If you want, I can also make a **GitHub-ready README with badges, sections, and visuals** that looks much more professional.

