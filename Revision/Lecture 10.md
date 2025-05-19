## 1. Term Representation Overview

1. **What are the two main categories of term representation?**  
   Local (each term independent) and Distributed (terms share features or embeddings).

2. **Give two examples of local representations.**  
   3. One-hot encoding  
   4. TF–IDF vectors

5. **What distinguishes observed from latent distributed representations?**  
   - Observed: feature-based, interpretable (e.g., co-occurrence counts)  
   - Latent: learned dense embeddings (e.g., Word2Vec, GloVe)

4. **Name three static (context-independent) embedding models.**  
   5. Word2Vec (CBOW & Skip-Gram)  
   6. GloVe  
   7. Paragraph2Vec

8. **Name two contextual (context-dependent) embedding models.**  
   9. ELMo (bi-LSTM based)  
   10. BERT (Transformer based)

---

## 2. Local Representation

1. **What is one-hot encoding?**  
   A binary vector marking one term’s position with 1 and all others 0.

2. **Why does one-hot encoding fail to capture semantic similarity?**  
   Distinct one-hot vectors have zero dot product, implying no similarity.

3. **Example:** Vocabulary = [red, green, blue]  
   - red → (1, 0, 0)  
   - green → (0, 1, 0)  
   - blue → (0, 0, 1)

---

## 3. Observed Distributed Representation

1. **What is an observed distributed representation?**  
   A feature vector where each dimension is a human-interpretable property (e.g., “is fruit,” “has tail”).

2. **How does a co-occurrence matrix serve as an observed representation?**  
   Rows and columns are words; entries count how often word pairs appear within a context window.

3. **List two drawbacks of co-occurrence matrices.**  
   4. High dimensionality  
   5. Sparsity and poor analogy performance

---

## 4. Latent Distributed Representation (Embeddings)

1. **What are embeddings?**  
   Dense, low-dimensional vectors learned from data that capture semantic relations.

2. **Why are embeddings preferred over one-hot or co-occurrence vectors?**  
   They are dense, lower-dimensional, capture similarity, and support analogies.

---

## 5. Word2Vec: CBOW & Skip-Gram

1. **What does CBOW predict?**  
   The target word given its surrounding context words.

2. **What does Skip-Gram predict?**  
   The context words given a target word.

3. **How is training structured in Word2Vec?**  
   One-hot input → hidden embedding layer → softmax output predicting words.

---

## 6. GloVe (Global Vectors)

1. **What key statistic does GloVe use to learn embeddings?**  
   The global word–word co-occurrence matrix.

2. **How does GloVe incorporate co-occurrence counts?**  
   By minimizing a weighted least-squares objective between dot products of embeddings and log counts.

---

## 7. Contextual Embeddings: RNNs & LSTMs

1. **What is the main advantage of RNNs for text?**  
   They maintain an internal memory, processing sequences while preserving order.

2. **Name the three weight matrices in a vanilla RNN.**  
   - $W_{xh}$: input → hidden  
   - $W_{hh}$: previous hidden → current hidden  
   - $W_{hy}$: hidden → output

3. **What problem do RNNs suffer from on long sequences?**  
   Vanishing gradients, which impair learning long-term dependencies.

4. **How do LSTMs address vanishing gradients?**  
   By using gated cells (input, forget, output gates) to control information flow.

---

## 8. ELMo (Embeddings from Language Models)

1. **What architecture does ELMo use?**  
   Two-layer bidirectional LSTMs to capture both forward and backward context.

2. **How does ELMo produce context-dependent vectors?**  
   It combines hidden states from forward and backward LSTMs at each position.

3. **Give an example of ELMo disambiguating “bank.”**  
   - “river bank” vs. “financial bank” yield different embeddings based on surrounding words.

---

## Multiple-Choice Questions

1. **Which representation is guaranteed to be orthogonal for all distinct terms?**  
   A. TF–IDF  
   B. One-hot encoding  
   C. Word embeddings  
   D. Co-occurrence vectors  
   **Answer:** B

2. **A co-occurrence matrix entry (i,j) counts:**  
   A. tf–idf weight of term i in document j  
   B. How many times terms i and j appear within a window  
   C. Inverse document frequency of term i  
   D. Cosine similarity of terms i and j  
   **Answer:** B

3. **Word2Vec’s Skip-Gram model maximizes:**  
   A. P(target | context)  
   B. P(context | target)  
   C. TF–IDF weights  
   D. Dice coefficient  
   **Answer:** B

4. **GloVe embeddings are trained by factorizing:**  
   A. One-hot vectors  
   B. Co-occurrence matrix  
   C. Query logs  
   D. User feedback  
   **Answer:** B

5. **Which RNN weight connects hidden state at $t-1$ to hidden state at $t$?**  
   A. $W_{xh}$  
   B. $W_{hy}$  
   C. $W_{hh}$  
   D. Bias  
   **Answer:** C

6. **LSTMs use gates to control:**  
   A. Vocabulary size  
   B. Word order  
   C. Information flow and memory retention  
   D. Co-occurrence counts  
   **Answer:** C

7. **ELMo generates different embeddings for a word based on:**  
   A. Its global frequency  
   B. Its position in the vocabulary  
   C. The surrounding context in the sentence  
   D. Its part-of-speech tag only  
   **Answer:** C

8. **Which model produces embeddings for entire paragraphs?**  
   A. Word2Vec  
   B. GloVe  
   C. Paragraph2Vec  
   D. One-hot encoding  
   **Answer:** C

9. **Contextual embeddings differ from static ones because they:**  
   A. Are one-hot vectors  
   B. Use co-occurrence counts only  
   C. Vary with sentence context  
   D. Are always lower-dimensional than static embeddings  
   **Answer:** C

10. **The main drawback of vanilla RNNs is:**  
    A. High dimensionality  
    B. Vanishing/exploding gradients  
    C. Zero similarity between words  
    D. Lack of interpretability  
    **Answer:** B
