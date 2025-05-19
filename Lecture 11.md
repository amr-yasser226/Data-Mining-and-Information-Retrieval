## 1. Transformers & the Need for Positional Information

1. **Why do Transformers require positional encoding?**  
   Because they process all tokens in parallel and have no inherent notion of sequence order (unlike RNNs), so we must inject order information explicitly.

2. **How is positional information incorporated into token embeddings?**  
   By adding a positional encoding vector to each word embedding:  
$$
     \text{InputEmb}(pos) = \text{WordEmb}(pos) + \text{PosEnc}(pos)
$$

3. **What are the desired properties of positional encodings?**  
   - Unique per position  
   - Allow model to learn both short-range (high-frequency) and long-range (low-frequency) dependencies  
   - Smoothly varying so that relative positions can be inferred

---

## 2. Sinusoidal Positional Encoding

1. **What sinusoidal formulas are used for dimension $i$ at position $pos$?**  
$$
     \text{PE}_{pos,2k}   = \sin\!\bigl(\tfrac{pos}{10000^{2k/d}}\bigr),\quad
     \text{PE}_{pos,2k+1} = \cos\!\bigl(\tfrac{pos}{10000^{2k/d}}\bigr)
$$

2. **Why use different frequencies across dimensions?**  
   - High-frequency dimensions capture fine-grained, short-range position differences  
   - Low-frequency dimensions capture coarse, long-range position relationships

1. **Given $d=4$ and positions 0,1,2, compute the positional vectors:**  
   - **pos=0:** $[0,1,0,1]$  
   - **pos=1:** $[\sin(1),\cos(1),\sin(0.01),\cos(0.01)] \approx [0.8415,0.5403,0.01,0.99995]$  
   - **pos=2:** $[\sin(2),\cos(2),\sin(0.02),\cos(0.02)] \approx [0.9093,-0.4161,0.02,0.9998]$

4. **How do you combine word and positional embeddings?**  
   Element-wise addition:  
$$
     \text{FinalEmb} = \text{WordEmb} + \text{PosEnc}
$$

---

## 3. Self-Attention Mechanism

1. **What are the three projections computed from each token embedding?**  
   - Query $Q = XW^Q$  
   - Key   $K = XW^K$  
   - Value $V = XW^V$

1. **What is the purpose of the dot product $QK^\top$?**  
   To compute raw attention scores measuring similarity between each query and all keys.

2. **Why scale the dot products by $\sqrt{d_k}$?**  
   To prevent extremely large scores when $d_k$ (the key dimension) is large, which stabilizes gradients and softmax behavior.

3. **Write the full scaled dot-product attention formula.**  
$$
     \text{Attention}(Q,K,V) = \text{softmax}\!\bigl(\tfrac{QK^\top}{\sqrt{d_k}}\bigr)\,V
$$

5. **How does self-attention enable each token to gather context?**  
   By weighting and summing all value vectors according to attention weights, so each output encodes information from every other token.

---

## 4. Parallel Processing & Efficiency

1. **What allows Transformers to leverage massive parallelism?**  
   Self-attention computes all token interactions simultaneously, unlike RNNs which are inherently sequential.

2. **Name three hardware types optimized for parallel deep-learning workloads.**  
   - GPUs (thousands of CUDA cores)  
   - TPUs (matrix units for massive parallel matrix ops)  
   - Multi-core CPUs (fewer but more general cores)

---

## Multiple-Choice Questions

1. **Why do Transformers use positional encodings?**  
   A. To reduce model size  
   B. To inject sequence order  
   C. To replace word embeddings  
   D. To avoid softmax  
   **Answer:** B

2. **Which function is NOT used in sinusoidal positional encoding?**  
   A. sine  
   B. cosine  
   C. tanh  
   D. both sine & cosine  
   **Answer:** C

3. **In scaled dot-product attention, the scaling factor is:**  
   A. $d_k$  
   B. $\sqrt{d_k}$  
   C. $1/d_k$  
   D. $\log d_k$  
   **Answer:** B

4. **Self-attention’s input projections produce Q, K, V. What are these used for?**  
   A. Query, Key, Value  
   B. Quick, Knot, Verify  
   C. Query, Key, Vector  
   D. Query, Kernel, Value  
   **Answer:** A

5. **Adding positional encoding to word embeddings is done via:**  
   A. Concatenation  
   B. Matrix multiplication  
   C. Element-wise addition  
   D. Division  
   **Answer:** C

6. **High-frequency sinusoidal dimensions help the model learn:**  
   A. Long-range dependencies  
   B. Short-range dependencies  
   C. Stop-word lists  
   D. Regularization  
   **Answer:** B

7. **Transformers achieve parallelism because:**  
   A. They use convolution  
   B. They use recurrence  
   C. Self-attention computes all positions at once  
   D. They avoid softmax  
   **Answer:** C

8. **Which hardware is specifically designed for matrix operations in deep learning?**  
   A. CPU  
   B. GPU  
   C. TPU  
   D. FPGA  
   **Answer:** C

9. **The softmax in attention converts scores into:**  
   A. Logits  
   B. Probabilities summing to 1  
   C. Raw similarities  
   D. TF–IDF weights  
   **Answer:** B

10. **Without positional encoding, a Transformer cannot distinguish:**  
    A. Different words  
    B. Sequence order  
    C. Word frequency  
    D. Vocabulary size  
    **Answer:** B
