## 1. BERT Overview

1. **What does BERT stand for and why is it “bidirectional”?**  
   BERT stands for **Bidirectional Encoder Representations from Transformers**. Its Transformer encoder attends to both left and right context for each token simultaneously, rather than processing in a fixed left‑to‑right or right‑to‑left order.

2. **How does BERT differ from unidirectional models like GPT or LSTMs?**  
   - **Unidirectional models** process tokens sequentially (e.g., left‑to‑right), so each token’s representation only sees preceding context.  
   - **BERT’s bidirectional attention** lets each token attend to all other tokens in the sequence, enabling richer contextual understanding.

3. **Why is bidirectionality important for disambiguation?**  
   It uses both preceding and following words, so ambiguous tokens like “bank” in “The bank was full of fish” are correctly interpreted as a riverbank, not a financial institution.

---

## 2. Input Representation

1. **What three embeddings are summed to form BERT’s input vectors?**  
   - **Token Embedding:** Subword tokens from WordPiece (e.g., “playing” → “play”, “##ing”).  
   - **Segment Embedding:** Distinguishes sentence A vs. B when two segments are given.  
   - **Position Embedding:** Sinusoidal or learned vectors that encode each token’s position.

2. **What special tokens does BERT use and why?**  
   - **[CLS]:** Prepended to every sequence; its final hidden state is used for classification tasks.  
   - **[SEP]:** Separates sentence pairs and marks the end of a single-sentence input.

3. **Example:**  
   Input `[CLS] He went to the bank [SEP] It was closed [SEP]`  
   – Each token gets a WordPiece embedding + segment ID (A or B) + positional encoding.

---

## 3. Bidirectional Self‑Attention

1. **How does BERT’s self‑attention differ from a vanilla Transformer?**  
   While both use scaled dot‑product attention, BERT’s pretraining applies attention over the entire sequence at once—no causal mask—so tokens attend equally in both directions.

2. **Why is bidirectional attention more powerful?**  
   It lets each token’s representation incorporate information from all other tokens, improving understanding of complex or ambiguous constructs.

---

## 4. Masked Language Modeling (MLM)

1. **What is the MLM pretraining objective?**  
   Randomly mask 15% of input tokens and train BERT to predict the masked tokens using surrounding context on both sides.

2. **Example:**  
   Input: `[CLS] He went to the [MASK] [SEP]`  
   Target: `bank`  
   BERT must leverage “He went to the” and “It was closed” (if provided) to predict “bank.”

---

## 5. Next Sentence Prediction (NSP)

1. **What is the NSP task in BERT pretraining?**  
   Given sentence A and sentence B, predict whether B follows A in the original text.

2. **How is NSP implemented?**  
   Use the final hidden state of the [CLS] token and a simple classification head to output “IsNext” vs. “NotNext.”

---

## 6. Transformer Encoder Stack & Output

1. **What architecture does BERT use after input embeddings?**  
   A stack of N Transformer encoder layers (e.g., 12 layers in BERT‑Base, 24 in BERT‑Large).

2. **What outputs does BERT produce?**  
   - **Token-level vectors:** Contextual embeddings for each position, used for tagging tasks.  
   - **[CLS] vector:** Aggregate representation for classification or sequence‑level tasks.

---

## 7. BERT for Ranking & Multi‑Stage Reranking

1. **How can BERT be applied to document ranking?**  
   Frame ranking as binary relevance classification: given (query, doc), use BERT to predict relevance probability, then sort by that score.

2. **What is MonoBERT vs. DuoBERT?**  
   - **MonoBERT:** Scores each document independently with BERT.  
   - **DuoBERT:** Considers document pairs and predicts which is more relevant, refining the ranking further.

3. **Why use a multi‑stage pipeline?**  
   Balance **efficiency** (fast first‑stage retrieval with BM25 or TF–IDF) and **effectiveness** (accurate BERT‑based reranking on a small candidate set).

---

## 8. Numerical Multi‑Stage Example

**Collection:**  
1. d1: “Machine learning is a subset of artificial intelligence.”  
2. d2: “Deep learning is a type of machine learning.”  
3. d3: “Artificial intelligence has various applications.”  
4. d4: “Natural language processing is a field within AI.”  
5. d5: “Supervised learning is a type of machine learning.”

**Query:** “machine learning”

### Stage 1 (TF–IDF / BM25)  
TF–IDF scores:  
- d2: 0.9  
- d1: 0.8  
- d5: 0.7  
- d3: 0.6  
- d4: 0.4  

**Ranking:** d2 > d1 > d5 > d3 > d4

### Stage 2 (MonoBERT rerank)  
MonoBERT scores:  
- d1: 0.85  
- d2: 0.82  
- d3: 0.78  
- d4: 0.65  
- d5: 0.42  

**Reranked:** d1 > d2 > d3 > d4 > d5

### Stage 3 (DuoBERT pairwise)  
Pairwise win probabilities \(p_{i,j}\):  
- \(p_{1,2}=0.9\), \(p_{1,3}=0.8\), \(p_{1,4}=0.6\), \(p_{1,5}=0.7\)  
- \(p_{2,3}=0.7\), \(p_{2,4}=0.5\), \(p_{2,5}=0.4\)  
- \(p_{3,4}=0.8\), \(p_{3,5}=0.9\)  
- \(p_{4,5}=0.6\)

Compute aggregate score \(S_i = \sum_{j\neq i} p_{i,j}\):  
- \(S_1 = 0.9+0.8+0.6+0.7 = 3.0\)  (d1)  
- \(S_2 = 0.9+0.7+0.5+0.4 = 2.5\)  (d2)  
- \(S_3 = 0.8+0.7+0.8+0.9 = 3.2\)  (d3)  
- \(S_4 = 0.6+0.5+0.8+0.6 = 2.5\)  (d4)  
- \(S_5 = 0.7+0.4+0.9+0.6 = 2.6\)  (d5)

**Final DuoBERT ranking:**  
1. d3 (3.2)  
2. d1 (3.0)  
3. d5 (2.6)  
4. d2 (2.5, before d4 in previous stage)  
5. d4 (2.5)

---

## Multiple-Choice Questions

1. **What does the [CLS] token’s final hidden state represent?**  
   A. The first token embedding only  
   B. A classification summary of the entire sequence  
   C. The last token embedding only  
   D. Positional encodings  
   **Answer:** B

2. **In BERT’s MLM pretraining, what percentage of tokens are masked?**  
   A. 5%  
   B. 15%  
   C. 50%  
   D. 100%  
   **Answer:** B

3. **What task does NSP train BERT to perform?**  
   A. Predict next word in a sentence  
   B. Classify sentiment  
   C. Decide if one sentence follows another  
   D. Generate text  
   **Answer:** C

4. **Which embedding types are summed to form BERT’s input vector?**  
   A. Token, Position, Segment  
   B. Token, TF–IDF, Position  
   C. Word2Vec, GloVe, LSTM  
   D. One-hot, Co-occurrence, Positional  
   **Answer:** A

5. **MonoBERT refers to:**  
   A. Pairwise document comparison  
   B. Single-document classification for relevance  
   C. Multi-head self-attention  
   D. Next sentence prediction  
   **Answer:** B

6. **Why use a multi-stage retrieval pipeline?**  
   A. To reduce model size  
   B. To balance retrieval speed and accuracy  
   C. To avoid using BM25  
   D. To train BERT from scratch  
   **Answer:** B

7. **In sinusoidal positional encoding, higher-frequency dimensions encode:**  
   A. Long-range dependencies  
   B. Short-range dependencies  
   C. Token identities  
   D. Segment IDs  
   **Answer:** B

8. **DuoBERT improves ranking by:**  
   A. Masking tokens  
   B. Pairwise comparisons of candidate documents  
   C. Increasing BM25 parameters  
   D. Using one-hot embeddings  
   **Answer:** B

9. **In the numerical example, which document ended up ranked first by DuoBERT?**  
   A. d1  
   B. d2  
   C. d3  
   D. d5  
   **Answer:** C

10. **BERT’s bidirectional attention allows each token to see:**  
    A. Only preceding tokens  
    B. Only following tokens  
    C. Both preceding and following tokens  
    D. No other tokens  
    **Answer:** C
