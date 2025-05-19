## 1. Basics and Definitions

1. **What is Information Retrieval (IR)?**  
   Finding material (usually documents) of an unstructured nature (text, images, etc.) that satisfies an information need within large collections.

2. **Why study IR instead of relying solely on databases?**  
   - **Data type:** Databases store structured data with formally defined schemas; IR deals with mostly unstructured free-text plus metadata.  
   - **Queries:** DB uses precise, unambiguous queries (SQL, relational algebra); IR uses free-text or Boolean queries.  
   - **Results:** DB returns exact “correct” answers; IR returns imprecise ranked results whose effectiveness must be measured.  
   - **Interaction:** DB queries are usually one-shot; IR often involves iterative interaction and refinement.

3. **How does IR differ from Natural Language Processing (NLP)?**  
   - **NLP** is about processing and analyzing natural language (tokenization, parsing, sentiment, etc.).  
   - **IR** is specifically about retrieving items that satisfy an information need; it may use NLP techniques, but its goal is ranking and finding relevant documents.

4. **In the broader AI landscape, where does IR sit?**  
   IR intersects with AI, ML/DL, NLP, and databases—it uses machine learning for ranking, NLP for query understanding, but focuses on search and retrieval.

## 2. Why IR Matters

5. **What real-world impact have search engines had, and why is IR pivotal?**  
   Search engines transformed how we access information; IR technology will similarly reshape fields by connecting people to the right content at scale.

6. **Is IR just the “search box” on a website?**  
   No. Modern IR encompasses text classification, expert search, conversational search, recommendations, snippet generation, sponsored search, visualization, and more.

## 3. Common IR Tasks and Features

7. **List six core IR tasks beyond simple keyword matching.**  
   8. Text classification  
   9. Expert (entity) search  
   10. Conversational (dialogue) search  
   11. Recommendation systems  
   12. Snippet selection & summarization  
   13. Query suggestion / correction; plus sponsored search, vertical categorization, information visualization, etc.

14. **What is “snippet selection” on a search results page?**  
   The process of choosing and possibly summarizing a segment of each document to display under each hit, to help users decide which links to click.

## 4. The IR Workflow

9. **What are the three main components of an IR system?**  
   10. **Document collection & representation** (indexing)  
   11. **Query processing** (parsing, expansion, matching)  
   12. **Ranking & retrieval** (scoring, sorting, evaluation)

13. **Define a “document” in IR.**  
    Any retrievable element—web page, email, tweet, image, video, code snippet, product description, etc.—assigned a unique ID within the collection.

14. **What makes a query “expressive” in IR?**  
    Queries are free-text (natural language), Boolean expressions, or more complex forms (fielded, structured, sample document for “find similar,” etc.) reflecting the user’s information need.

## 5. Query and Relevance

12. **What is the difference between an information need and a query?**  
    - **Information need:** The user’s internal topic/context they want to satisfy.  
    - **Query:** The user’s external expression (keywords, Boolean, question) sent to the system.

13. **How is “relevance” defined in IR?**  
    The degree to which a document satisfies the user’s information need—which is inherently subjective, context-dependent, and often judged on a graded scale (perfect, good, fair, etc.).

14. **Why is relevance challenging?**  
    - No formal logical semantics for “meaning”  
    - Ambiguity and polysemy in language (e.g. “Apple,” “Jaguar”)  
    - Subjectivity—different users or tasks may judge relevance differently.

15. **What proxy do IR systems often use for relevance?**  
    *Similarity* between query and document representations (e.g. vector cosine similarity, language model scores).

## 6. Simple Retrieval Methods

16. **Describe the “sequential scan” method.**  
    A brute-force grep-style scan over every document in the collection for query terms. Extremely simple but totally impractical for large collections.

17. **What is the Boolean Retrieval Model?**  
    - Documents are represented as bags of words (or term-document incidence vectors).  
    - Queries are Boolean expressions (AND, OR, NOT).  
    - Returns only those documents that exactly satisfy the Boolean formula (exact-match retrieval).

18. **How do you build a term-document incidence matrix?**  
    Rows correspond to terms, columns to documents; the entry is 1 if the term occurs in the document, else 0. Precomputed before any queries.

19. **Given the following term-document matrix, how would you evaluate**  
    ```
    Query: wink AND drink AND NOT ink
    ```  
    **Answer:**  
    - Retrieve the incidence vectors for “wink” (10001), “drink” (11111), “ink” (00111).  
    - Compute: 10001 ∧ 11111 ∧ ¬(00111) = 10001 ∧ 11000 = 10000 → only document d1.

20. **Where is Boolean retrieval still used?**  
    Email clients, library catalogs, desktop search (Spotlight), many legal and enterprise search systems.

## 7. Efficiency and Scalability

21. **Why can’t we store a full 500K×1M term-document matrix explicitly?**  
    It would be half-a-trillion entries, mostly zeros—too large. Instead, we exploit sparsity (only ~1 billion ones) with inverted indexes.

22. **What two properties must IR systems balance?**  
    - **Effectiveness:** finding the relevant “needle in the haystack.”  
    - **Efficiency:** returning results quickly at web scale (tens of billions of documents, tens of thousands of queries per second, continuous updates).

