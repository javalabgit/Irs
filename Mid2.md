Information Retrieval Systems and Algorithms Study Guide

Part 1: Review Questions and Answers

1. Explain the structure of PAT trees. How to construct PAT trees?

A PAT tree (Patricia Tree) is an information retrieval structure that treats text as a single, long string. It introduces new indices to the text where each position corresponds to a semi-infinite string (sistring).

Structure: A PAT tree is a type of binary trie with the following components:

* Internal Nodes (◯): These nodes do not store data directly but contain a "skip counter," which indicates the total displacement (bit position) in the string to be inspected next. They also have two pointers, corresponding to the bit values '0' and '1', leading to the next node.
* External Nodes (□): These nodes are the leaves of the tree. Each external node stores an integer displacement, which is the starting bit position of a unique semi-infinite string in the original text.

Construction Process: A PAT tree is constructed over all possible semi-infinite strings (sistrings) of a text. The process involves inserting each sistring into the tree based on its binary representation.

1. Start with an empty tree.
2. Insert Sistrings Sequentially: For each sistring (starting at positions 1, 2, 3, ... of the text), traverse the tree from the root.
3. Traversal and Bit Comparison: At each internal node, examine the bit of the current sistring at the position specified by the node's skip counter.
4. Follow Pointers: Follow the pointer corresponding to the bit's value (0 or 1).
5. Create New Nodes: If the traversal leads to a point where a distinction must be made between the new sistring and the ones already in the tree, a new internal node is created. This node's skip counter is set to the first bit position where the strings differ. The existing string and the new string are then placed as children of this new node.
6. Add External Nodes: The traversal continues until a unique path for the sistring is established, ending in a new external node that stores the starting position of that sistring.

The following diagram from the source illustrates the structure for a text starting with 01100100...:

 (Note: A renderable image is not possible, but the source diagram shows how sis1 through sis8 are inserted. For example, sis7 (starting 000101...) and sis4 (starting 001000...) are differentiated at the 3rd bit. An internal node would be created for bit position 3, with sis7 following the '0' path and sis4 following the '1' path.)


--------------------------------------------------------------------------------


2. Explain how a PAT tree is represented as an array.

A PAT tree can be represented as a PAT Array for searching purposes. This representation flattens the tree structure into a simple array.

* Content: The PAT array contains the integer displacements from the external (leaf) nodes of the PAT tree. Each integer represents the starting position of a semi-infinite string.
* Order: The leaf nodes in the array are stored in lexicographical order of the semi-infinite strings they represent.
* Usage: Because the array is sorted lexicographically, a binary search can be performed on it to find patterns efficiently.
* Updates: While searching is simple, updating a PAT array can be more complex than updating the tree structure.

For the example PAT tree provided in the source, the corresponding PAT Array is: 7 4 8 5 1 6 3 2

This means the sistring starting at position 7 is lexicographically first, followed by the one starting at position 4, and so on, with the sistring at position 2 being last.


--------------------------------------------------------------------------------


3. Describe the algorithms used for text searching operations in a PAT tree.

The source context implies two main methods for searching, corresponding to the tree and array representations.

1. Searching in a PAT Tree Structure: The search algorithm traverses the tree based on the bits of the query string.

1. Start at the root of the PAT tree.
2. At each internal node, read the node's skip counter to determine which bit of the query string to inspect.
3. Examine the value of that bit (0 or 1).
4. Follow the corresponding pointer (left for 0, right for 1) to the next node.
5. Repeat this process until an external node is reached or there is no valid path.
6. The external nodes found in the resulting subtree represent all the sistrings in the text that begin with the query string.

2. Searching in a PAT Array: Since the PAT array stores the leaf nodes (sistrings) in lexicographical order, searching is straightforward.

* Binary Search: A standard binary search can be used on the array to locate the range of sistrings that match the query prefix. This is efficient for locating patterns.


--------------------------------------------------------------------------------


4. Discuss experimental evaluations of stemming. How do they measure effectiveness?

Experimental evaluations of stemming aim to determine if reducing words to their root form improves information retrieval performance.

