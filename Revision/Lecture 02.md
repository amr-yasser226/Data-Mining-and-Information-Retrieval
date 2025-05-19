## 1. Boolean Retrieval & Term-Document Incidence Matrix

1. **What is a term-document incidence matrix?**  
   A binary matrix where rows are terms, columns are documents, and each entry is 1 if the term appears in the document, 0 otherwise.

2. **Given documents d1–d5, how do you compute the incidence vector for “wink”?**  
   Check each document for “wink”: d1=1, d2=0, d3=0, d4=0, d5=1 → [1, 0, 0, 0, 1].

3. **How do you evaluate the Boolean query `wink AND drink AND NOT ink` using incidence vectors?**  
   Compute the logical AND of the “wink” and “drink” vectors, then AND with the negation of the “ink” vector:  
   `10001 ∧ 11111 ∧ ¬(00111) = 10000` → only d1.

4. **Why is pure sequential scan impractical at web scale?**  
   Because it must scan every document for each query, which is too slow for millions or billions of documents.

5. **Where are Boolean retrieval systems still commonly used?**  
   Email search, library catalogs, desktop search (Spotlight), legal and enterprise search.

---

## 2. Preprocessing Pipeline Overview

1. **What are the three main preprocessing steps before indexing?**  
   2. Tokenization  
   3. Stopword removal (Stopping)  
   4. Normalization (case folding, stemming/lemmatization, etc.)

5. **What is the purpose of preprocessing in IR?**  
   To convert raw text into a canonical set of terms that improve matching between queries and documents and reduce index size.

---

## 3. Encoding & Parsing

1. **Why detect and standardize text encoding before other preprocessing?**  
   To ensure characters are correctly interpreted (e.g., avoid “Ã©” instead of “é”) and to normalize all documents to a common encoding (UTF-8).

2. **Name four document formats and corresponding parsing libraries in Python.**  
   - PDF: PyMuPDF (fitz) or pdfplumber  
   - Word (.docx): python-docx  
   - HTML: BeautifulSoup  
   - Excel (.xlsx/.csv): pandas

---

## 4. Tokenization

1. **What is tokenization?**  
   Splitting text into smaller units (“tokens”), typically words or sentences.

2. **Give the tokens for “Friends, Romans and Countrymen.”**  
   [“Friends”, “Romans”, “and”, “Countrymen”]

3. **List three tokenization challenges.**  
   - Apostrophes and possessives (e.g., Egypt’s)  
   - Hyphenation (e.g., state-of-the-art)  
   - URLs and hashtags (e.g., `http://…`, `#BlackLivesMatter`)

4. **How do languages without spaces (e.g., Chinese) handle tokenization?**  
   They require segmentation algorithms to detect word boundaries.

---

## 5. Stopword Removal (Stopping)

1. **What are stopwords?**  
   Very common words (e.g., “the”, “is”, “and”) that carry little semantic weight.

2. **Why might you retain stopwords in some applications?**  
   - Phrase queries where stopwords are meaningful (“to be or not to be”)  
   - When compression and query optimization reduce the cost of including them

3. **Give the result after removing stopwords from “The cat is sitting on the mat.”**  
   [“cat”, “sitting”, “mat”]

---

## 6. Normalization

1. **What is case folding?**  
   Converting all letters to lowercase so that “Car” and “car” match.

2. **What are thesauri used for in IR preprocessing?**  
   Query or index expansion via synonyms, antonyms, and hierarchical relationships.

3. **Describe the Soundex algorithm’s goal.**  
   To encode words by pronunciation so that similarly sounding words (e.g., “Smith” and “Smyth”) share the same code.

4. **What is lemmatization?**  
   Reducing words to their dictionary form (lemma) using part-of-speech and vocabulary (e.g., “saw” → “see”).

5. **How does stemming differ from lemmatization?**  
   Stemming applies simple rules to chop affixes, producing non-dictionary stems (e.g., “running” → “run” or “runn”), whereas lemmatization yields valid lemmas.

