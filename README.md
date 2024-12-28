# README: Comparative Analysis of Video Classification Models Using the TikHarm Dataset

## Overview
This project aimed to build and evaluate multiple machine learning models for video classification using the TikHarm dataset from Kaggle as a benchmark. We focused on extracting captions and features from videos, and training and comparing different architectures for the classification task. Below is a step-by-step description of our process and findings.

---

## Process

### 1. Dataset and Preprocessing
We used the TikHarm dataset from Kaggle. Our preprocessing steps included:
1. **Frame Extraction**: We extracted 5 key frames from each video using the following code:
   - Library: `OpenCV`
   - Functionality: Extract frames at equally spaced intervals.

2. **Caption Generation**: For each key frame, captions were generated using the BLIP model:
   - Library: `transformers` (Salesforce BLIP model)
   - Output: Captions concatenated into a single string for each video.

---

### 2. Models and Architectures

#### Model 1: Bidirectional LSTM (BiLSTM)
**Hyperparameters**:
- Embedding Dimension: Pre-trained Word2Vec embeddings.
- LSTM Units: 128
- Dropout Rate: 0.3
- Batch Size: 32
- Epochs: 10

**Results**:
- Final Training Accuracy: 90.43%
- Final Validation Accuracy: 89.03%

**Findings**:
- BiLSTM captured sequential dependencies effectively but showed overfitting due to the validation accuracy being slightly lower than training accuracy.

#### Model 2: Bidirectional LSTM with Attention Mechanism
**Hyperparameters**:
- Embedding Dimension: Pre-trained Word2Vec embeddings.
- LSTM Units: 128
- Attention Layer: Custom implementation for context extraction.
- Dropout Rate: 0.3
- Batch Size: 32
- Epochs: 10

**Results**:
- Final Training Accuracy: 87.63%
- Final Validation Accuracy: 84.44%

**Findings**:
- The addition of attention improved context understanding but slightly reduced overall accuracy compared to pure BiLSTM, potentially due to increased model complexity.

#### Model 3: Transformer-based Architecture
**Hyperparameters**:
- Embedding Dimension: 128
- Number of Attention Heads: 4
- Feedforward Network Size: 128
- Dropout Rate: 0.3
- Batch Size: 32
- Epochs: 10

**Results**:
- Final Training Accuracy: 92.09%
- Final Validation Accuracy: 91.84%

**Classification Report**:
| Class           | Precision | Recall | F1-Score | Support |
|-----------------|-----------|--------|----------|---------|
| Harmful Content | 0.94      | 0.85   | 0.89     | 123     |
| Safe            | 0.94      | 0.88   | 0.91     | 116     |
| Suicide         | 0.89      | 1.00   | 0.94     | 153     |
| **Accuracy**    | **0.92**  |        |          | 392     |

**Findings**:
- The transformer model achieved the best results among all architectures, demonstrating its ability to capture long-range dependencies and contextual relationships effectively.

#### Model 4: State Space Model
**Results**:
- Test Accuracy: 84.948%

**Findings**:
- While simpler, the state space model underperformed compared to the transformer model. It struggled with more complex relationships in the data.

---

## Comparative Analysis
From our experimentation, the transformer-based model emerged as the most effective for video classification using the TikHarm dataset, achieving the highest accuracy and F1-scores. The BiLSTM and BiLSTM with attention mechanisms demonstrated the importance of sequential modeling, while the state space model provided a baseline comparison.

**Key Observations**:
1. Transformer models excel at capturing contextual and sequential information in video captions.
2. Attention mechanisms improve interpretability but may not always yield better accuracy.
3. Proper preprocessing and feature extraction (e.g., using BLIP for captioning) are crucial for achieving high classification performance.

---

## Conclusion
This project highlights the comparative strengths and weaknesses of various architectures for video classification. The transformer model demonstrated the best overall performance, and this study provides a foundation for future exploration of hybrid models or further optimization on the TikHarm dataset.

The findings from this project are documented in detail in our research paper: **"Comparative Analysis of Video Classification Models Using the TikHarm Dataset."**

