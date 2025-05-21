## 1. Why Query Expansion

1. **What problem does query expansion address?**  
   Queries often fail to fully express the user’s true information need, leading to poor precision or recall.

2. **Give an example of an ambiguous query.**  
   “apple” could refer to the fruit or the tech company.

3. **What is query expansion?**  
   Adding related, synonymous, or conceptually similar terms to the original query to improve retrieval.

4. **How can expansion improve both precision and recall?**  
   By capturing more relevant documents (recall) and reducing ambiguity (precision).

---

## 2. Types of Query Expansion

1. **What are three main methods for query expansion?**  
   2. Thesaurus-based methods  
   3. Query logs  
   4. Relevance feedback

5. **Define synonym expansion.**  
   Replacing or augmenting a term with its synonyms (e.g., “car” → “automobile”).

6. **Define related-term expansion.**  
   Adding co-occurring or semantically related words (e.g., “heart attack” → “myocardial infarction”).

7. **Define conceptual expansion.**  
   Adding terms that describe the same concept at different levels (e.g., “AI” → “artificial intelligence,” “machine learning”).

---

## 3. Thesaurus-Based Methods

1. **What is a manually built thesaurus?**  
   A curated dictionary (e.g., WordNet) that groups words into synsets and defines relations.

2. **List four relationships WordNet provides.**  
   Synonyms, hypernyms (broader), hyponyms (narrower), meronyms (parts), holonyms (wholes).

3. **Pros and cons of using WordNet?**  
   - Pros: High-quality, interpretable, language-agnostic.  
   - Cons: Limited coverage, manual maintenance, may miss domain jargon.

4. **What is an automatic thesaurus?**  
   A collection of term associations learned from co-occurrence patterns in large corpora.

5. **Name two techniques for building an automatic thesaurus.**  
   a) Term vectors + similarity (e.g., cosine)  
   b) Term association measures (e.g., Dice, Mutual Information)

---

## 4. Automatic Thesaurus Techniques

1. **How do term vectors produce expansions?**  
   Represent each word by its co-occurrence vector; find top-k nearest neighbors by cosine similarity.

2. **What is Dice’s coefficient?**  
   $\displaystyle\frac{2|A\cap B|}{|A|+|B|}$, measuring overlap between document sets A and B.

3. **What is Pointwise Mutual Information (PMI)?**  
   $\displaystyle\log\frac{P(A,B)}{P(A)P(B)}$, quantifying how much co-occurrence exceeds chance.

4. **Give an example Dice computation.**  
   “heart attack” in 500 docs, “cardiac arrest” in 400, co-occur in 100 → Dice = $2×100/(500+400)=0.222$.

---

## 5. Query Logs

1. **How are query logs used for expansion?**  
   Mining prior user queries to find frequently co-searched terms or reformulations.

2. **Pros and cons of query-log expansion?**  
   - Pros: Reflects real user behavior, up-to-date  
   - Cons: Requires large logs, may amplify popular but irrelevant patterns

---

## 6. Relevance Feedback

1. **What is explicit relevance feedback?**  
   Users mark retrieved documents as relevant/non-relevant; the system refines the query accordingly.

2. **Outline the relevance feedback process.**  
   3. Issue initial query  
   4. Retrieve results  
   5. User marks relevant/non-relevant  
   6. System refines query (e.g., Rocchio)  
   7. Retrieve improved results (repeat as needed)

8. **Pros and cons of explicit feedback?**  
   - Pros: Tailored to user’s intent  
   - Cons: User effort required, possible overfitting

---

### 7. Rocchio Algorithm

#### 1. What does Rocchio aim to do?  
Shift the query vector toward relevant documents and away from non-relevant ones in a Vector Space Model (VSM).

---

#### 2. Rocchio’s Relevance-Feedback Formula

**Given**  
- Original query vector: $\displaystyle \vec{q}_0$  
- Relevant document set: $D_r$  
- Non-relevant document set: $D_{nr}$  
- Weighting parameters: $\alpha, \beta, \gamma$

**Compute**  
<p align="center">
  <strong>q<sub>new</sub> =</strong>
  &alpha; &middot; q<sub>0</sub>
  + &beta; &middot; (1 / |D<sub>r</sub>|) &sum;<sub>d∈D<sub>r</sub></sub> d
  &minus; &gamma; &middot; (1 / |D<sub>nr</sub>|) &sum;<sub>d∈D<sub>nr</sub></sub> d
</p>

---

#### 3. Explanation of Terms

- **$\alpha\,\vec{q}_0$**  
  Retains a fraction $\alpha$ of the original query.

- **$\beta\,\dfrac{1}{|D_r|}\sum_{d\in D_r}\vec{d}$**  
  Adds the centroid of relevant documents, scaled by $\beta$.

- **$\gamma\,\dfrac{1}{|D_{nr}|}\sum_{d\in D_{nr}}\vec{d}$**  
  Subtracts the centroid of non-relevant documents, scaled by $\gamma$.

---

#### 4. Roles of $\alpha, \beta, \gamma$

- **$\alpha$**: Weight of the original query  
- **$\beta$**: Weight of positive (relevant) feedback  
- **$\gamma$**: Weight of negative (non-relevant) feedback  

---

#### 5. Why Might Vector Components Go Negative?

