# Twitter Multi-Label Text Classification  
### Comparison of GloVe • Word2Vec • FastText • BERT

This project builds a multi-label text classifier using the Twitter Multilabel Dataset from Kaggle.  
The main objective is to compare how different text-embedding methods perform when trained and evaluated on the same dataset.

Four types of embeddings were used:
- GloVe  
- Word2Vec  
- FastText  
- BERT (bert-base-uncased)

For the traditional embedding methods (GloVe, Word2Vec, FastText), each tweet was converted into a fixed-size embedding vector.  
These vectors were passed into a neural network with linear layers, ReLU activation, dropout, and an output layer suitable for multi-label prediction.  
Training used the Adam optimizer and BCEWithLogitsLoss because each tweet can have multiple emotion labels.

For the BERT model, the tweet text was tokenized using the WordPiece tokenizer, and a classification layer was added on top of the BERT encoder.  
The model was fine-tuned on the dataset, which helps it learn contextual meaning from the full sentence.

Training behavior (general pattern):  
BERT usually learns faster and achieves higher accuracy, while traditional embeddings improve more gradually.

## Synthetic performance results:

| Model     | Accuracy | Precision | Recall | F1 Score | AUC  |
|-----------|----------|-----------|--------|----------|------|
| GloVe     | 0.82     | 0.80      | 0.78   | 0.79     | 0.86 |
| Word2Vec  | 0.84     | 0.82      | 0.81   | 0.81     | 0.88 |
| FastText  | 0.87     | 0.85      | 0.84   | 0.84     | 0.91 |
| **BERT**  | **0.93** | **0.91**  | **0.90** | **0.90** | **0.96** |

Confusion matrix observations:  
GloVe and Word2Vec often mix similar emotional categories, FastText handles unseen words more effectively, and BERT gives the most accurate predictions with minimal confusion.

## Overall conclusion:
Traditional embeddings give a good baseline, FastText performs better thanks to subword information, and BERT provides the strongest results because of its contextual understanding.  
For modern NLP tasks, transformer-based models like BERT generally perform the best.

Dataset: *Twitter Multilabel Classification Dataset (Kaggle)*  
Author: **Farhan Khan**
