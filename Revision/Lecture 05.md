## 1. Reusable Test Collections

1. **What are Reusable Test Collections?**  
   Standardized datasets for IR evaluation, consisting of a document collection, topics (information needs), and relevance judgments (qrels).

2. **What is a Document Collection?**  
   A set of documents to be searched—can be structured (databases, JSON) or unstructured (raw text, web pages).

3. **What are Topics?**  
   Sample information needs or queries, expressed in natural language or keyword form.

4. **What are Relevance Judgments (qrels)?**  
   Human- or machine-assigned mappings from queries to documents indicating relevance (e.g., 0 = not relevant, 1 = partially, 2 = highly).

---

## 2. Main IR Evaluation Campaigns

1. **What is TREC?**  
   The Text REtrieval Conference by NIST since 1992, providing collections, topics, and shared tasks across many IR tracks.

2. **What is CLEF?**  
   The Conference and Labs of the Evaluation Forum (Europe), focusing on multilingual and cross-lingual IR since 2000.

3. **What is NTCIR?**  
   The NII Testbeds and Community for Information access Research (Asia), run by Japan’s NII since 1999 on Asian languages and QA.

4. **What is FIRE?**  
   The Forum for Information Retrieval Evaluation (India) since 2008, emphasizing South Asian languages and diverse IR tasks.

---

## 3. TREC Qrels Format

1. **Describe the TREC qrel file line format.**  
   `<query_id> <iteration> <document_id> <relevance>`, where iteration is usually 0.

2. **What do the relevance values mean?**  
   0 = not relevant, 1 = partially relevant, 2 = highly relevant.

3. **How are qrels used?**  
   To compute metrics like precision, recall, MAP, and NDCG by comparing system outputs to gold judgments.

---

## 4. Ranked Retrieval

1. **What is ranked retrieval?**  
   Assigning a relevance score S(d,q) to each document for query q, then returning documents sorted by score.

2. **How does ranked retrieval differ from Boolean?**  
   - No Boolean syntax required  
   - Results are ordered by predicted relevance  
   - Typically only the top-k (e.g., 10) are shown

---

## 5. Scoring Example: Jaccard Coefficient

1. **What is the Jaccard Similarity Coefficient?**  
   $$
     J(A,B) = \frac{|A \cap B|}{|A \cup B|}
   $$

2. **What is its range?**  
   0 (no overlap) to 1 (identical sets).

3. **How is it used in IR?**  
   Comparing query and document term sets after preprocessing.

4. **What are its limitations?**  
   Ignores term frequency and semantic relationships.

5. **Example:**  
   Query `{arab, world}` vs. Document `{fifa, world, cup, arab, country}` →  
   \(|A∩B|=2, |A∪B|=5 ⇒ J=0.4\).

---

## 6. Term-Document Count Matrix

1. **What is the Term-Document Count Matrix?**  
   A matrix where rows = terms, columns = documents, and each cell = raw term frequency (tf).

2. **Give an example.**

| Term     | D1 | D2 | D3 |
|----------|----|----|----|
| AI       |  3 |  0 |  1 |
| Machine  |  2 |  1 |  0 |
| Learning |  1 |  4 |  2 |
| Model    |  0 |  2 |  1 |
3. **What are its limitations?**  
   - Loses word order and context  
   - High dimensionality and sparsity  
   - Treats all words equally

---

## 7. Term Frequency & Log-Frequency Weighting

1. **What is term frequency (tf)?**  
   The raw count of occurrences of term t in document d, \(tf_{t,d}\).

2. **Why is relevance non-linear in tf?**  
   Repeated occurrences add diminishing returns to relevance.

3. **What is log-frequency weighting?**  
   $\;w_{t,d} = 1 + \log_{10}(tf_{t,d})$, to dampen the impact of very high tf.

4. **Why use log weighting?**  
   Controls the dominance of very frequent terms and highlights rarer, informative ones.

5. **Score computation:**  
   Sum of log-weighted tfs over all query terms present in the document.

