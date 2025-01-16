# Training on large language models for genomics

# Overview

In this repo, we will follow a training for large language models (LLMs) for genomics. The training comprises a short lecture and several lab classes. 

# Lecture notes

See file: 

# Lab classes


## Data to pretrain the model

Data:
- **data/genome_sequences/hg38/sequences_hg38_200b_small.csv.gz** (10% of the human genome)
- **data/genome_sequences/hg38/sequences_hg38_200b_verysmall.csv.gz** (1% of the human genome)

## Pretraining of an LLM on DNA sequences

Here, we will pretrain an LLM from scratch (a simplified mistral model) on fixed size DNA sequences from the human genome. 
The LLM is pretrained with causal language modeling using 200b DNA sequences from the human genome hg38 assembly.

[Script on Google Colab](https://colab.research.google.com/drive/1gcw_MYiqwB-pbVYHIx8kevx-ZD7sqMxL#scrollTo=JTYKjBrwRSU6)

## Finetuning of an LLM for DNA sequence classification

Here, we will use a pretrained LLM "Mixtral-8x7B-v0.1" and finetuned it for DNA sequence classification. 
The aim is to classify a DNA sequence depending on if it binds a protein or not (transcription factor), or if a histone mark is present, or if a promoter is active.

[Script on Google Colab](https://colab.research.google.com/drive/19AQsrmiCnEfvgHKz7HQ27-vFsHQogrya).

## Pretraining of an LLM on DNA sequences


## Pretraining of an LLM on DNA sequences




