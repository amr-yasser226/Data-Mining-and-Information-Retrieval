1. **Which component of an IR system converts raw documents into indexed terms?**  
   A. Retrieval Model  
   B. Query Processor  
   C. Indexer  
   D. User Interface  
   **Answer:** C

2. **In Boolean retrieval, a postings list contains:**  
   A. Term frequencies  
   B. Document IDs where the term appears  
   C. Term positions  
   D. Document lengths  
   **Answer:** B

3. **What is the primary disadvantage of a full term–document incidence matrix?**  
   A. Too few zeros  
   B. Inefficient boolean retrieval  
   C. High memory usage due to sparsity  
   D. Lack of ranking  
   **Answer:** C

4. **Tokenization is the process of:**  
   A. Removing stopwords  
   B. Splitting text into tokens  
   C. Lemmatizing words  
   D. Encoding characters  
   **Answer:** B

5. **Stopword removal is least advisable for which query type?**  
   A. Boolean  
   B. Phrase  
   C. Navigation  
   D. Image  
   **Answer:** B

6. **Case folding converts:**  
   A. Words to uppercase  
   B. Words to lowercase  
   C. Numbers to words  
   D. Punctuation to tokens  
   **Answer:** B

7. **Soundex groups words by:**  
   A. Spelling similarity  
   B. Semantic meaning  
   C. Pronunciation  
   D. Term frequency  
   **Answer:** C

8. **Lemmatization differs from stemming by:**  
   A. Using rule-based suffix removal  
   B. Producing non-dictionary stems  
   C. Considering part-of-speech and context  
   D. Only handling prefixes  
   **Answer:** C

9. **The Porter Stemmer is a:**  
   A. Lemmatizer  
   B. Rule-based stemmer  
   C. Phonetic algorithm  
   D. Contextual embedder  
   **Answer:** B

10. **An inverted index maps terms to:**  
    A. Query IDs  
    B. Posting lists  
    C. Stopword lists  
    D. Raw document text  
    **Answer:** B

11. **Self-attention computes token interactions in:**  
    A. Sequential order  
    B. Parallel  
    C. Random  
    D. Frequency order  
    **Answer:** B

12. **In Transformer positional encoding, sinusoids provide:**  
    A. Token IDs  
    B. Frequency patterns for position  
    C. Stopwords  
    D. Document boundaries  
    **Answer:** B

13. **Cosine similarity between two one-hot vectors is:**  
    A. 1  
    B. 0  
    C. –1  
    D. Undefined  
    **Answer:** B

14. **TF–IDF weight of a term with df = N is:**  
    A. High  
    B. Zero  
    C. 1  
    D. Negative  
    **Answer:** B

15. **IDF is calculated as:**  
    A. \(\log_{10}N\)  
    B. \(\log_{10}(N/\mathrm{df})\)  
    C. \(1 + \log\mathrm{tf}\)  
    D. \(\mathrm{tf}/\mathrm{df}\)  
    **Answer:** B

16. **BM25 normalizes term frequency by:**  
    A. Document frequency  
    B. Document length  
    C. Query length  
    D. Term rarity  
    **Answer:** B

17. **BERT’s pretraining uses which two tasks?**  
    A. MLM and NSP  
    B. CBOW and Skip-Gram  
    C. PRP and DCG  
    D. PRF and LM  
    **Answer:** A

18. **In PRF, the top-k documents are assumed to be:**  
    A. Non-relevant  
    B. Relevant  
    C. Random  
    D. Stopwords  
    **Answer:** B

19. **Dice’s coefficient ranges between:**  
    A. –1 and 1  
    B. 0 and 1  
    C. 1 and ∞  
    D. –∞ and ∞  
    **Answer:** B

20. **Mutual information is zero when two terms are:**  
    A. Independent  
    B. Identical  
    C. Rare  
    D. Frequent  
    **Answer:** A

21. **Rocchio feedback moves the query vector toward:**  
    A. Non-relevant docs  
    B. Relevant docs  
    C. Stopwords  
    D. Random docs  
    **Answer:** B

22. **Which parameter in Rocchio controls negative feedback?**  
    A. \(\alpha\)  
    B. \(\beta\)  
    C. \(\gamma\)  
    D. \(\lambda\)  
    **Answer:** C

23. **Pseudo-relevance feedback may suffer from:**  
    A. Perfect recall  
    B. Query drift  
    C. High precision  
    D. Low latency  
    **Answer:** B

