# Twitter Multi-Label Text Classification  
### Comparison of GloVe • Word2Vec • FastText • BERT (GPU Training)

This project builds a multi-label text classifier using the Twitter Multilabel Dataset from Kaggle.  
The goal is to compare how different text-embedding methods perform when trained on the same dataset using GPU acceleration.

Four types of embeddings were tested:
- GloVe  
- Word2Vec  
- FastText  
- BERT (bert-base-uncased)

For the classical methods (GloVe, Word2Vec, FastText), the tweets were converted into fixed-size embedding vectors.  
These vectors were passed to a simple neural network with linear layers, ReLU activation, dropout, and a final output layer.  
Training used the Adam optimizer and BCEWithLogitsLoss because the task contains multiple labels per tweet.

For the BERT model, the built-in tokenizer was used to break text into subword tokens.  
Only a small classification head was added on top of the BERT encoder and the entire model was fine-tuned on GPU.  
BERT learns context from full sentences, giving it a natural advantage over static embeddings.

Training trends (synthetic pattern):  
BERT usually learns the fastest and reaches the highest accuracy, while classic embeddings improve more slowly.

**Synthetic performance comparison:**

| Model     | Accuracy | Precision | Recall | F1 Score | AUC  |
|-----------|----------|-----------|--------|----------|------|
| GloVe     | 0.82     | 0.80      | 0.78   | 0.79     | 0.86 |
| Word2Vec  | 0.84     | 0.82      | 0.81   | 0.81     | 0.88 |
| FastText  | 0.87     | 0.85      | 0.84   | 0.84     | 0.91 |
| **BERT**  | **0.93** | **0.91**  | **0.90** | **0.90** | **0.96** |

General confusion-matrix observations:  
GloVe and Word2Vec often confuse emotions with similar wording, FastText handles unknown words better, and BERT provides the most accurate and clean predictions with very few misclassifications.

**Overall conclusion:**  
Traditional embeddings are useful and lightweight, FastText performs better because of subword information, but BERT gives the strongest performance due to its contextual understanding.  
For real NLP applications, transformer-based models are the most effective choice.

Dataset used: *Twitter Multilabel Classification Dataset (Kaggle)*  
Author: **Farhan Khan**
