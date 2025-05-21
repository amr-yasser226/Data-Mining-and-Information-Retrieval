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

## 7. Rocchio Algorithm

1. **What does Rocchio aim to do?**  
   Shift the query vector toward relevant documents and away from non-relevant ones in VSM.

2. **Write the Rocchio formula.**  
$$\vec{q}_{\text{new}} = \alpha\vec{q}_0 + \beta\frac{1}{|D_r|}\sum_{d\in D_r}\vec{d}$$
$$\gamma\frac{1}{|D_{nr}|}\sum_{d\in D_{nr}}\vec{d}$$

4. **What roles do $\alpha,\beta,\gamma$ play?**  
   Weights for original query, positive feedback, negative feedback.

5. **Why might weights go negative?**  
   If $\gamma$ is large, subtraction can yield negative term weights (then clamped to zero).

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

## Multiple-Choice Questions

1. **Which QE method uses WordNet?**  
   A. Query logs  
   B. Thesaurus-based  
   C. Relevance feedback  
   D. PRF  
   **Answer:** B

2. **Dice’s coefficient of 1 indicates:**  
   A. No overlap  
   B. Perfect overlap  
   C. Independent terms  
   D. Rare terms  
   **Answer:** B

3. **In Rocchio, increasing $\gamma$ does what?**  
   A. Emphasizes original query  
   B. Emphasizes relevant docs  
   C. Emphasizes non-relevant docs  
   D. Removes synonyms  
   **Answer:** C

4. **PRF assumes which documents are relevant?**  
   A. User-labeled ones  
   B. Bottom-k ranked  
   C. Top-k ranked  
   D. Random sample  
   **Answer:** C

5. **Implicit feedback includes all EXCEPT:**  
   A. Clicks  
   B. Relevance labels  
   C. Time spent  
   D. Scroll depth  
   **Answer:** B

6. **Mutual Information (MI) is zero if terms are:**  
   A. Perfectly correlated  
   B. Independent  
   C. Rare  
   D. Frequent  
   **Answer:** B

7. **Query drift is caused by:**  
   A. Too many synonyms  
   B. Poor expansion terms  
   C. Long documents  
   D. Low IDF  
   **Answer:** B

8. **A context vector in expansion is:**  
   A. A document field  
   B. A virtual doc of co-occurring terms  
   C. A vector of user preferences  
   D. A stopword list  
   **Answer:** B

9. **Which expansion is domain-specific by design?**  
   A. WordNet  
   B. Automatic thesaurus  
   C. Query logs  
   D. Medical thesaurus  
   **Answer:** D

10. **Relevance feedback iteration is usually:**  
    A. Unbounded  
    B. Only once or twice  
    C. Never repeated  
    D. Done per document  
    **Answer:** B