24. **Implicit feedback is collected via:**  
    A. Clicks and dwell time  
    B. Manual labeling  
    C. WordNet  
    D. BM25 scores  
    **Answer:** A

25. **One-hot encoding dimension equals:**  
    A. Vocabulary size  
    B. Document count  
    C. Query length  
    D. Embedding dimension  
    **Answer:** A

26. **A co-occurrence matrix is typically:**  
    A. Dense  
    B. Sparse  
    C. Low-dimensional  
    D. Learned  
    **Answer:** B

27. **Word2Vec CBOW predicts:**  
    A. Context words from the target  
    B. Target word from context  
    C. TF–IDF scores  
    D. BM25 scores  
    **Answer:** B

28. **Skip-Gram predicts:**  
    A. Target word  
    B. Context words  
    C. Document frequencies  
    D. Sentence boundaries  
    **Answer:** B

29. **GloVe optimizes:**  
    A. Softmax over contexts  
    B. Weighted least-squares on log co-occurrence  
    C. TF–IDF on global docs  
    D. BM25 on term vectors  
    **Answer:** B

30. **ELMo uses:**  
    A. Bidirectional LSTMs  
    B. CBOW  
    C. Skip-Gram  
    D. One-hot encoding  
    **Answer:** A

31. **BERT’s WordPiece tokenization handles:**  
    A. Punctuation only  
    B. Rare words by subword units  
    C. Sentence splitting  
    D. Stopwords  
    **Answer:** B

32. **Masked tokens in BERT amount to:**  
    A. 5%  
    B. 15%  
    C. 50%  
    D. 100%  
    **Answer:** B

33. **[CLS] vector is used for:**  
    A. Token classification  
    B. Sequence classification  
    C. Positional encoding  
    D. Word embedding  
    **Answer:** B

34. **Next sentence prediction trains BERT to:**  
    A. Predict masked words  
    B. Classify sentence order  
    C. Generate next word  
    D. Compute embeddings  
    **Answer:** B

35. **Transformer encoders process layers:**  
    A. Recurrently  
    B. In parallel  
    C. Convolutively  
    D. Sequentially one token at a time  
    **Answer:** B

36. **Positional encoding uses base frequency of:**  
    A. 1  
    B. 10,000  
    C. \(d\)  
    D. \(\sqrt{d}\)  
    **Answer:** B

37. **Self-attention scaling divides by:**  
    A. \(d\)  
    B. \(\sqrt{d_k}\)  
    C. \(1/d\)  
    D. \(d^2\)  
    **Answer:** B

38. **Multi-headed attention improves:**  
    A. Single representation  
    B. Parallel context learning  
    C. Document frequency  
    D. Stopword removal  
    **Answer:** B

39. **PRP ranks by:**  
    A. \(P(d\mid Q)\)  
    B. \(P(Q\mid d)\)  
    C. \(P(d)\)  
    D. \(P(Q)\)  
    **Answer:** A

40. **In LM retrieval, smoothing avoids:**  
    A. Overfitting  
    B. Zero probabilities  
    C. High recall  
    D. Low precision  
    **Answer:** B

41. **Jelinek–Mercer smoothing parameter \(\lambda\) is used for:**  
    A. PRF  
    B. LM smoothing  
    C. TF–IDF  
    D. BM25  
    **Answer:** B

42. **MAP is the mean of:**  
    A. P@k  
    B. AP  
    C. DCG  
    D. Recall  
    **Answer:** B

43. **nDCG normalizes by:**  
    A. Query length  
    B. Ideal DCG  
    C. Document frequency  
    D. Term frequency  
    **Answer:** B

44. **Precision@k measures:**  
    A. Recall at k  
    B. Precision at k  
    C. AP at k  
    D. DCG at k  
    **Answer:** B

45. **A zone index encodes:**  
    A. Stopwords  
    B. Document sections  
    C. Term frequency  
    D. Query logs  
    **Answer:** B

46. **Boolean AND on postings lists costs:**  
    A. O(nm)  
    B. O(n+m)  
    C. O(n\*log m)  
    D. O(1)  
    **Answer:** B

47. **Transformers lack:**  
    A. Attention  
    B. Positional awareness  
    C. Parallelism  
    D. Embeddings  
    **Answer:** B

48. **Doc length normalization in BM25 uses parameter:**  
    A. \(k_1\)  
    B. \(b\)  
    C. \(\lambda\)  
    D. \(\beta\)  
    **Answer:** B