If $\gamma$ (or $\beta$) is large, the subtraction (or addition) term can dominate, potentially producing negative components in $\vec{q}_\text{new}$. In practice, these negative values are often clamped to zero.


---

## 8. Pseudo (Blind) Relevance Feedback

1. **What is Pseudo-Relevance Feedback (PRF)?**  
   Assume top-k retrieved documents are relevant without user input, then apply feedback algorithm automatically.

2. **Pros and cons of PRF?**  
   - Pros: Unsupervised, scalable  
   - Cons: Can introduce query drift if initial results are poor

---

## 9. Implicit Feedback

1. **What is implicit feedback?**  
   Signals inferred from user behavior (clicks, dwell time, scrolling) rather than explicit labels.

2. **List five forms of implicit feedback.**  
   Clicks, time spent, scrolling depth, mouse movements, query refinements.

3. **Why might implicit feedback be preferable?**  
   Continuous, low user effort, language-independent.

---

## 10. Additional Notes on Setting Weights & Feedback Effects

1. **How should β and γ be set relative to α when many judged documents are available?**  
   Set β and γ high compared to α to give more influence to feedback when you have ample relevance judgments.

2. **Why is positive feedback usually more valuable than negative feedback?**  
   Positive feedback helps reinforce genuinely relevant terms, so systems typically use β > γ; some even set γ = 0 and rely solely on positive judgments.

3. **What happens when γ > 0 in the Rocchio formula?**  
   Negative components can appear in the updated query vector; in practice, any negative term weights are clamped to zero (ignored).

4. **How does relevance feedback affect recall and precision?**  
   It can boost both metrics, but it’s especially effective at improving recall when finding more relevant documents is critical; one round often yields large gains, while further rounds offer diminishing returns.

5. **What are the main challenges of explicit relevance feedback?**  
   1. **Long Queries:** Increases retrieval cost and slows response.  
   2. **User Effort:** Users may resist providing explicit judgments.  
   3. **Interpretability:** Results can become harder to explain after feedback.

6. **What unsupervised alternatives exist to explicit feedback?**  
   1. **Pseudo-Relevance Feedback (PRF):** Automatically assumes the top-k results are relevant to refine the query.  
   2. **Implicit Feedback:** Leverages user interaction (clicks, dwell time, scrolling) to infer relevance without manual labels.

---


## Multiple-Choice Questions

### Question 1:

Which QE method uses WordNet?

 A. Query logs  
 B. Thesaurus-based  
 C. Relevance feedback  
 D. PRF

<details> <summary>Answer</summary> B. Thesaurus-based. WordNet is a manually curated thesaurus used for expansion. </details>

---

### Question 2:

Dice’s coefficient of 1 indicates:

 A. No overlap  
 B. Perfect overlap  
 C. Independent terms  
 D. Rare terms

<details> <summary>Answer</summary> B. Perfect overlap. A Dice score of 1 means the two term sets are identical. </details>

---

### Question 3:

In Rocchio, increasing γ does what?

 A. Emphasizes original query  
 B. Emphasizes relevant docs  
 C. Emphasizes non-relevant docs  
 D. Removes synonyms

<details> <summary>Answer</summary> C. Emphasizes non-relevant docs. A larger γ increases the subtraction of non-relevant document centroids. </details>

---

### Question 4:

PRF assumes which documents are relevant?

 A. User-labeled ones  
 B. Bottom-k ranked  
 C. Top-k ranked  
 D. Random sample

<details> <summary>Answer</summary> C. Top-k ranked. Pseudo-Relevance Feedback treats the top-k results as relevant. </details>

---

### Question 5:

Implicit feedback includes all EXCEPT:

 A. Clicks  
 B. Relevance labels  
 C. Time spent  
 D. Scroll depth

<details> <summary>Answer</summary> B. Relevance labels. That is explicit feedback, not implicit. </details>

---

### Question 6:

Mutual Information (MI) is zero if terms are:

 A. Perfectly correlated  
 B. Independent  
 C. Rare  
 D. Frequent

<details> <summary>Answer</summary> B. Independent. MI measures deviation from independence; zero means no association. </details>

---

### Question 7:

Query drift is caused by:

 A. Too many synonyms  
 B. Poor expansion terms  
 C. Long documents  
 D. Low IDF

<details> <summary>Answer</summary> B. Poor expansion terms. Irrelevant terms in the expanded query can steer results off-topic. </details>

---

### Question 8:

A context vector in expansion is:

 A. A document field  
 B. A virtual doc of co-occurring terms  
 C. A vector of user preferences  
 D. A stopword list

<details> <summary>Answer</summary> B. A virtual doc of co-occurring terms. It aggregates term contexts for expansion. </details>

---

### Question 9:

Which expansion is domain-specific by design?

 A. WordNet  
 B. Automatic thesaurus  
 C. Query logs  
 D. Medical thesaurus

<details> <summary>Answer</summary> D. Medical thesaurus. Domain-specific thesauri target specialized vocabularies. </details>

---

### Question 10:

Relevance feedback iteration is usually:

 A. Unbounded  
 B. Only once or twice  
 C. Never repeated  
 D. Done per document

<details> <summary>Answer</summary> B. Only once or twice. Empirically, one round yields large gains and additional rounds offer marginal benefit. </details>

---
