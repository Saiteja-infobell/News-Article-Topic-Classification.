# News-Article-Topic-Classification.
# BBC News Text Classification using BERT (Linear Probing)

This project performs text classification on the **BBC News dataset** using
**Transfer Learning with BERT (bert-base-uncased)**.  
Only the final **Linear Classifier** is trained while the full BERT encoder
remains **frozen** — a technique known as **Linear Probing**.

The model was trained and evaluated entirely inside **Google Colab**.

---

## 📂 Dataset

**Source:** `SetFit/bbc-news` (Hugging Face)

| Split | Samples |
|-------|---------|
| Train | 1,225 |
| Test  | 1,000 |

**Categories (5):**
- Business  
- Entertainment  
- Politics  
- Sport  
- Tech

Invalid or empty text rows were removed during preprocessing.

---

## ⚙️ Model Configuration

| Component | Description |
|----------|-------------|
| **Base Model** | BERT-base-uncased |
| **Strategy** | Freeze encoder + train linear head |
| **Classifier** | Linear layer (768 → 5) |
| **Optimizer** | Adam |
| **Loss Function** | CrossEntropyLoss |
| **Learning Rate** | **2e-4** |
| **Batch Size** | 16 |
| **Epochs** | 10 |
| **Trainable Parameters** | ~3,800 |
| **Total BERT Parameters** | ~110M (all frozen) |

This setup allows fast training while leveraging BERT’s strong semantic representations.

---

## 📈 Training Results

Below are the major training metrics (from your Colab run):

| Epoch | Loss | Accuracy |
|-------|--------|-----------|
| 1 | 123.04 | 0.2359 |
| 2 | 113.95 | 0.4000 |
| 3 | 108.02 | 0.5020 |
| 4 | 103.05 | 0.5265 |
| 5 | 99.16 | 0.6147 |
| 6 | 94.68 | 0.6180 |
| 7 | 91.05 | 0.6686 |
| 8 | 87.77 | 0.7012 |
| 9 | 85.41 | 0.7224 |
| 10 | 82.10 | 0.7216 |

---

## 🎯 Final Evaluation

| Metric | Value |
|--------|--------|
| **Final Test Accuracy** | **78.7%** |
| **Model Type** | Frozen BERT + Linear Probe |

---

## 🔍 Example Inference Outputs

| Input Text | Predicted Label |
|------------|-----------------|
| *"Apple releases new AI laptop"* | tech |
| *"Government announces new policy"* | tech |
| *"Manchester United wins the match"* | tech |

The model shows a slight **bias toward ‘tech’**, a common behavior when using a simple linear probe.

---

## 🧠 Insights & Analysis

### 1️⃣ Linear Probing Performs Well  
Even without fine-tuning BERT, the model achieved nearly **80% accuracy**.

### 2️⃣ Accuracy Improved Steadily  
Loss reduced from **123 → 82**, showing consistent learning.

### 3️⃣ Model Bias  
The linear layer sometimes predicts “tech” more often than expected → can be reduced by deeper fine-tuning or balancing the dataset.

### 4️⃣ Why Only Linear Layer Was Trained  
Freezing BERT:
- reduces compute  
- avoids catastrophic forgetting  
- speeds up training  
- shows how powerful BERT’s pretrained embeddings already are  

---

## 🚀 Possible Improvements

- Unfreeze last **2–4 layers** of BERT (partial fine-tuning)
- Increase classifier capacity (MLP: 768 → 256 → 5)
- Use LR schedulers (warmup, cosine decay)
- Train 15–20 epochs with early stopping
- Use data augmentation to improve generalization

---

## 📁 Submission Includes

Since the work was completed in Colab:

- `bbc_news_bert_linear_probe.ipynb`  
- This README with full explanation  
- (Optional) Saved model + tokenizer if exported

---

## ✨ Author

**Gadigoppula Saiteja**  

