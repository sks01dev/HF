

# Train a New Tokenizer from an Old One

## Goal

Train a **code-aware tokenizer** by adapting the **GPT-2 tokenizer** using the **CodeSearchNet (Python) dataset**.

---

## Key Idea

Use the GPT-2 tokenizer as a base and **learn a new vocabulary from code data** using the `train_new_from_iterator()` method.

---

## Process

**1. Load dataset**
Use the CodeSearchNet Python dataset and extract the function text (`whole_func_string`).

**2. Create training iterator**
Build a generator that streams function code instead of loading the whole dataset into memory.

**3. Load base tokenizer**
Start from the pretrained **GPT-2 tokenizer**.

**4. Train new tokenizer**
Train a new vocabulary from the dataset using
`train_new_from_iterator()`.

**5. Save / upload tokenizer**
Store the tokenizer locally or push it to the Hugging Face Hub.

---

## Workflow

```
CodeSearchNet dataset
        ↓
Extract Python functions
        ↓
Training iterator
        ↓
GPT-2 tokenizer
        ↓
train_new_from_iterator()
        ↓
New code tokenizer
```

