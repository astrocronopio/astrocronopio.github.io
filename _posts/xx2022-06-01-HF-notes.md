---
layout: post
title: Hugging Face Course Notes
categories: [coding, ML]
---
## Chapter 2 - Using HF Transformers

### About the input/output values of the HF Transformers
You can use 🤗 Transformers without having to worry about which ML framework is used as a backend; it might be PyTorch or TensorFlow, or Flax for some models. However, *Transformer models only accept tensors as input*. 

To specify the type of tensors we want to get back (PyTorch, TensorFlow, or plain NumPy), we use the `return_tensors` argument: 'pt', 'tf' & 'np'? Default is a python list.

### About TF and the heads

A model can be used for different purposes, it learns a set of hidden parameters/states then a 'head' changes these values to the task we want to do. The hidden states are a final representation of the input, then this is transformed into the actual output.

Embeddings into the tokenized input <br>
'AutoModel' is the model without a head
'AutoTokenizer' is the Embeddings layers?
'AutoModelForSequenceClassification' is a head for classification 
 

### 