6. **Example (“Deep Learning AI”):**  

| Term     | tf in D1 | log-wt D1 | tf in D2 | log-wt D2 |
|----------|----------|-----------|----------|-----------|
| Deep     | 5        | 1.7       | 2        | 1.3       |
| Learning |10        | 2.0       | 4        | 1.6       |
| AI       | 2        | 1.3       | 8        | 1.9       |
→ D1 score = 1.7+2.0+1.3=5.0; D2 = 1.3+1.6+1.9=4.8

---

## 8. Collection & Document Frequency

1. **What is collection frequency (cfₜ)?**  
   Total occurrences of term t across the entire collection.

2. **What is document frequency (dfₜ)?**  
   Number of documents containing term t at least once.

3. **Why are they useful?**  
   To identify rare (informative) vs. common (less informative) terms.

---

## 9. Inverse Document Frequency (IDF)

1. **What is IDF?**  
   $\;idf_t = \log_{10}\bigl(\tfrac{N}{df_t}\bigr)$.

2. **Why use log in IDF?**  
   To moderate extreme weights between very rare and very common terms.

3. **Example (N=1,000,000):**  

| Term      | dfₜ       | idfₜ |
| --------- | --------- | ---- |
| calpurnia | 1         | 6.0  |
| animal    | 100       | 4.0  |
| sunday    | 1,000     | 3.0  |
| fly       | 10,000    | 2.0  |
| the       | 1,000,000 | 0.0  |
4. **Interpretation:**  
   Higher IDF → rarer, more discriminative term.

---

## 10. TF–IDF Term Weighting & Ranking

1. **What is the TF–IDF weight?**  
   $$
     w_{t,d} = (1 + \log_{10} tf_{t,d}) \times \log_{10}\bigl(\tfrac{N}{df_t}\bigr).
   $$

2. **How is document-query score computed?**  
   Sum of TF–IDF weights for all terms in the intersection of query and document.

3. **Example Ranking (“destructive storm” query):**  
   Compute tf, log-wt, idf, then TF–IDF per term per doc, sum to rank D1–D5 → most relevant = highest score.

---

## Multiple-Choice Questions

1. **Which file provides document relevance judgments for TREC?**  
   A. .txt  
   B. .qrel  
   C. .xml  
   D. .csv  
   **Answer:** B

2. **What does a Jaccard score of 0 indicate?**  
   A. Identical sets  
   B. No shared elements  
   C. One set is empty  
   D. Both sets empty  
   **Answer:** B

3. **Which weighting uses \(1 + \log_{10}(tf)\)?**  
   A. Binary  
   B. Raw tf  
   C. Log-frequency  
   D. IDF  
   **Answer:** C

4. **In TF–IDF, a term with dfₜ = N has idfₜ =**  
   A. 1  
   B. 0  
   C. log₁₀(N)  
   D. –∞  
   **Answer:** B

5. **Which campaign emphasizes multilingual IR?**  
   A. TREC  
   B. FIRE  
   C. CLEF  
   D. NTCIR  
   **Answer:** C

6. **Precision@k measures:**  
   A. Recall at rank k  
   B. Precision on top k results  
   C. Average precision over k queries  
   D. P/R balance factor  
   **Answer:** B

7. **Term-document count matrices suffer from:**  
   A. Low dimensionality  
   B. Context preservation  
   C. High sparsity  
   D. Graded relevance  
   **Answer:** C

8. **IDF down-weights a term that appears in:**  
   A. Few documents  
   B. Many documents  
   C. No documents  
   D. Exactly one document  
   **Answer:** B

9. **Log-frequency weighting addresses:**  
   A. Semantic similarity  
   B. Term ordering  
   C. Diminishing returns of tf  
   D. Rare term boosting  
   **Answer:** C

10. **MAP aggregates AP over:**  
    A. Documents  
    B. Queries  
    C. Terms  
    D. Systems  
    **Answer:** B
