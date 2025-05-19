## 1. Evaluation Strategies

1. **What are the two main types of evaluation strategies in IR?**  
   - **System-centered studies:** laboratory experiments using fixed documents, queries, and relevance judgments (qrels), comparing system variants without real users.  
   - **User-centered studies:** involve real users performing tasks on two or more systems, measuring which system better satisfies users.

2. **When would you choose a system-centered study?**  
   When you have a test collection (documents + queries + qrels) and want controlled comparisons of algorithms.

3. **When would you choose a user-centered study?**  
   When you want to measure real-world usability, satisfaction, and task success with actual users.

---

## 2. Evaluation Criteria

1. **What are the three high-level evaluation criteria for search engines?**  
   2. **Effectiveness:** quality of retrieved documents (precision, recall, etc.)  
   3. **Efficiency:** response time (latency), indexing time  
   4. **Usability:** learnability, flexibility, satisfaction for novice vs. expert users

---

## 3. Cranfield Paradigm

1. **What are the components of the Cranfield paradigm?**  
   - **Document collection**  
   - **Query set** (information needs/topics)  
   - **Relevance judgments** (qrels)  
   - **IR system** + **evaluation module** that measures system output against qrels

2. **Why is the Cranfield paradigm important?**  
   It provides a standardized framework for offline, repeatable evaluation of IR effectiveness.

---

## 4. Set-Based Measures (Boolean-style)

1. **When are set-based measures appropriate?**  
   For systems that return an unranked set of results (e.g., Boolean search).

2. **Define precision.**  
   Fraction of retrieved documents that are relevant:  
   $$
     \text{Precision} = \frac{|\{\text{relevant} \}\cap \{\text{retrieved}\}|}{|\{\text{retrieved}\}|}
   $$

3. **Define recall.**  
   Fraction of relevant documents that were retrieved:  
   $$
     \text{Recall} = \frac{|\{\text{relevant}\}\cap \{\text{retrieved}\}|}{|\{\text{relevant in collection}\}|}
   $$

4. **What trade-off exists between precision and recall?**  
   Retrieving more documents tends to increase recall but may lower precision; retrieving fewer increases precision but may miss relevant items.

---

## 5. F-Measure

1. **What is the F-measure?**  
   The harmonic mean of precision and recall with parameter β:  
   $$
     F_\beta = (1 + \beta^2)\,\frac{P\,R}{\beta^2 P + R}
   $$
   - **β=1** yields F₁, equal weight to P and R.  
   - **β>1** emphasizes recall; **β<1** emphasizes precision.

2. **Why use the harmonic mean rather than the arithmetic mean?**  
   Because it penalizes extreme values (a very low P or R) more heavily, reflecting that both must be high for good performance.

---

## 6. Ranked-Based Measures

1. **Why do we need rank-based measures?**  
   Two systems with identical P, R, and F can order relevant documents differently; ranked measures account for position.

2. **What is Precision@k?**  
   Precision computed at a fixed cutoff k (first k results):  
   $$
     P@k = \frac{\#\text{relevant docs in top }k}{k}
   $$

---

## 7. Average Precision (AP) & Mean Average Precision (MAP)

1. **What is Average Precision (AP)?**  
   The average of P@k computed at each rank k where a relevant document appears.  

2. **How do you compute MAP?**  
   The mean of AP scores over all queries:  
   $$
     \text{MAP} = \frac{1}{Q}\sum_{q=1}^Q AP(q)
   $$

3. **Why is AP a user-oriented measure?**  
   It models the user stopping at each relevant document and averages precision at those points.

---

## 8. Discounted Cumulative Gain (DCG) & nDCG

1. **Why use graded relevance instead of binary?**  
   Because some relevant documents are more useful than others (e.g., “perfect” vs. “good”).

2. **What is DCG@k?**  
   Cumulative gain of the ranked list up to position k, discounting lower ranks by log₂:  
   $$
     DCG@k = \sum_{i=1}^k \frac{G_i}{\log_2(i+1)}
   $$
   where \($G_i$\) is the graded relevance at rank i.

3. **What is nDCG@k?**  
   Normalized DCG:  
   $$
     nDCG@k = \frac{DCG@k}{IDCG@k}
	$$ 
   where IDCG@k is the DCG of the ideal (best-possible) ranking. Ensures 0 ≤ nDCG ≤ 1.

---

## 9. Sample Calculation Questions

1. **Q1/Q2 Precision, Recall, F₀.₅, P@10, P@Recall=50%**  
   - Q1: relevant at ranks [5,7,9,10,22], 6 total relevant in collection  
   - Q2: relevant at ranks [1,2,50], 4 total relevant  
   - Calculate P, R, F₀.₅, P@10, and precision when R=0.5.

2. **MAP calculation for Q1/Q2 as above.**  

3. **nDCG for a single query with graded relevance**  
   - Relevance grades: P=100, E=10, G=1, N=0  
   - Retrieved sequence: G E N P N G N N G N  
   - Compute DCG@10, IDCG@10, then nDCG@10.

---

## Multiple-Choice Questions

1. **Which study type uses fixed qrels and no real users?**  
   A. User-centered study  
   B. System-centered study  
   C. A/B testing  
   D. Live experiment  
   **Answer:** B

2. **Which metric balances precision and recall with equal weight?**  
   A. P@k  
   B. MAP  
   C. F₁  
   D. nDCG  
   **Answer:** C

3. **What does P@5 measure?**  
   A. Precision at rank 5 (first 5 docs)  
   B. Precision when recall=0.5  
   C. Proportion of relevant in top 50%  
   D. Precision averaged over 5 queries  
   **Answer:** A

4. **Which measure accounts for graded relevance and position?**  
   A. Recall  
   B. AP  
   C. DCG  
   D. F₀.₅  
   **Answer:** C

5. **nDCG is always ≤ 1 because it is:**  
   A. A harmonic mean  
   B. Normalized by ideal DCG  
   C. Discounted logarithmically  
   D. Averaged over queries  
   **Answer:** B

6. **Which evaluation criterion measures query latency?**  
   A. Effectiveness  
   B. Efficiency  
   C. Usability  
   D. Precision  
   **Answer:** B

7. **In MAP, AP is computed per:**  
   A. Document  
   B. Ranking position  
   C. Query  
   D. System variant  
   **Answer:** C

8. **A user-centered study primarily assesses:**  
   A. Precision/recall on qrels  
   B. Algorithmic runtime  
   C. Learnability and satisfaction  
   D. Index size  
   **Answer:** C

9. **IDCG@k is:**  
   A. The discount factor for DCG  
   B. DCG of the best possible ranking up to k  
   C. Inverse DCG  
   D. DCG normalized by k  
   **Answer:** B

10. **Which trade-off is fundamental in IR evaluation?**  
    A. Speed vs. memory  
    B. Precision vs. recall  
    C. Index size vs. throughput  
    D. Usability vs. effectiveness  
    **Answer:** B