49. **In TF–IDF, term frequency uses:**  
    A. Raw count only  
    B. Log-frequency  
    C. IDF only  
    D. BM25 formula  
    **Answer:** B

50. **A “hit” in IR terminology is a:**  
    A. Retrieved document  
    B. Click  
    C. Session  
    D. Token  
    **Answer:** A

51. **An “expert search” retrieves:**  
    A. Documents  
    B. People  
    C. Queries  
    D. Ads  
    **Answer:** B

52. **Snippet selection is performed on:**  
    A. Results page  
    B. Index  
    C. Query  
    D. Document parsing  
    **Answer:** A

53. **Precision measures:**  
    A. Retrieved vs. relevant  
    B. Relevant vs. retrieved  
    C. Retrieved vs. non-relevant  
    D. Relevant vs. non-relevant  
    **Answer:** A

54. **Recall measures:**  
    A. Retrieved vs. relevant  
    B. Relevant vs. retrieved  
    C. Retrieved vs. corpus  
    D. Relevant vs. corpus  
    **Answer:** D

55. **F1 is the harmonic mean of:**  
    A. P & R  
    B. P & AP  
    C. MAP & nDCG  
    D. BM25 & TF–IDF  
    **Answer:** A

56. **Sequential scan retrieval is:**  
    A. Inverted index  
    B. Grep-like full scan  
    C. BM25  
    D. BERT-based  
    **Answer:** B

57. **Mean Reciprocal Rank applies when each query has:**  
    A. One relevant doc  
    B. Many relevant docs  
    C. No relevance  
    D. Binary relevance only  
    **Answer:** A

58. **Scholar search allows structured queries based on:**  
    A. Keywords only  
    B. Author, title, year  
    C. URL  
    D. BM25  
    **Answer:** B

59. **Text classification in IR is considered a(n):**  
    A. Retrieval task  
    B. Preprocessing step  
    C. Ranking function  
    D. Efficiency metric  
    **Answer:** A

60. **Expert search uses:**  
    A. Terms only  
    B. Entity representations  
    C. Zone indexes  
    D. Positional encodings  
    **Answer:** B

61. **Conversational search requires:**  
    A. Static queries  
    B. Dialogue context  
    C. One-hot embeddings  
    D. Co-occurrence counts  
    **Answer:** B

62. **Recommendation in IR retrieves:**  
    A. Documents  
    B. Items based on user history  
    C. Queries  
    D. Stopwords  
    **Answer:** B

63. **Information visualization in IR helps with:**  
    A. Query parsing  
    B. User navigation of results  
    C. Ranking  
    D. Tokenization  
    **Answer:** B

64. **Sponsored search refers to:**  
    A. Unpaid results  
    B. Advertisements  
    C. Stopword lists  
    D. Inverted index  
    **Answer:** B

65. **Postings with positions are called:**  
    A. Frequency indexes  
    B. Positional indexes  
    C. Zone indexes  
    D. One-hot  
    **Answer:** B

66. **Phrase queries are a special case of:**  
    A. Boolean queries  
    B. Proximity queries (k=1)  
    C. Ranked queries  
    D. Zone queries  
    **Answer:** B

67. **Zone encoding in postings tags each docID with:**  
    A. Term frequency  
    B. Zone label  
    C. Position  
    D. Query ID  
    **Answer:** B

68. **Precision and recall trade-off is visualized by:**  
    A. ROC curve  
    B. P-R curve  
    C. DCG plot  
    D. TF–IDF histogram  
    **Answer:** B

69. **AP averages precision at:**  
    A. All ranks  
    B. Relevant doc positions  
    C. k = 10 only  
    D. Query count  
    **Answer:** B

70. **DCG discounts by:**  
    A. \(\log_2(i+1)\)  
    B. \(i\)  
    C. \(\sqrt{i}\)  
    D. \(1/i\)  
    **Answer:** A

71. **NDCG is DCG divided by:**  
    A. MAP  
    B. IDCG  
    C. TF–IDF  
    D. BM25  
    **Answer:** B

72. **Document frequency df\(_t\) counts:**  
    A. Term occurrences in doc  
    B. Docs containing the term  
    C. Query matches  
    D. Zone hits  
    **Answer:** B

73. **Collection frequency cf\(_t\) counts:**  
    A. Terms in doc  
    B. Occurrences across corpus  
    C. Query frequency  
    D. AP score  
    **Answer:** B

74. **High IDF indicates:**  
    A. Common term  
    B. Rare term  
    C. Stopword  
    D. Phrase  
    **Answer:** B