Effectiveness Measures: The effectiveness of stemming is typically measured using standard information retrieval metrics, which assess how well a system retrieves relevant documents. The studies mentioned in the source use the following dependent variables:

* Recall: The proportion of relevant documents that are successfully retrieved.
* Precision: The proportion of retrieved documents that are relevant.
* Combined Measures:
  * Rank Recall, Log Precision, Normalized Recall, Normalized Precision.
  * Precision measured at ten different recall levels (Recall-Precision plots).
  * The "E" measure, which combines recall and precision.

Summary of Experimental Evaluations:

Study	Collections Used	Comparison	Findings
Salton (1968)	IRE-3, ADI, Cranfield-1	Full stemming vs. suffix "s" removal	Mixed results. Full stemming was better for IRE-3 and ADI. "s" removal was better for the highly technical Cranfield-1 vocabulary.
Hafer & Weiss (1974)	ADI, Carolina Population Centre (CPC)	Their stemmer vs. SMART and manual stemming	Their stemmer outperformed the SMART stemmer and performed equally to manually derived stems. All stemming methods were better than using full terms.
Van Rijsbergen et al. (1980)	Cranfield-1	Porter stemmer vs. Dawson stemmer	The Porter stemmer was slightly better, but the differences were considered not meaningful.
Katzer et al. (1982)	Computer and Control Abstracts	Stemmed terms vs. 6 other representations	Stemmed terms never performed worse and in some cases performed significantly better than other representations like descriptors or title terms.
Harman (1991)	Cranfield 1400, Medlars, CACM	Porter, Lovins, and "s" removal stemmers	None of the stemmers significantly improved retrieval effectiveness in the IRX ranking system.

Conclusions from Studies: The source offers the following cautious conclusions:

