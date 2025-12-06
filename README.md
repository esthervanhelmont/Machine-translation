# Machine-translation
ToU x Udacity Machine Translation

# Machine Translation with Deep Learning  
### English to French Neural Machine Translation  

---

## Overview  
This project implements an end-to-end Neural Machine Translation (NMT) system that translates English sentences into French using deep learning.  
Multiple architectures are trained and compared, from simple recurrent networks to encoder–decoder models, to explore how model complexity affects translation quality.

The final system uses an **Encoder–Decoder LSTM with Embeddings**, which provides the strongest performance.

---

## Project Objectives  
The goals of this project were:

1. **Understand and implement the preprocessing pipeline**
   - Tokenization of text  
   - Converting words to integer sequences  
   - Padding sentences to uniform length  

2. **Build and compare different translation models**
   - Simple RNN  
   - RNN with word embeddings  
   - Bidirectional RNN  
   - Encoder–Decoder model  
   - Final hybrid model combining best ideas  

3. **Train models and analyze performance**

4. **Meet Udacity assessment criteria**, including:
   - Complete preprocessing chain  
   - Correct neural architectures  
   - Evidence of experimentation  
   - Interpretation of results  
   - Clear, readable code  

---

## Dataset  
Each line in the English file corresponds to the French translation in the same line number of the French file.

| Property | English | French |
|----------|---------|--------|
| Total tokens | ~1.8M | ~1.9M |
| Unique words | 227 | 355 |
| Avg. sentence length | ~13 | ~15 |

The vocabulary size is small enough to train models efficiently while still demonstrating realistic machine translation behaviour.

---

## Preprocessing Pipeline  

### Tokenization  
Each corpus is tokenized using a Keras `Tokenizer`, producing:

- Integer sequences for each sentence  
- A vocabulary dictionary mapping word to index  

### Padding  
All sentences are padded to the maximum sequence length to allow batch processing.

### Label Reshaping  
French labels are reshaped to meet the input requirements of `sparse_categorical_crossentropy`.

---

## Models Implemented  

### 1. Simple RNN Model  
A minimal baseline translation model with:

- `SimpleRNN` layer  
- `TimeDistributed(Dense(...))` softmax outputs  

Accuracy: **~62%**  
Provides a baseline for comparison.

---

### 2. Embedding RNN Model  
Adds an `Embedding` layer to learn semantic word relationships.

Accuracy: **~84%**  
Produces noticeably more fluent translations.

---

### 3. Bidirectional RNN Model  
Processes input sequences in both directions.

Architecture:
- Embedding  
- Bidirectional GRU/LSTM  
- Dense time-distributed output  

Accuracy: **~67%**

Although stronger than the simple RNN, it does not outperform the embedding model alone.

---

### 4. Encoder–Decoder Model  
Follows the classical sequence-to-sequence translation structure.

**Encoder**
- Embedding  
- LSTM to context vector  

**Decoder**
- LSTM initialized with encoder states  
- TimeDistributed Dense softmax  

Accuracy: **~75%**

Provides better contextual understanding and sentence-level coherence.

---

### 5. Final Hybrid Model (Best)  
Combines the strengths of previous models:

- Embedding layer  
- Bidirectional LSTM encoder  
- RepeatVector for output alignment  
- Decoder LSTM  
- TimeDistributed Dense for final word predictions  

Performance:
- Training accuracy **>95%**  
- Validation accuracy **~94–96%**  
- High-quality translations, even for unseen sentences  