75. **TF–IDF ranking sums weights of:**  
    A. All terms in doc  
    B. Query terms intersection  
    C. All vocabulary  
    D. Zone labels  
    **Answer:** B

76. **Query logs expansion uses:**  
    A. WordNet  
    B. Past user queries  
    C. BM25 scores  
    D. Co-occurrence only  
    **Answer:** B

77. **Relevance feedback refines queries based on:**  
    A. Segment IDs  
    B. User judgments  
    C. Document IDs  
    D. Positional encodings  
    **Answer:** B

78. **Implicit feedback includes:**  
    A. Manual labels  
    B. Click patterns  
    C. Random sampling  
    D. Word vectors  
    **Answer:** B

79. **Word embeddings are:**  
    A. Sparse vectors  
    B. Dense vectors  
    C. One-hot  
    D. Zone lists  
    **Answer:** B

80. **Contextual embeddings vary by:**  
    A. Pretraining corpora  
    B. Sentence context  
    C. Vocabulary size  
    D. Embedding dimension  
    **Answer:** B

81. **ELMo uses:**  
    A. Convolution  
    B. Bi-LSTM  
    C. Transformer encoder  
    D. One-hot  
    **Answer:** B

82. **BERT’s architecture is:**  
    A. Decoder-only  
    B. Encoder-only  
    C. Encoder-decoder  
    D. RNN-based  
    **Answer:** B

83. **BERT uses attention mask:**  
    A. To prevent future token peeking  
    B. To ignore padding tokens  
    C. To mark stopwords  
    D. To encode positions  
    **Answer:** B

84. **Multi-stage ranking often begins with:**  
    A. BERT  
    B. BM25  
    C. GloVe  
    D. RNN  
    **Answer:** B

85. **MonoBERT scores each doc:**  
    A. Pairwise  
    B. Independently  
    C. In parallel  
    D. Using co-occurrence  
    **Answer:** B

86. **DuoBERT compares docs:**  
    A. Independently  
    B. Pairwise probabilities  
    C. Using TF–IDF only  
    D. With one-hot encoding  
    **Answer:** B

87. **Transformer layers contain:**  
    A. RNN cells  
    B. Self-attention + feedforward  
    C. Convolutions  
    D. GloVe lookups  
    **Answer:** B

88. **BERT fine-tuning adapts:**  
    A. Only embeddings  
    B. All transformer weights  
    C. Only QA head  
    D. Only segment embeddings  
    **Answer:** B

89. **Positional encoding dimension must be:**  
    A. Odd  
    B. Even  
    C. Prime  
    D. One  
    **Answer:** B

90. **In softmax attention, sum of weights =**  
    A. 0  
    B. 1  
    C. d  
    D. Query length  
    **Answer:** B

91. **TF–IDF one-hot hybrid is used in:**  
    A. BERT  
    B. BM25  
    C. VSM  
    D. RNN  
    **Answer:** C

92. **A zone labeled index helps with:**  
    A. Phrase queries  
    B. Fielded search  
    C. Trigram models  
    D. LM smoothing  
    **Answer:** B

93. **Bigram LMs account for:**  
    A. Single-word frequency  
    B. Word pairs  
    C. TF–IDF  
    D. Self-attention  
    **Answer:** B

94. **Trigram LMs include:**  
    A. Three-word sequences  
    B. One word only  
    C. Doc length  
    D. Zone labels  
    **Answer:** A

95. **RNNs maintain:**  
    A. Document frequency  
    B. Internal hidden state  
    C. Positional encoding  
    D. Term weights  
    **Answer:** B

96. **LSTM includes gates for:**  
    A. Input, forget, output  
    B. Syntax only  
    C. Zone labels  
    D. Static embeddings  
    **Answer:** A

97. **Transformer parallelism advantage is mainly for:**  
    A. Single CPU  
    B. GPU/TPU  
    C. RNN hardware  
    D. Disk I/O  
    **Answer:** B

98. **TF–IDF and BM25 are examples of:**  
    A. Language models  
    B. Heuristic weighting  
    C. Neural embeddings  
    D. Zone indexes  
    **Answer:** B

99. **Stopwords are removed to:**  
    A. Improve precision and reduce index size  
    B. Improve recall only  
    C. Decrease document length  
    D. Increase term frequency  
    **Answer:** A

100. **The Cranfield paradigm requires:**  
    A. Query logs only  
    B. Document collection, queries, relevance judgments  
    C. User clicks  
    D. BM25 scores only  
    **Answer:** B
