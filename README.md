# Language Token Analysis & Prompt Compression — README 📚✨

## TL;DR
### Part 1
English is king when it comes to prompting LLMs, other languages tend to use more tokens (even if they have fewer words/character). This is because most popular tokenizers are trained primarily on majority-English data, but it would be interesting to test with tokenizers that are specifically suited to those languages.
### Part 2
You can strip out a lot of fluff from English (articles and punctuation) and use about 20% fewer tokens, with an average information loss in the prompts of about 5% (which may or may not be tolerable for you). Seems to be consistent with variable-sized texts.

Note: In order to use the code as-is, you must define `GOOGLE_APPLICATION_CREDENTIALS` (for the Translate API) and `HF_TOKEN` (for the Huggingface API) env variables.

## Overview 🌍
This project explores how different languages are tokenized by modern LLM tokenizers and investigates whether English prompts can be compressed without significantly altering their semantic meaning. The notebook includes:

- Cross-language translation tests
- Tokenization comparisons across models (OpenAI, DeepSeek, Hugging Face)
- Embedding-based semantic similarity measurements
- Preliminary analysis of “prompt compression” — reducing token count while preserving meaning

**Goal:** Understand which techniques can be used to meaningfully reduce token usage and costs. The two techniques that are explored are 1) Using foreign languages, and 2) Removing extraneous articles and punctuation from English prompts.

---

## Features ⭐

### 1. Language Token Usage Comparison
- Translates English sentences into other languages using the Google Translate API  
- Tokenizes both versions with multiple tokenizers  
- Calculates:
  - Token counts
  - Token usage ratios
  - Patterns that show which languages compress or expand relative to English  

### 2. Prompt Compression Experiment
- Removes low-information English elements
- Computes token savings
- Uses embedding cosine similarity to estimate semantic loss  
- Produces:
  - Average information loss (~3–5%)
  - Average token savings (~20–25%)

### 3. Visualization Tools
The notebook generates helpful plots, including:  
- Token count bar charts
- Token ratio summaries  
- Embedding-loss visualizations  

These help illustrate how different languages and compression strategies behave.

---

## Project Motivation 💡
Most widely-used tokenizers (OpenAI, DeepSeek, Hugging Face’s GPT-style tokenizers) are optimized for English. This project investigates:

- How that affects multilingual token efficiency  
- Whether English, despite containing function words, actually tokenizes more efficiently  
- Whether prompt compression can reduce model usage costs in production workloads  

---

## Notebook Structure 🗂️

### 1. Setup & Dependencies
- Installs `tiktoken`, Hugging Face Transformers, Google Translate API, and plotting tools  

### 2. Translation Utilities
- Functions for automatic sentence translation into multiple languages  

### 3. Tokenization Functions
- Counts tokens for each language  
- Supports multiple tokenizer backends  

### 4. Embedding Similarity Analysis
- Encodes original and compressed sentences  
- Computes cosine distances  
- Aggregates estimated information loss  

### 5. Visualization & Summary Metrics

---

## Results (Summary) 📊
- English often tokenizes more efficiently than many other languages because common English patterns map to single tokens  
- Removing articles/punctuation reduces English sentence length without meaningfully affecting semantic structure (depending on your threshold)
- Token savings of ~20% appear feasible with minimal semantic degradation (information loss of ~3-5%)

This motivates further exploration of automated prompt compression.

---

## Future Work 🚀
- Fine-tune a model to automatically compress prompts while minimizing embedding-loss  
- Explore multilingual tokenizers (e.g., Jieba for Chinese)
- Experiment with algorithmic compression techniques such as PCA on sentence embeddings  
- Build a production-ready "prompt optimizer" API (if I feel like it)

---

## How to Use
1. Open the notebook in Google Colab  
2. Insert your Google Cloud Translate API key  
3. Run the cells in order  
4. Adjust the input sentences and target languages as needed  
5. Use the visualizations and printed metrics to evaluate compression strategies  

---

## Requirements
- Python 3.12.12  
- Google Colab  

**Packages:**
- `tiktoken`  
- `transformers`  
- `google-cloud-translate`  
- `matplotlib`  
- `sentence-transformers`  
- `numpy`  
- `tqdm`  
