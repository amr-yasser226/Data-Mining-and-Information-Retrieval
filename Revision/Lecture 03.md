## 1. Inverted Index & IR “Black Box”

1. **What is the role of the inverted index in IR?**  
   It maps each term to a posting list of document IDs where the term occurs, enabling fast lookup at query time.

2. **In the IR “black box,” what are the inputs and outputs?**  
   - **Inputs:** Query (online) and Document Collection (offline)  
   - **Outputs:** Ranked hits for the query.

3. **What are the three core functions of an IR system?**  
   4. **Representation:** Convert queries and documents into internal forms (e.g., terms, vectors)  
   5. **Indexing:** Build an efficient data structure (inverted index) offline  
   6. **Retrieval Model:** At query time, compare query and document representations via the index to return hits.

---

## 2. Basic Indexing Pipeline

1. **List the steps from raw documents to an inverted index.**  
   2. Preprocessing (tokenization, normalization)  
   3. Term extraction (modified tokens)  
   4. Indexer → build dictionary and posting lists.

5. **Given “Friends, Romans, countrymen,” show the token stream and terms.**  
   - **Tokenization:** [“Friends”, “Romans”, “countrymen”]  
   - **Normalization:** [“friend”, “roman”, “countryman”]

3. **What is stored in the inverted index for each term?**  
   A sorted posting list of docIDs where the term appears (and optionally term frequency, positions, zones).

---

## 3. Why Boolean Matrices Are Inefficient

1. **Why is a full term-document incidence matrix wasteful?**  
   It stores many zeros for absent terms, consuming memory unnecessarily.

2. **Why is Boolean retrieval insufficient for large-scale search?**  
   - No ranking—only exact-match or no-match  
   - Cannot weight or score results, leading to too many or too few hits.

---

## 4. Postings Lists

1. **What is a postings list?**  
   A list of document identifiers (docIDs) for each term, replacing the full incidence row.

2. **Why must postings lists be sorted by docID?**  
   To allow efficient merge-based intersection (AND), union (OR), and difference (NOT) in O(n+m) time.

---

## 5. Constructing an Inverted Index (Example)

1. **Given three docs (“deep learning is powerful”, “machine learning is evolving”, “deep neural networks”), list the final posting lists for each term.**  
   - **deep:** (1,3)  
   - **learning:** (1,2)  
   - **is:** (1,2)  
   - **powerful:** (1)  
   - **machine:** (2)  
   - **evolving:** (2)  
   - **neural:** (3)  
   - **networks:** (3)

---

## 6. Boolean Queries with an Inverted Index

1. **How do you answer “deep AND learning”?**  
   Intersect postings of “deep” (1,3) and “learning” (1,2) → (1).

2. **How do you answer “learning OR neural”?**  
   Union postings of “learning” (1,2) and “neural” (3) → (1,2,3).

3. **How do you answer “NOT learning”?**  
   Complement postings of “learning” (1,2) against the full doc set {1,2,3} → (3).

---

## 7. Inverted Index with Frequencies

1. **What extra information can postings hold beyond docIDs?**  
   - **Term frequency (tf):** count of term occurrences in each document  
   - **Positions:** list of token positions for proximity queries  
   - **Zones:** field or section tags (title, body, etc.)

2. **Why ignore tf for Boolean queries?**  
   Boolean only checks presence/absence, not how many times a term appears.

---

## 8. Query Processing Algorithms

1. **Describe the merge algorithm for `A AND B`.**  
   - Maintain pointers i, j at start of both postings A and B.  
   - If A[i] == B[j], emit it and advance both.  
   - If A[i] < B[j], advance i; else advance j.  
   - Stop when one list is exhausted.

2. **What is the time complexity of AND, OR, and NOT using sorted postings?**  
   O(|p₁| + |p₂|) where |p| is the length of each postings list.

---

## 9. Proximity & Positional Indexes

1. **What is an ordered proximity query?**  
   Finds documents where term1 appears before term2 within k words (e.g., `"artificial intelligence"~5`).

2. **What is an unordered proximity query?**  
   Finds documents where two terms appear within k words in any order (e.g., `#NEAR(5)(deep, learning)`).

3. **How must the postings be augmented for proximity queries?**  
   Include positions of each occurrence in the posting list (positional indexes).

---

## 10. Phrase Queries

1. **How do you answer a phrase query like `"Zewail university"`?**  
   Use the positional index to ensure “Zewail” and “university” occur consecutively (position2 = position1 + 1).

2. **Why are phrase queries popular?**  
   They match users’ implicit expectations and improve precision for multi-word concepts.

---

## 11. Zone Indexes

1. **What is a “zone” in document indexing?**  
   A structural section (title, abstract, body, author) treated separately in the index.

2. **Name two ways to encode zone information in an inverted index.**  
   - **Dictionary-level:** separate posting lists per term per zone  
   - **Posting-level:** tag each docID in the posting with its zone (e.g., `(docID, zone)`).

---

## Multiple-Choice Questions

1. **Why sort postings lists by docID?**  
   A. To compress them more effectively  
   B. To support O(n+m) merge operations  
   C. To compute tf–idf  
   D. To store term frequencies  
   **Answer:** B

2. **What does a posting entry `(5: [3, 17, 42])` represent?**  
   A. Term appears in doc 5 with frequency 3  
   B. Term appears in positions 3, 17, 42 of doc 5  
   C. Doc 5 has 3 to 17 to 42 postings  
   D. Term frequency is 42 in doc 5  
   **Answer:** B

3. **An AND query on two postings lists of lengths 100 and 200 costs approximately:**  
   A. 100×200 operations  
   B. O(100 + 200) operations  
   C. O(max(100,200)²)  
   D. Constant time  
   **Answer:** B

4. **Which extra index information supports phrase queries?**  
   A. Term frequency  
   B. Document frequency  
   C. Token positions  
   D. Stopword markers  
   **Answer:** C

5. **A proximity query `"data mining"~3` returns documents where “data” and “mining” occur within:**  
   A. Exactly 3 characters  
   B. 3 sentences  
   C. 3 words  
   D. 3 documents  
   **Answer:** C

6. **Zone indexes improve retrieval by:**  
   A. Reducing index size  
   B. Distinguishing term occurrences in different fields  
   C. Eliminating stopwords  
   D. Merging synonyms  
   **Answer:** B

7. **The complement operation (NOT) in postings requires knowing:**  
   A. The entire document ID universe  
   B. Term frequencies  
   C. Token positions  
   D. Zone information  
   **Answer:** A

8. **Which structure solves the sparsity of Boolean incidence matrices?**  
   A. Full inverted matrix  
   B. Linked list (postings list)  
   C. Hash table of all zeros  
   D. Dense vector  
   **Answer:** B

9. **Phrase queries are a special case of proximity queries where k equals:**  
   A. 0  
   B. 1  
   C. 2  
   D. The document length  
   **Answer:** B

10. **In the IR pipeline, indexing is performed:**  
    A. At query time  
    B. Offline before any queries  
    C. After retrieval  
    D. During merge operations  
    **Answer:** B
