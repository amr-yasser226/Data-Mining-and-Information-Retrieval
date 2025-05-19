## 1. Probability Ranking Principle (PRP)

1. **What does the Probability Ranking Principle state?**  
   Rank documents in decreasing order of their probability of relevance to the user’s query:  
$$
     P(\text{rel} \mid d_1) > P(\text{rel} \mid d_2) > \cdots
$$

2. **Why is probability theory useful in IR?**  
   It provides a principled way to manage uncertainty and decide which documents are most likely relevant.

3. **Example:**  
   Query: “machine learning basics”  
   - Document A: $0.8$  
   - Document B: $0.6$  
   - Document C: $0.4$  
   Ranking: A > B > C

---

## 2. Language Models in IR

1. **How is a Language Model (LM) used for ranking?**  
   Treat each document $d$ as its own LM $M_d$ and rank by $P(Q \mid M_d)$, the probability that $M_d$ generates the query $Q$.

2. **What is a unigram LM?**  
   A model where each word is generated independently with probability estimated from term frequency:
$$
     P(Q \mid M_d) = \prod_{w \in Q} P(w \mid M_d)
$$

3. **Compute $P(Q \mid M_d)$ for “data science” in “data science is powerful”:**  
   Each term count = 1 of 4 words → $P(w\mid d)=\tfrac14$.  
$$   P(\text{“data science”}\mid d)=\tfrac14\times\tfrac14=0.0625
$$

---

## 3. Example: Unigram LM Ranking

Documents:
1. “click go the shears boys click click click”  
2. “click click”  
3. “metal here”  
4. “metal shears click here”  

Query: “click shears click shears”

| d   | P(click\|$d$) | P(shears\|$d$) | P(Q\|$d$)                 |
| --- | ------------- | -------------- | ------------------------- |
| d1  | 4/8 = 0.5     | 1/8 = 0.125    | $0.5^2\cdot0.125^2=0.004$ |
| d2  | 2/2 = 1.0     | 0              | 0                         |
| d3  | 0             | 0              | 0                         |
| d4  | 1/4 = 0.25    | 1/4 = 0.25     | $0.25^4=0.004$            |

Ranking: d1 = d4 > d2 = d3

---

## 4. Bigram & Trigram LMs

1. **Bigram LM:**  
$$
     P(w_1w_2w_3\mid d)=P(w_1\mid d)\prod_{i=2}^3P(w_i\mid w_{i-1},d)
$$  
   Example: Document “deep learning works, deep networks perform”  
$$
     P(\text{“deep networks”}\mid d)
     =P(\text{deep}\mid d)\,
     P(\text{networks}\mid \text{deep},d)= $$$$\tfrac26\times\tfrac16=0.167
$$

2. **Trigram LM:**  
$$
     P(w_1w_2w_3\mid d)
     =P(w_1\mid d)\,P(w_2\mid w_1,d)\,P(w_3\mid w_1w_2,d)
$$  
   Example: “artificial intelligence systems work” → query “artificial intelligence systems”  
$$
     P(Q\mid d)=\tfrac14\times1\times1=0.25
$$

---

## 5. Smoothing

1. **Why smooth?**  
   To assign non-zero probability to unseen terms and avoid zeroing out $P(Q\mid d)$.

2. **Jelinek–Mercer smoothing:**  
$$
     P_{\lambda}(w\mid d)
     =(1-\lambda)P_{\mathrm{ML}}(w\mid d)
     +\lambda\,P(w\mid\text{collection})
$$

3. **Effect of $\lambda$:**  
   - Low $\lambda$: conjunctive-like (favor documents containing all query terms)  
   - High $\lambda$: disjunctive-like (suitable for long queries)

4. **Example:**  
   Documents:  
   - d1: “Jackson … entertainers …” (11 words, “jackson” count=1)  
   - d2: “Michael Jackson anointed himself King of Pop” (7 words, “michael”=1, “jackson”=1)  
   Query: “Michael Jackson”, $\lambda=1/3$  
$$
     P(Q\mid d1)
     =\bigl[\tfrac23\times0+\tfrac13\times\tfrac1{18}\bigr]
      \times\bigl[\tfrac23\times\tfrac1{11}+\tfrac13\times\tfrac2{18}\bigr]
$$  
$$
     P(Q\mid d2)
     =\bigl[\tfrac23\times\tfrac1{7}+\tfrac13\times\tfrac1{18}\bigr]
      \times\bigl[\tfrac23\times\tfrac1{7}+\tfrac23\times\tfrac2{18}\bigr]
$$  
   Ranking: d2 > d1

---

## Multiple-Choice Questions

1. **PRP ranks documents by:**  
   A. Decreasing length  
   B. Decreasing probability of relevance  
   C. Increasing tf–idf score  
   D. Random order  
   **Answer:** B

2. **Unigram LM assumes:**  
   A. Word probabilities independent  
   B. Dependence on previous word  
   C. Dependence on two previous words  
   D. Document length normalization  
   **Answer:** A

3. **Without smoothing, a query with an unseen term yields:**  
   A. High probability  
   B. Zero probability  
   C. One  
   D. Negative probability  
   **Answer:** B

4. **Bigram probability $P(w_i\mid w_{i-1},d)$ captures:**  
   A. Document length  
   B. Previous-word dependence  
   C. Term frequency only  
   D. TF–IDF weighting  
   **Answer:** B

5. **Jelinek–Mercer smoothing parameter $\lambda$ blends:**  
   A. Document and background LMs  
   B. Unigram and bigram LMs  
   C. TF–IDF and BM25  
   D. RNN and Transformer outputs  
   **Answer:** A

6. **High $\lambda$ in JM smoothing makes the model:**  
   A. More conjunctive  
   B. More disjunctive  
   C. Ignore collection stats  
   D. Equivalent to ML estimate  
   **Answer:** B

7. **Trigram LM conditions on:**  
   A. One previous word  
   B. Two previous words  
   C. Three previous words  
   D. No previous words  
   **Answer:** B

8. **In the example “click shears click shears,” which docs tie in score?**  
   A. d1 & d2  
   B. d1 & d4  
   C. d2 & d3  
   D. d3 & d4  
   **Answer:** B

9. **Without smoothing, $P(\text{unseen term}\mid d)=$**  
   A. $\tfrac12$  
   B. 1  
   C. 0  
   D. undefined  
   **Answer:** C

10. **PRP relies on which probability?**  
    A. $P(Q\mid d)$  
    B. $P(d\mid Q)$  
    C. $P(d)$  
    D. $P(Q)$  
    **Answer:** B
