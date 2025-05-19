## 1. Term Representation

1. **What are the two broad categories of term representation?**  
   - Local (each term independent)  
   - Distributed (terms represented by features or embeddings)

2. **Give two examples of local representations.**  
   3. One-hot encoding  
   4. TF–IDF vectors

5. **What distinguishes observed vs. latent distributed representations?**  
   - Observed: hand-crafted or co-occurrence features (interpretable)  
   - Latent: learned dense embeddings (not directly interpretable)

---

## 2. Local Representation

1. **What is one-hot encoding (OHE)?**  
   A binary vector where only the index of the given term is 1 and all others are 0.

2. **Why does OHE fail to capture semantic similarity?**  
   Cosine similarity between any two distinct one-hot vectors is zero.

3. **Give an example OHE for vocabulary [red, green, blue].**  
   - red → (1, 0, 0)  
   - green → (0, 1, 0)  
   - blue → (0, 0, 1)

---

## 3. Observed Distributed Representation

1. **What is an observed distributed representation?**  
   A vector where each dimension corresponds to a known feature (e.g., “has tail,” “fruit”).

2. **How can a co-occurrence matrix be viewed as an observed representation?**  
   Rows/columns are words, cells count how often pairs co-occur within a context window.

3. **List two drawbacks of co-occurrence matrices.**  
   4. Very high dimensionality  
   5. Sparsity and poor performance on analogies

---

## 4. Latent Distributed Representation (Embeddings)

1. **What are embeddings?**  
   Dense, low-dimensional vectors learned from data that capture semantic relations.

2. **Name three static (context-independent) embedding models.**  
   3. Word2Vec (CBOW & Skip-Gram)  
   4. GloVe  
   5. Paragraph2Vec

6. **Name two contextual embedding models.**  
   7. ELMo (RNN-based)  
   8. BERT (Transformer-based)

---

## 5. Word2Vec: CBOW & Skip-Gram

1. **What does CBOW predict?**  
   A target word given its context words in a fixed window.

2. **What does Skip-Gram predict?**  
   Context words given a target word.

3. **How is the training objective implemented?**  
   Using one-hot inputs, a hidden embedding layer, and a softmax output to maximize prediction likelihood.

---

## 6. GloVe (Global Vectors)

1. **What key matrix does GloVe use to learn embeddings?**  
   The word–word co-occurrence matrix.

2. **How does GloVe incorporate global statistics?**  
   It minimizes weighted least-squares between dot products of embeddings and the log of co-occurrence counts.

---

## Multiple-Choice Questions

1. **Which representation yields zero similarity between all distinct terms?**  
   A. One-hot encoding  
   B. TF–IDF  
   C. Word embeddings  
   D. Observed features  
   **Answer:** A

2. **An observed distributed vector for “banana” might include a 1 for which feature?**  
   A. “has tail”  
   B. “is fruit”  
   C. “is animal”  
   D. “barks”  
   **Answer:** B

3. **Co-occurrence matrices are typically:**  
   A. Dense and low-dimensional  
   B. Sparse and high-dimensional  
   C. Learned via backpropagation  
   D. Limited to binary features  
   **Answer:** B

4. **Word2Vec’s Skip-Gram model maximizes:**  
   A. P(target | context)  
   B. P(context | target)  
   C. P(term frequency)  
   D. Cosine similarity  
   **Answer:** B

5. **GloVe embeddings are trained using:**  
   A. Local window predictions only  
   B. Global co-occurrence counts  
   C. User click logs  
   D. One-hot vectors without training  
   **Answer:** B

6. **Contextual embeddings (e.g., BERT) differ from static ones because they:**  
   A. Use one-hot encoding  
   B. Produce different vectors for a word based on its sentence context  
   C. Rely on co-occurrence matrices  
   D. Are always lower-dimensional than Word2Vec  
   **Answer:** B

7. **Which technique can solve OHE’s inability to capture similarity?**  
   A. Increasing vocabulary size  
   B. Distributed embeddings  
   C. More stop-word removal  
   D. Boolean retrieval  
   **Answer:** B

8. **In a co-occurrence matrix with window size = 1, “I like NLP” produces which pair?**  
   A. (I, NLP)  
   B. (I, like)  
   C. (like, everyday)  
   D. (NLP, I)  
   **Answer:** B

9. **CBOW uses as input:**  
   A. One-hot vector of the target word  
   B. Sum or average of one-hot vectors of context words  
   C. Full co-occurrence matrix  
   D. Document frequency only  
   **Answer:** B

10. **Which latent model can produce embeddings for entire paragraphs?**  
    A. Word2Vec  
    B. GloVe  
    C. Paragraph2Vec  
    D. One-hot encoding  
    **Answer:** C
