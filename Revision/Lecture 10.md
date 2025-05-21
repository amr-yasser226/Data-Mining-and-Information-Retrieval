## 1. Term Representation

1. **What are the two main families of term representation?**  
   - **Local (sparse) representations:** Vector space models (e.g. TF-IDF, one-hot encoding)  
   - **Distributed (dense) representations:** Embeddings (observed via co-occurrence matrices or latent low-dimensional vectors)

2. **Name two common local representation methods.**  
   - **TF-IDF:** weighs term frequency by inverse document frequency  
   - **One-hot encoding:** binary vector indicating presence/absence of each term

3. **What are the static embedding algorithms covered?**  
   - **Word2Vec:**  
     1. Continuous Bag-of-Words (CBOW)  
     2. Skip-Gram  
   - **GloVe:** Global Vectors for word co-occurrence  
   - **Paragraph2Vec:** learns document-level embeddings  

4. **Which models produce contextual (dynamic) embeddings?**  
   - **RNN-based:** ELMo (Embeddings from Language Models)  
   - **Transformer-based:** BERT (Bidirectional Encoder Representations from Transformers)

---

## 2. Recurrent Neural Networks (RNNs)

1. **What key feature allows RNNs to handle sequences?**  
   - An **internal memory** (hidden state) that stores context from previous time steps.

2. **Why are RNNs well-suited to NLP and sequential tasks?**  
   - They process data **sequentially**, updating memory at each step, enabling contextual understanding.

3. **What are the three weight matrices in a basic RNN?**  
   - \(W_{xh}\): input → hidden  
   - \(W_{hh}\): previous hidden → current hidden  
   - \(W_{hy}\): hidden → output  

4. **How does an RNN incorporate past inputs into its current output?**  
   - The current hidden state \(h_t\) depends on both the new input \(x_t\) and the previous hidden state \(h_{t-1}\).

5. **Give a brief numeric example of an RNN sequence [1, 2].**  
   - **Time step 1** (input = 1): computes hidden \(h_1\) → output \(y_1\)  
   - **Time step 2** (input = 2 + memory from \(h_1\)): computes hidden \(h_2\) → output \(y_2\)  
   - Shows \(y_2\) reflects both inputs due to the hidden state’s memory.

---

## 3. RNN Limitations & LSTM

1. **What is the main training problem in vanilla RNNs?**  
   - **Vanishing gradients**, which hinder learning long-term dependencies in long sequences.

2. **How does LSTM address the vanishing gradient problem?**  
   - Introduces **gates** (input, forget, output) to control what information is kept, forgotten, or added, enabling retention of long-range context.

3. **When are LSTMs particularly useful?**  
   - Tasks requiring understanding of **long sequences**, e.g., speech recognition, long-form text generation, and time-series prediction.

---

## 4. ELMo (Embeddings from Language Models)

1. **What architecture does ELMo use?**  
   - **Two-layer bidirectional LSTM**: one reads forward (start→end), the other backward (end→start).

2. **How does ELMo differ from static embeddings?**  
   - Generates **contextualized vectors**: the same word can have different embeddings depending on its sentence context.

3. **Give an example showing ELMo’s contextual understanding.**  
   - Word “bank”:  
     - In “river bank,” ELMo’s embedding reflects a riverside meaning.  
     - In “deposit at the bank,” it reflects a financial institution.

4. **How is the final ELMo representation computed?**  
   1. Convert raw tokens to initial word vectors.  
   2. Feed into the first bidirectional LSTM → intermediate vectors.  
   3. Feed intermediates into the second bidirectional LSTM.  
   4. **Final embedding** = weighted sum of the raw + first-layer + second-layer representations.

---