## 8. Beyond Boolean: Ranking Models

23. **What is the “bag-of-words” representation?**  
    Documents (and queries) are represented as unordered collections (“bags”) of word counts or weights; ignores word order but captures topical content.

24. **Name a basic ranked retrieval model.**  
    - **Vector Space Model (VSM):** represents docs & queries as tf–idf weighted vectors, scores by cosine similarity.  
    - **Probabilistic models:** e.g., BM25, language models.

25. **How do you evaluate search engine performance?**  
    Common metrics include precision, recall, F-measure, average precision (AP), mean average precision (MAP), discounted cumulative gain (DCG), and user-oriented measures (click-through rate, satisfaction surveys).

## 9. Advanced & Modern IR

26. **What role do ML/DL methods play in IR?**  
    - Learning‐to‐rank (LTR) models to combine features for ranking.  
    - Neural retrieval (dense vector representations, transformers).  
    - Query understanding (BERT for query expansion), snippet generation.

27. **Give two examples of conversational IR.**  
    - Voice assistants (Siri, Alexa) answering follow-up questions.  
    - Chatbot interfaces that refine search via dialogue.

28. **What is expert search?**  
    Retrieving people (experts) rather than documents, given a topic or question.

29. **How does recommendation relate to IR?**  
    Recommendations “retrieve” items (products, movies) based on user’s interests/history; uses collaborative and content‐based filtering.

30. **What’s “information visualization” in IR?**  
    Graphical representations (e.g., cluster maps, timelines) to help users navigate large result sets or data collections.

---

## Multiple Choice Questions

1. **Which of the following most accurately defines Information Retrieval (IR)?**  
   A. Storing and managing structured data in relational tables  
   B. Finding unstructured materials (e.g., text) that satisfy an information need within large collections  
   C. Translating from one natural language to another  
   D. Classifying images into predefined categories  
   **Answer:** B

2. **Which query language is typical of database systems (not of IR)?**  
   A. Free-text natural language  
   B. Boolean expressions  
   C. SQL  
   D. Keyword search  
   **Answer:** C

3. **In IR, “relevance” is best described as:**  
   A. Whether a document exactly matches the Boolean query  
   B. The similarity between a document and the user’s information need  
   C. The number of times a term appears in a document  
   D. The document’s length relative to the query  
   **Answer:** B

4. **Which of these is NOT a core component of a basic IR system?**  
   A. Query processing  
   B. Document representation/indexing  
   C. Transaction rollback  
   D. Ranking and retrieval  
   **Answer:** C

5. **A “sequential scan” IR method is:**  
   A. Building an inverted index for fast lookup  
   B. Grep-style scan of every document at query time  
   C. Using BERT to encode queries and documents  
   D. Partitioning the collection by topic  
   **Answer:** B

6. **In the Boolean Retrieval Model, documents are represented as:**  
   A. TF–IDF weighted vectors  
   B. Dense neural embeddings  
   C. Bags of words (term-document incidence vectors)  
   D. Markov chains  
   **Answer:** C

7. **Which of these queries would retrieve documents containing “wink” and “drink” but not “ink”?**  
   A. wink OR drink AND NOT ink  
   B. wink AND drink AND NOT ink  
   C. (wink OR drink) AND ink  
   D. wink XOR drink  
   **Answer:** B

8. **Why can’t we store a full 500K×1M term-document matrix explicitly?**  
   A. It would require a relational schema  
   B. It is mostly zeros and far too large to store efficiently  
   C. Boolean retrieval doesn’t use matrices  
   D. Natural language is too ambiguous  
   **Answer:** B

9. **Which metric measures the proportion of retrieved documents that are relevant?**  
   A. Recall  
   B. Precision  
   C. MAP (Mean Average Precision)  
   D. DCG (Discounted Cumulative Gain)  
   **Answer:** B

10. **Which of the following is an example of an advanced IR task?**  
    A. Simple Boolean keyword matching  
    B. Expert search (finding people experts on a topic)  
    C. Storing tweets in a database  
    D. Serializing documents to XML  
    **Answer:** B

11. **A “bag-of-words” representation:**  
    A. Preserves word order exactly  
    B. Discards word order but retains frequency information  
    C. Maps words to topics using LDA  
    D. Embeds words in a continuous vector space  
    **Answer:** B

12. **Which statement is true about IR vs. NLP?**  
    A. IR always uses deep learning; NLP never does  
    B. NLP focuses on processing language; IR focuses on retrieving relevant items  
    C. IR systems only handle images; NLP only handles text  
    D. They are the same field with different names  
    **Answer:** B

13. **In modern IR, “learning-to-rank” models are used to:**  
    A. Build Boolean indexes  
    B. Automatically generate SQL queries  
    C. Combine multiple features to produce better ranking  
    D. Translate queries into multiple languages  
    **Answer:** C

14. **Which of these is NOT typically evaluated using IR effectiveness metrics?**  
    A. Precision  
    B. Recall  
    C. Latency  
    D. Mean Average Precision (MAP)  
    **Answer:** C

15. **Which IR component continually ingests new documents to keep the index up to date?**  
    A. Query processor  
    B. Indexer  
    C. Ranker  
    D. User interface  
    **Answer:** B
