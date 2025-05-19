## 1. BM25 Ranking Function

1. **What is the Okapi BM25 ranking function?**  
   A term-weighted ranking formula that extends TF–IDF by normalizing for document length and saturating term frequency.

2. **Write the BM25 score formula for a single term t in document D and query Q.**  
$$
     \mathrm{BM25}(D,Q) \;=\; \sum_{t \in Q} \mathrm{IDF}(t)\,\frac{\mathrm{tf}_{t,D}\,(k_1 + 1)}
       {\mathrm{tf}_{t,D} + k_1 \bigl(1 - b + b \cdot \tfrac{|D|}{\mathrm{avgDL}}\bigr)}
$$

3. **What do the parameters \(k_1\) and \(b\) control?**  
   - \(k_1\): term-frequency saturation (typical range 1.2–2.0)  
   - \(b\): document-length normalization (typical default 0.75)

2. **How is \($\mathrm{IDF}(t)$\) computed in BM25?**  
$$
     \mathrm{IDF}(t) = \log\!\frac{N - \mathrm{df}_t + 0.5}{\mathrm{df}_t + 0.5}
$$

3. **Why is BM25 preferred over plain TF–IDF?**  
   - Prevents long documents from dominating by length normalization  
   - Controls diminishing returns of repeated terms with ($k_1$)

---

## 2. Vector Space Model & Cosine Similarity

1. **How are documents and queries represented in the Vector Space Model (VSM)?**  
   As high-dimensional vectors of term weights (e.g., TF–IDF).

2. **Why is Euclidean distance not ideal for comparing document and query vectors?**  
   It penalizes document length and duplicates: if you append a document to itself, distance grows despite identical content.

3. **What similarity measure fixes this?**  
   **Cosine similarity**, which depends only on the angle between vectors:
$$
     \cos(\theta) = \frac{\mathbf{d} \cdot \mathbf{q}}{\|\mathbf{d}\|\,\|\mathbf{q}\|}
$$

---

## 3. TF–IDF Term Weighting

1. **Define term frequency (tf) and how it is log-weighted.**  
$$
     \mathrm{tf}_{t,d} = \text{raw count},\quad
     w_{t,d}^{(\rm tf)} = 1 + \log_{10}(\mathrm{tf}_{t,d})
$$

2. **What is document frequency (df) and inverse document frequency (idf)?**  
   - ($\mathrm{df}_t$): number of docs containing term \(t\)  
   - ($\mathrm{idf}_t = \log_{10}\tfrac{N}{\mathrm{df}_t}$)

3. **Write the combined TF–IDF weight.**  
$$
     w_{t,d} = (1 + \log_{10}\mathrm{tf}_{t,d}) \times \log_{10}\!\tfrac{N}{\mathrm{df}_t}
$$

4. **How is a document’s score for query Q computed under TF–IDF & cosine?**  
   Build weighted vectors for D and Q, then compute ($\cos(\theta)$).

---

## 4. Worked Examples

1. **BM25 for two docs and query “deep learning”:**  
   - N=2, |D₁|=5, |D₂|=6, avgDL=5.5, \(k_1=1.5\), \(b=0.75\).  
   - df(deep)=2, df(learning)=2 → IDF≈0.08 each.  
   - Compute BM25₁≈0.083, BM25₂≈0.077 → rank D₁ above D₂.

2. **BM25 for D₁: “the sky is blue”, D₂: “the sun is bright”, D₃: “the sun in the blue sky”**, query “blue sky”:  
   - N=3, |D₁|=4, |D₂|=4, |D₃|=6, avgDL≈4.7, \(k_1=1.5\), \(b=0.75\).  
   - df(blue)=2→idf≈0.204, df(sky)=2→idf≈0.204.  
   - Compute BM25₁, BM25₃ (D₂ score=0); rank accordingly.

3. **Cosine similarity example:**  
   - Document: “car insurance auto insurance”  
   - Query: “best car insurance”  
   - Given df and tf tables, compute tf–idf weights, build vectors, and find ($\cos(d,q)≈0.8$).

4. **Zewail CSAI school example:**  
   - Two docs, query “Zewail CSAI school”, compute tf, df, idf, tf–idf weights, then cosine → identify most relevant doc.

5. **Digital Cameras example:**  
   - Doc: “digital cameras video cameras”, query “digital cameras”, N=10 000 000, given df table → compute tf–idf weights and cosine.

---

## Multiple-Choice Questions

1. **Which BM25 parameter controls length normalization?**  
   A. $(k_1$)  
   B. \(b\)  
   C. avgDL  
   D. IDF  
   **Answer:** B

2. **In VSM, cosine similarity ranges between:**  
   A. –1 and 1  
   B. 0 and 1  
   C. –∞ and +∞  
   D. 0 and ∞  
   **Answer:** B

3. **Log-frequency weighting uses \(1 + \log_{10}(tf)\) to:**  
   A. Emphasize very high tf linearly  
   B. Dampen the effect of high tf  
   C. Normalize by document length  
   D. Compute df  
   **Answer:** B

4. **IDF is highest for a term that appears in:**  
   A. Almost every document  
   B. Exactly half the documents  
   C. Only one document  
   D. No documents  
   **Answer:** C

5. **Under BM25, if \(|D|\) increases while tf stays the same, the term’s weight:**  
   A. Increases  
   B. Decreases  
   C. Remains constant  
   D. Becomes IDF  
   **Answer:** B

6. **Euclidean distance fails in VSM when:**  
   A. Comparing two identical texts of different lengths  
   B. Query and document share no terms  
   C. Vectors are normalized  
   D. Using TF–IDF weights  
   **Answer:** A

7. **A document that contains no query terms under BM25 receives a score of:**  
   A. ∞  
   B. 0  
   C. IDF sum  
   D. $(k_1$)  
   **Answer:** B

8. **Cosine similarity is invariant to:**  
   A. Vector direction  
   B. Vector magnitude  
   C. Both magnitude and direction  
   D. None of the above  
   **Answer:** B

9. **TF–IDF weight of term t in d is zero if:**  
   A. tf$(_{t,d}=0$)  
   B. df\(_t = N\)  
   C. Either A or B  
   D. Neither A nor B  
   **Answer:** C

10. **In the “digital cameras” example, increasing N (collection size) will:**  
    A. Increase idf of both terms  
    B. Decrease idf of both terms  
    C. Leave idf unchanged  
    D. Affect only df  
    **Answer:** A
