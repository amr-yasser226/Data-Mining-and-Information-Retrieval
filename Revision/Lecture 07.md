## Information Retrieval Concepts Cheat Sheet

### Table of Contents

1. [Probability Ranking Principle (PRP)](#prp)
2. [Language Models for Ranking](#lms)
3. [Unigram LM: Detailed Example](#unigram-example)
4. [Bigram & Trigram Language Models](#ngram-lms)
5. [Smoothing Techniques](#smoothing)
6. [Multiple-Choice Review Questions](#mcqs)

---

<a name="prp"></a>

## 1. Probability Ranking Principle (PRP)

**Principle:** Documents should be sorted in descending order by their probability of relevance to the user’s query.

$\text{If }P(\mathrm{rel}\mid d_1) > P(\mathrm{rel}\mid d_2) > \cdots, \text{ then rank }d_1, d_2, \dots$\\

**Why use PRP?**

* Provides a formal, probabilistic framework for ranking under uncertainty.
* Guarantees maximum effectiveness under certain assumptions.

**Simple Example:**

| Document | \$P(\mathrm{rel}\mid d)\$ | Rank |
| :------: | :-----------------------: | :--: |
|     A    |            0.80           |   1  |
|     B    |            0.60           |   2  |
|     C    |            0.40           |   3  |

---

<a name="lms"></a>

## 2. Language Models for Ranking

**Approach:**

* Treat each document $d$ as a language model $M_d$.
* Score documents by the likelihood that $M_d$ would generate the query $Q$:

$\text{score}(d) = P(Q \mid M_d).$

**Unigram Assumption:** Words in the query are generated independently:

$P(Q \mid M_d) = \prod_{w \in Q} P(w \mid M_d).$

---

<a name="unigram-example"></a>

## 3. Unigram LM: Detailed Example

**Scenario:**

* Document text: *"data science is powerful"*
* Query: *"data science"*

Term counts in the document (4 words total):

* $\text{count}({\text{data}})=1$
* $\text{count}({\text{science}})=1$

Unigram probabilities:

$$
P(w \mid d) = \frac{\text{count}(w, d)}{|d|} = \frac{1}{4} = 0.25 \quad \text{for each term.}
$$

Score computation:

$$
P(\text{"data science"} \mid d) = 0.25 \times 0.25 = 0.0625.
$$

---

<a name="ngram-lms"></a>

## 4. Bigram & Trigram Language Models

**Bigram LM:**

$$
P(w_1 w_2 \dots w_n \mid d) = P(w_1 \mid d) \prod_{i=2}^n P(w_i \mid w_{i-1}, d).
$$

**Bigram Example:**

* Document: *"deep learning works, deep networks perform"*
* Probability of *"deep networks"*:

$$
P(\text{deep networks} \mid d)
= P(\text{deep} \mid d) \times P(\text{networks} \mid \text{deep}, d)
= \frac{2}{6} \times \frac{1}{6} \approx 0.167.
$$

**Trigram LM:**

$$
P(w_1 w_2 \dots w_n \mid d) = P(w_1 \mid d) \prod_{i=2}^n P(w_i \mid w_{i-2} w_{i-1}, d).
$$

**Trigram Example:**

* Document: *"artificial intelligence systems work"*
* Query: *"artificial intelligence systems"*

Assuming counts give:
$P(\text{artificial})=1/4$,
$P(\text{intelligence}\mid \text{artificial})=1$,
$P(\text{systems}\mid \text{artificial intelligence})=1$:

$$
P(Q \mid d) = \frac{1}{4} \times 1 \times 1 = 0.25.
$$

---

<a name="smoothing"></a>

## 5. Smoothing Techniques

**Motivation:** Without smoothing, any unseen query term in a document assigns a zero probability to the entire query.

**Jelinek–Mercer (Linear) Smoothing:**

$$
P_{\lambda}(w \mid d) = (1 - \lambda) P_{\mathrm{ML}}(w \mid d)
+ \lambda \, P(w \mid \text{collection}).
$$

* $\lambda \in [0,1]$ blends the document model and the background (collection) model.
* **Low** $\lambda$: leans on document evidence (conjunctive behavior).
* **High** $\lambda$: leans on collection statistics (disjunctive behavior).

**Illustrative Example:**

* Documents: d1 (11 words, one "jackson"), d2 (7 words, "michael"=1, "jackson"=1).
* Collection frequencies: total words = 25, $\mathrm{count}(\text{jackson})=2$.
* Query: *"Michael Jackson"*, $\lambda = 1/3$.

$$
P(Q \mid d_1)
= \Bigl[(1-\tfrac{1}{3})\times0 + \tfrac{1}{3}\times\tfrac{2}{25}\Bigr]
\times \Bigl[(1-\tfrac{1}{3})\times\tfrac{1}{11} + \tfrac{1}{3}\times\tfrac{2}{25}\Bigr].
$$

$$
P(Q \mid d_2)
= \Bigl[(1-\tfrac{1}{3})\times\tfrac{1}{7} + \tfrac{1}{3}\times\tfrac{2}{25}\Bigr]
\times \Bigl[(1-\tfrac{1}{3})\times\tfrac{1}{7} + \tfrac{1}{3}\times\tfrac{2}{25}\Bigr].
$$

Ranking: $d_2 > d_1$.

---

<a name="mcqs"></a>

## 6. Multiple-Choice Review Questions

1. **PRP ranks documents by:**

   * A. Decreasing length
   * B. Decreasing probability of relevance
   * C. Increasing tf–idf score
   * D. Random order

   > **Answer:** B

2. **Unigram LM assumes:**

   * A. Word probabilities are independent
   * B. Dependence on the previous word
   * C. Dependence on two previous words
   * D. Document length normalization

   > **Answer:** A

3. **Without smoothing, a query with an unseen term yields:**

   * A. High probability
   * B. Zero probability
   * C. One
   * D. Negative probability

   > **Answer:** B

4. **Bigram probability \$P(w\_i\mid w\_{i-1},d)\$ captures:**

   * A. Document length
   * B. Previous-word dependence
   * C. Term frequency only
   * D. TF–IDF weighting

   > **Answer:** B

5. **Jelinek–Mercer smoothing parameter \$\lambda\$ blends:**

   * A. Document and background LMs
   * B. Unigram and bigram LMs
   * C. TF–IDF and BM25
   * D. RNN and Transformer outputs

   > **Answer:** A

6. **High \$\lambda\$ in JM smoothing makes the model:**

   * A. More conjunctive
   * B. More disjunctive
   * C. Ignore collection stats
   * D. Equivalent to ML estimate

   > **Answer:** B

7. **Trigram LM conditions on:**

   * A. One previous word
   * B. Two previous words
   * C. Three previous words
   * D. No previous words

   > **Answer:** B

8. **In the example “click shears click shears,” which two docs tie?**

   * A. d1 & d2
   * B. d1 & d4
   * C. d2 & d3
   * D. d3 & d4

   > **Answer:** B

9. **Without smoothing, \$P(\text{unseen term}\mid d)=\$**

   * A. \$\tfrac12\$
   * B. \$1\$
   * C. \$0\$
   * D. Undefined

   > **Answer:** C

10. **PRP relies on which probability?**

    * A. \$P(Q\mid d)\$
    * B. \$P(d\mid Q)\$
    * C. \$P(d)\$
    * D. \$P(Q)\$

    > **Answer:** B