1. Performance Impact is Equivocal: Stemming can affect retrieval performance, but the results are not consistently positive or negative. However, there is generally no evidence that stemming degrades effectiveness.
2. Equivalence to Manual Conflation: Stemming appears to be as effective as manual conflation (grouping of words).
3. Vocabulary Dependence: The effect of stemming depends on the nature of the vocabulary. Specific, homogeneous vocabularies (like Cranfield's) may show different results.
4. No Clear Best Stemmer: There is little difference in retrieval effectiveness between different full stemmers.


--------------------------------------------------------------------------------


5. Explain STOPLIST and its advantages.

Explanation: A stoplist is a list of trivial or common words that are filtered out during the text processing phase of an information retrieval system. These words, often called "stop words," include prepositions (with, in), conjunctions (and, but), articles (the, a), and other high-frequency words that are considered to have little value for indexing or searching. The process involves creating a list of these words and then removing them from documents and queries before they are further processed (e.g., by stemming or indexing).

Advantages: While the source doesn't list advantages in a separate section, they can be inferred from the context of text normalization and indexing:

* Reduces Index Size: By eliminating the most frequent words in a language, stoplists significantly reduce the size of the index (e.g., an inverted file), saving storage space.
* Improves Efficiency: With a smaller index, search operations become faster as there are fewer terms to process.
* Increases Relevance (Focus): Removing non-informative words helps the system focus on the more important, content-bearing terms in a document or query, which can lead to more relevant search results.


--------------------------------------------------------------------------------


6. Explain different types of stemming algorithms with suitable examples.

Stemming algorithms reduce words to their base or root form. The source describes several types available in Python's NLTK library.

Algorithm	Description	Example(s)	Advantages	Disadvantages
Porter's Stemmer	One of the most popular algorithms (1980). Applies a series of rules to remove common English suffixes.	agreed → agree	Very fast and efficient.	Output may not be a real word. Limited to English.
Snowball Stemmer	An enhanced, faster, and more aggressive version of Porter's stemmer (also by Martin Porter). Also known as Porter2.	running → run, quickly → quick	More efficient than Porter. Supports multiple languages.	More aggressive, which might lead to over-stemming.
Lancaster Stemmer	A very aggressive and fast stemmer that can be destructive, leading to excessively shortened stems.	happily → happy	Very fast, good for small datasets.	Can result in severe over-stemming. Less efficient than Snowball on large sets.
Regexp Stemmer	A flexible stemmer that uses user-defined regular expressions (regex) to remove prefixes or suffixes.	running → runn (using rule r'ing$')	Highly customizable for domain-specific tasks.	Requires manual rule definition. Can be computationally expensive.
Krovetz Stemmer	A linguistically-oriented stemmer (1993) designed to be more accurate and preserve meaning. Converts plurals to singulars and handles verb tenses.	children → child, running → run	More accurate, preserves meaning.	Slower and may be inefficient with large corpora.
Lovins Stemmer	One of the earliest stemming algorithms (1968). Applies a set of rules to remove common word endings.	looks → look, winged → wing	Simple and fast.	May not be as accurate as more advanced algorithms.


--------------------------------------------------------------------------------


7. What are the important features of a thesaurus used in information retrieval?

An Information Retrieval (IR) thesaurus is a controlled vocabulary of terms and their relationships, designed to coordinate the processes of indexing and document retrieval within a specific subject domain.

Key Features:

1. Coordination Level: This refers to the construction of phrases.
  * Pre-coordination: The thesaurus contains phrases (e.g., "computer-aided instruction"). This increases precision but requires the user to know the specific phrases.
  * Post-coordination: The thesaurus contains only single words, and users construct phrases during the search (e.g., "library" AND "school"). This is more flexible but can be ambiguous ("school library" vs. "library school").
2. Term Relationships: These define the semantic connections between terms.
  * Equivalence: Connects synonyms or quasi-synonyms (e.g., USE "caesium" FOR "cesium").
  * Hierarchical: Shows broader (BT) and narrower (NT) relationships, like genus-species (e.g., "computer applications" BT for "computer-aided instruction").
  * Non-hierarchical (Associative): Links related terms (RT) that are not hierarchically connected, such as part-whole or object-property (e.g., "bus" RT "seat").
3. Number of Entries for Each Term: Ideally, each term has a single entry. However, homographs (words with multiple meanings) require separate entries, often distinguished by parenthetical qualifiers, like bonds (chemical) and bonds (adhesive).
4. Specificity of Vocabulary: A highly specific vocabulary uses precise terms to describe subjects in great detail. This improves retrieval precision but leads to a larger vocabulary that requires more maintenance.
5. Control on Term Frequency (for statistical thesauri): To ensure good matching, terms grouped into an equivalence class should have roughly equal frequencies of occurrence in the document collection.
6. Normalization of Vocabulary: This involves applying a set of rules to standardize the form of terms in the thesaurus. Rules may dictate that terms should be nouns, avoid prepositions, and have consistent spelling, capitalization, and abbreviation formats. This brings consistency but requires users to be aware of the rules.


--------------------------------------------------------------------------------


8. Explain stemming compressed inverted file.

The concept of a stemming compressed inverted file refers to the use of stemming as a method to reduce the storage size of index files, particularly inverted files. An inverted file is a core data structure in IR that maps terms to the documents they appear in.

Process and Effect:

* Mechanism: Since a stem (e.g., "inform") is typically shorter than the original words it represents (e.g., "information," "informing," "informed"), replacing the full words with their stems in the index file's dictionary leads to a reduction in file size.
* Compression Savings: The savings in storage can be substantial.
  * A study by Lennon et al. (1981) reported that the index file for the Cranfield collection was 32.1% smaller after being stemmed.
  * Harman (1991) reported a 20% index reduction for a 1.6 MB database and a 13.5% reduction for a 50 MB database.
* Factors Affecting Compression:
  * The number of suffixes used by the stemmer: a stemmer with more suffix-removal rules generally achieves a higher compression rate.
  * The nature of the database: for real-world databases containing numbers, proper names, and misspellings, the compression factors are not as large.


--------------------------------------------------------------------------------


9. Explain the process of thesaurus construction from text with an example.

Automatic thesaurus construction from text uses statistical procedures to identify important terms and their relationships from a representative document collection. The process involves three main stages.

The Process:

1. Construction of Vocabulary: The goal is to identify the most informative terms (words and phrases).
  * Normalization:
    * Apply a stoplist to remove trivial words (e.g., "the", "is", "at").
    * Apply a stemming algorithm to reduce words to their root form (e.g., "retrieval", "retrieved" → "retriev").
  * Term Selection: Statistically evaluate the resulting stems to select the best ones. Methods include:
    * Frequency of Occurrence: Select terms in the mid-frequency range, as they are often the most descriptive.
    * Discrimination Value (DV): Select terms that are good at distinguishing documents from one another.
    * Poisson Model: Identify non-trivial words, as their distribution in text deviates from a single Poisson distribution.
  * Phrase Construction (Optional): If a pre-coordinated thesaurus is desired, build phrases from high-frequency terms that frequently co-occur (e.g., identify "artificial intelligence" as a phrase).
2. Similarity Computations: Calculate the statistical association between pairs of selected terms. This is typically based on their co-occurrence within documents (or smaller contexts like sentences). Common similarity measures include:
  * Cosine Similarity
  * Dice Coefficient
3. Organization of Vocabulary: Structure the vocabulary based on the computed similarities.
  * This is often done using a clustering algorithm to group similar terms into classes.
  * These classes can be organized into a hierarchy, where broader terms become parents to more specific, similar terms. For example, a method described in the source uses frequency to define levels, with high-frequency terms at the top and low-frequency terms at the bottom, creating parent-child links based on similarity between adjacent levels.

Example Illustration: Imagine a collection of documents on computer science.

1. Vocabulary Construction:
  * Text: "Information retrieval systems retrieve data."
  * After stoplist: "Information retrieval systems retrieve data."
  * After stemming: "inform retriev system retriev data."
  * The stems inform, retriev, system, and data are selected as candidate terms.
2. Similarity Computation: The system analyzes the entire collection and finds that retriev and inform co-occur frequently. Their similarity score (e.g., Cosine) is calculated and found to be high.
3. Vocabulary Organization: The term system might be identified as a high-frequency, broad term. retriev might be a mid-frequency term. In a frequency-based hierarchy, system could become a parent node to a cluster containing retriev and inform, establishing a conceptual relationship.


--------------------------------------------------------------------------------


10. Describe the process in steps of a KMP Algorithm and how it improves efficiency.

The Knuth-Morris-Pratt (KMP) algorithm is an efficient string matching algorithm that finds occurrences of a pattern within a text. It achieves linear time complexity by intelligently handling mismatches.

Process Steps:

The algorithm works in two main phases:

1. Preprocessing Step – Build the LPS Array:

* This step processes only the pattern to create an auxiliary array called the LPS (Longest Prefix Suffix) array.
* For each position i in the pattern, lps[i] stores the length of the longest proper prefix of the substring pattern[0...i] which is also a suffix of that same substring.
* Example: For the pattern abcdabca:
  * The prefix abc at the beginning is also a suffix of abcdabc. Its length is 3, so lps[6] = 3.
  * The final LPS array is: [0, 0, 0, 0, 1, 2, 3, 1].

2. Matching Step – Search the Pattern in the Text:

* Two pointers are used: i for the text and j for the pattern.
* Characters text[i] and pattern[j] are compared.
* If characters match: Increment both i and j to continue matching.
* If characters do not match:
  * If j > 0 (mismatch is not at the start of the pattern), consult the LPS array. The pattern pointer j is moved back to lps[j-1]. The text pointer i is not moved. This effectively slides the pattern forward, aligning the previously matched prefix with a corresponding suffix, thus avoiding redundant comparisons.
  * If j == 0 (mismatch at the first character of the pattern), simply increment i to check the next position in the text.
* If a full match is found (j reaches the end of the pattern): Record the starting index (i - j) as a match. Then, to find subsequent matches, update j using the LPS array (j = lps[j-1]) and continue the search.

How KMP Improves Efficiency: The KMP algorithm's efficiency comes from its ability to avoid re-comparing characters. The Naive algorithm shifts the pattern by only one position after a mismatch. KMP, by using the precomputed LPS array, makes an "intelligent shift". It already knows the length of the prefix that matches a suffix ending at the point of mismatch, so it can shift the pattern forward by several positions, skipping comparisons for characters that are guaranteed not to match. This ensures that each character in the text is examined at most once, reducing the time complexity from the Naive algorithm's O(n*m) to O(n + m).


--------------------------------------------------------------------------------


11. Briefly discuss the Naive algorithm.

The Naive algorithm is a straightforward, brute-force string searching algorithm.

* Method: It works by sliding a "template" of the pattern over the text, one character at a time, from the first possible position to the last. At each position, it performs a character-by-character comparison between the pattern and the corresponding substring of the text. If all characters match, it reports an occurrence.
* Example: To find "TEST" in "THIS IS A TEST TEXT":
  1. Compare "TEST" with "THIS" (mismatch). Shift by 1.
  2. Compare "TEST" with "HIS " (mismatch). Shift by 1.
  3. ...Continue until reaching index 10.
  4. Compare "TEST" with "TEST" (match). Report match at index 10.
* Complexity:
  * Time Complexity: The worst-case time complexity is O((n-m+1) * m), often simplified to O(n*m), where n is the text length and m is the pattern length. This occurs when a mismatch is always found on the last character of the pattern, or when no match exists. The best case is O(n).
  * Space Complexity: It requires O(1) auxiliary space.


--------------------------------------------------------------------------------


12. Explain the Shift-Or algorithm and its advantage for bit-parallelism.

The Shift-Or algorithm (also known as the Bitap algorithm) is a fast and efficient text searching algorithm that uses bitwise operations.

How it Works:

1. Preprocessing (Bit Masking): For a pattern of length m, a bit mask of length m is created for each character in the alphabet. For a given character c, the i-th bit of its mask is set to 0 if the i-th character of the pattern is c, and 1 otherwise. A default mask of all 1s is used for characters not in the pattern.
2. Searching:
  * A state register r, which is an m-bit integer, is maintained and initialized to all 1s.
  * The algorithm iterates through the text character by character.
  * For each text character t, the state register r is updated using the formula: r = (r << 1) | mask[t].
    * r << 1: This is a left bit shift, which effectively advances the state of the match by one position. A 0 is shifted in on the right.
    * | mask[t]: This is a bitwise OR operation with the precomputed mask for the current text character. It updates the bit positions corresponding to potential matches for t.
3. Match Detection: A match is found when the most significant (leftmost) bit of the state register r becomes 0. This indicates that a 0 has successfully been shifted through all m positions, meaning all characters of the pattern have been matched consecutively.

Advantage for Bit-Parallelism: The primary advantage of the Shift-Or algorithm is its efficient use of bit-parallelism.

* Hardware-Level Speed: The core of the algorithm relies on bitwise operations (shift << and OR |), which are executed as single, extremely fast instructions at the hardware level of a CPU.
* Parallel Comparisons: For patterns with a length m that is less than or equal to the computer's word size (e.g., 64 bits), the entire state update for one text character is performed in a single clock cycle. This is equivalent to performing m character comparisons in parallel.
* Efficiency: This parallelism makes the algorithm extremely fast, especially for short patterns.


--------------------------------------------------------------------------------


13. Explain the working of the Karp-Rabin algorithm with an example string & pattern.

The Karp-Rabin algorithm is a string matching algorithm that uses hashing to find a pattern in a text. Instead of comparing characters, it compares the hash value of the pattern with the hash values of text substrings.

Working Principle:

1. Hashing: The algorithm first computes a numeric hash value for the pattern.
2. Sliding and Hashing Text: It then iterates through the text, considering each substring of the same length as the pattern. For each substring, it computes a hash value.
3. Hash Comparison: The hash of the text substring is compared to the hash of the pattern.
  * If hashes differ: The substring cannot be a match, and the algorithm moves to the next substring.
  * If hashes match: A potential match is found. However, this could be a hash collision (where two different strings produce the same hash). To confirm, the algorithm performs a direct, character-by-character comparison between the pattern and the substring. If they are identical, a true match is reported.
4. Rolling Hash: To achieve efficiency, Karp-Rabin uses a rolling hash function. Instead of re-calculating the hash for each new substring from scratch (which would be slow), it calculates the hash for the next substring in constant O(1) time. This is done by mathematically removing the contribution of the character leaving the "window" and adding the contribution of the new character entering it.

Example:

* Text: aabaacaadaabaaba
* Pattern: aaba

1. Calculate Pattern Hash: The algorithm computes the hash for "aaba". Let's call this hash_p. (For simplicity, assume a simple hash function).
2. Initial Text Substring: It computes the hash for the first substring of the text, "aaba". The hash matches hash_p.
3. Verification: A character-by-character check confirms "aaba" == "aaba". A match is reported at index 0.
4. Roll the Hash: The algorithm slides the window one position to the right. Using the rolling hash function, it efficiently calculates the hash for the new substring "abaa" from the previous hash of "aaba".
5. Compare: The new hash for "abaa" does not match hash_p. The algorithm continues.
6. Continue Sliding: This process of rolling the hash, comparing, and (if necessary) verifying continues for every substring: "baac", "aaca", etc.
7. Subsequent Matches: When the window reaches the substring at index 9 ("aaba"), the hash will match hash_p again. Verification confirms the match. The same occurs at index 12.
8. Final Output: The algorithm returns the starting indices of all confirmed matches: [0, 9, 12].


--------------------------------------------------------------------------------


14. Explain the Boyer-Moore algorithm.

The Boyer-Moore algorithm is a highly efficient string searching algorithm known for its ability to skip large sections of text, making it significantly faster than many other algorithms in practice.

Core Concepts:

* Right-to-Left Scan: Unlike most algorithms that compare from left to right, Boyer-Moore starts matching from the last character of the pattern and moves backward.
* Large Shifts: Its efficiency comes from two precomputed heuristics that determine the maximum possible safe shift of the pattern along the text after a mismatch. The algorithm always takes the larger of the two suggested shifts.

Heuristics:

1. Bad Character Heuristic: This rule is triggered when a mismatch occurs. The mismatched character in the text is called the "bad character."

* Idea: Upon a mismatch, shift the pattern to the right so that the last occurrence of the bad character within the pattern aligns with the bad character in the text.
* Case 1: Bad character exists in the pattern.
  * Example: Text ...A..., Pattern ...B.... Mismatch occurs at text character A. Find the last A in the pattern and shift the pattern so they align.
  * T: ... G C A A G A ...
  * P: A A T A A C (Mismatch at G vs C)
  * The bad character is G. The last occurrence of G is not in the pattern. Wait, the source example is a bit different. Let's re-read it.
  * T: ... G C A A G A ...
  * P:          G A A T A A (Aligned at some position. Mismatch A vs T)
  * The "bad character" in the text is A. We look for the last occurrence of A in the pattern before the mismatch point. Let's say it's at index 1 of the pattern. We shift the pattern so that pattern[1] aligns with the bad character A in the text.
* Case 2: Bad character does not exist in the pattern.
  * If the bad character from the text does not appear anywhere in the pattern, then no match is possible until the pattern is shifted completely past the point of the mismatch.
  * T: ... G C A A G A ...
  * P:          T E S T I N G (Mismatch at A vs G)
  * The bad character is A. A does not exist in the pattern TESTING. The entire pattern is shifted past this position A.

2. Good Suffix Heuristic:

* The source context mentions this heuristic as the second component of the Boyer-Moore algorithm but does not provide a detailed explanation. It is used in conjunction with the Bad Character Heuristic to determine the maximum shift distance.

Overall Process:

1. Preprocess the pattern to create lookup tables for the Bad Character and Good Suffix heuristics.
2. Align the pattern with the start of the text.
3. Compare the pattern from right to left against the corresponding text.
4. If a mismatch occurs, calculate the shift distance suggested by both heuristics.
5. Shift the pattern forward by the maximum of these two distances.
6. Repeat from step 3 until the end of the text is reached.


--------------------------------------------------------------------------------


Part 2: Glossary of Key Terms

Term	Definition
Bad Character Heuristic	A rule in the Boyer-Moore algorithm. When a mismatch occurs, it shifts the pattern to align the last occurrence of the mismatched text character (the "bad character") with its position in the pattern.
Bit Mask	A bit pattern used in the Shift-Or algorithm to represent the positions of a specific character within the search pattern.
Boyer-Moore Algorithm	An efficient string searching algorithm that matches the pattern from right to left and uses the Bad Character and Good Suffix heuristics to make large shifts along the text.
Coordination Level	A feature of a thesaurus that defines whether phrases are pre-defined in the vocabulary (pre-coordination) or constructed by the user during a search (post-coordination).
Cosine Similarity	A measure used in thesaurus construction to compute the statistical association between two terms based on the number of documents they co-occur in.
Discrimination Value (DV)	A statistical method for evaluating a term's worth by measuring how much it helps to distinguish documents from one another in a collection.
External Node	A leaf node in a PAT tree that stores an integer representing the starting position of a semi-infinite string in the text.
Hash Collision	In the Karp-Rabin algorithm, the event where two different strings produce the same hash value, requiring a character-by-character check to confirm a match.
Homograph	A word that has multiple meanings. In thesauri, homographs require separate entries, often distinguished by qualifiers (e.g., bonds (chemical)).
Internal Node	A non-leaf node in a PAT tree that contains a skip counter (a bit position to check) and pointers to its children.
Inverted File/Index	A data structure used in information retrieval that maps keywords to a list of documents in which they appear.
Karp-Rabin Algorithm	A string searching algorithm that uses a rolling hash function to quickly compare the hash of a pattern with the hashes of text substrings.
Knuth-Morris-Pratt (KMP)	An efficient string searching algorithm that uses a precomputed LPS (Longest Prefix Suffix) array to avoid redundant comparisons after a mismatch, achieving linear time complexity.
LPS (Longest Prefix Suffix) Array	An auxiliary array used in the KMP algorithm. lps[i] stores the length of the longest proper prefix of pattern[0...i] that is also a suffix of pattern[0...i].
Naive Algorithm	A simple, brute-force string searching algorithm that checks for a pattern match at every possible position in a text by sliding the pattern one character at a time.
Normalization (Vocabulary)	The process of standardizing thesaurus terms by applying rules for form (e.g., noun form), spelling, capitalization, etc., to ensure consistency.
PAT Array	An array representation of a PAT tree containing the starting positions of all semi-infinite strings, sorted in lexicographical order.
PAT Tree (Patricia Tree)	A compressed binary trie data structure used to index a text by storing all of its semi-infinite strings for efficient searching.
Rolling Hash	A function used in the Karp-Rabin algorithm that allows the hash value of a new text substring to be calculated in constant time from the hash of the previous substring.
Semi-Infinite String (sistring)	A string that starts at a specific position in a text and is considered to extend to the end of the text. It is the fundamental data unit indexed by a PAT tree.
Shift-Or Algorithm (Bitap)	A string searching algorithm that uses bitwise operations (bit masks and bit shifts) to perform fast, parallel comparisons, making it highly efficient for patterns shorter than the computer's word size.
Stemming	A text processing technique that reduces words to their root or base form by removing prefixes and suffixes (e.g., "running" becomes "run").
Stoplist	A list of common, high-frequency words (e.g., "the", "a", "is") that are removed from a text during processing to reduce index size and improve efficiency.
Term Relationships	The semantic connections between terms in a thesaurus, categorized as equivalence (synonyms), hierarchical (broader/narrower terms), and non-hierarchical (related terms).
Thesaurus (in IR)	A controlled vocabulary for a specific domain, listing terms and their semantic relationships to coordinate indexing and retrieval.