6. **What is the Porter Stemmer?**  
   A rule-based stemming algorithm that strips common English suffixes in multiple steps to produce stems.

---

## 7. End-to-End Preprocessing Example

1. **List the preprocessing steps applied to the sentence “The researchers are studying advanced techniques for processing textual data.”**  
   2. Tokenization → [“The”, “researchers”, “are”, …]  
   3. Lowercasing → [“the”, “researchers”, …]  
   4. Stopword removal → [“researchers”, “studying”, …]  
   5. Lemmatization → [“researcher”, “study”, …]  
   6. (Optional) Stemming → [“research”, “studi”, …]

---

## Multiple-Choice Questions

1. **Which step ensures “é” is not misinterpreted as “Ã©”?**  
   A. Tokenization  
   B. Encoding detection and standardization  
   C. Stopword removal  
   D. Lemmatization  
   **Answer:** B

2. **In tokenization, “Hewlett-Packard” is best handled by:**  
   A. Splitting on hyphens → [“Hewlett”, “Packard”]  
   B. Keeping as one token → [“Hewlett-Packard”]  
   C. Removing the hyphen → [“HewlettPackard”]  
   D. Discarding the term entirely  
   **Answer:** A

3. **A stopword list removal might wrongly remove “not” in sentiment analysis. Why?**  
   A. “not” is rare  
   B. It carries sentiment polarity  
   C. It appears at document boundaries  
   D. It is an acronym  
   **Answer:** B

4. **Which normalization technique groups “running,” “runs,” and “ran” under “run”?**  
   A. Case folding  
   B. Thesaurus expansion  
   C. Lemmatization  
   D. Soundex  
   **Answer:** C

5. **Soundex codes for “Robert” and “Rupert” are both R163 because:**  
   A. They have the same first vowel  
   B. They are homographs  
   C. Their consonant patterns sound similar  
   D. They are synonyms  
   **Answer:** C

6. **The Porter Stemmer differs from lemmatization because it:**  
   A. Uses a dictionary  
   B. Applies grammar rules  
   C. Strips affixes via heuristics  
   D. Resolves word sense ambiguity  
   **Answer:** C

7. **Which Python library would you use to extract text from a `.docx` file?**  
   A. pdfplumber  
   B. python-docx  
   C. BeautifulSoup  
   D. pandas  
   **Answer:** B

8. **After stopword removal, the query “Find hotels in New York” becomes:**  
   A. [“Find”, “hotels”, “in”, “New”, “York”]  
   B. [“hotels”, “New”, “York”]  
   C. [“Find”, “York”]  
   D. [“hotels”, “York”]  
   **Answer:** B

9. **Which encoding supports all Unicode characters in 1–4 bytes?**  
   A. ASCII  
   B. ISO-8859-1  
   C. UTF-8  
   D. UTF-16  
   **Answer:** C

10. **Tokenization in Chinese and Japanese requires:**  
    A. Splitting on spaces  
    B. A compound-splitting module  
    C. Vowel removal  
    D. No preprocessing  
    **Answer:** B

11. **Why might you skip stopword removal in a web search engine?**  
    A. Stopwords never affect performance  
    B. Modern compression makes including them cheap  
    C. Stopwords improve precision always  
    D. Web texts have no stopwords  
    **Answer:** B

12. **Which step converts “Cars” to “car”?**  
    A. Soundex  
    B. Case folding  
    C. Parsing  
    D. Tokenization  
    **Answer:** B

13. **An incidence matrix entry of 0 means:**  
    A. The term appears once  
    B. The term does not appear  
    C. The term appears multiple times  
    D. The term is a stopword  
    **Answer:** B

14. **Boolean query evaluation requires:**  
    A. Cosine similarity  
    B. Logical operations on incidence vectors  
    C. Neural embeddings  
    D. TF–IDF weighting  
    **Answer:** B

15. **Which step is most computationally intensive but yields linguistically valid forms?**  
    A. Stemming  
    B. Stopword removal  
    C. Lemmatization  
    D. Case folding  
    **Answer:** C
