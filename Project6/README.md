# Parser and Questions
## Parser
Write an AI to parse sentences and extract noun phrases.

A common task in natural language processing is parsing, the process of determining the structure of a sentence. This is useful for a number of reasons: knowing the structure of a sentence can help a computer to better understand the meaning of the sentence, and it can also help the computer extract information out of a sentence. In particular, it’s often useful to extract noun phrases out of a sentence to get an understanding for what the sentence is about.

In this problem, we’ll use the context-free grammar formalism to parse English sentences to determine their structure. Recall that in a context-free grammar, we repeatedly apply rewriting rules to transform symbols into other symbols. The objective is to start with a nonterminal symbol S (representing a sentence) and repeatedly apply context-free grammar rules until we generate a complete sentence of terminal symbols (i.e., words). The rule S -> N V, for example, means that the S symbol can be rewritten as N V (a noun followed by a verb). If we also have the rule N -> "Holmes" and the rule V -> "sat", we can generate the complete sentence "Holmes sat."

The **specifications** for the project as mentioned at: https://cs50.harvard.edu/ai/2020/projects/6/parser/
### Specification
Complete the implementation of **preprocess** and **np_chunk**, and complete the context-free grammar rules defined in **NONTERMINALS**.

• The preprocess function should accept a sentence as input and return a lowercased list of its words.
1. You may assume that sentence will be a string.
2. You should use nltk’s word_tokenize function to perform tokenization.
3. Your function should return a list of words, where each word is a lowercased string.
4. Any word that doesn’t contain at least one alphabetic character (e.g. . or 28) should be excluded from the returned list.

• The **NONTERMINALS** global variable should be replaced with a set of context-free grammar rules that, when combined with the rules in TERMINALS, allow the parsing of all sentences in the sentences/ directory.
1. Each rules must be on its own line. Each rule must include the -> characters to denote which symbol is being replaced, and may optionally include | symbols if there are multiple ways to rewrite a symbol.
2. You do not need to keep the existing rule S -> N V in your solution, but your first rule must begin with S -> since S (representing a sentence) is the starting symbol.
3. You may add as many nonterminal symbols as you would like.
4. Use the nonterminal symbol NP to represent a “noun phrase”, such as the subject of a sentence.

• The **np_chunk** function should accept a tree representing the syntax of a sentence, and return a list of all of the noun phrase chunks in that sentence.
1. For this problem, a “noun phrase chunk” is defined as a noun phrase that doesn’t contain other noun phrases within it. Put more formally, a noun phrase chunk is a subtree of the original tree whose label is NP and that does not itself contain other noun phrases as subtrees.
<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;•	For example, if "the home" is a noun phrase chunk, then "the armchair in the home" is not a noun phrase chunk, because the latter contains the former as a subtree.
2. You may assume that the input will be a nltk.tree object whose label is S (that is to say, the input will be a tree representing a sentence).
3. Your function should return a list of nltk.tree objects, where each element has the label NP.
4. You will likely find the documentation for nltk.tree helpful for identifying how to manipulate a nltk.tree object.

A video Demonstrating the Functionality of this Project and be found at: https://youtu.be/vOVqJ-0J5h8

## Questions
Write an AI to answer questions.

Question Answering (QA) is a field within natural language processing focused on designing systems that can answer questions. Among the more famous question answering systems is Watson, the IBM computer that competed (and won) on Jeopardy!. A question answering system of Watson’s accuracy requires enormous complexity and vast amounts of data, but in this problem, we’ll design a very simple question answering system based on inverse document frequency.

Our question answering system will perform two tasks: document retrieval and passage retrieval. Our system will have access to a corpus of text documents. When presented with a query (a question in English asked by the user), document retrieval will first identify which document(s) are most relevant to the query. Once the top documents are found, the top document(s) will be subdivided into passages (in this case, sentences) so that the most relevant passage to the question can be determined.

How do we find the most relevant documents and passages? To find the most relevant documents, we’ll use tf-idf to rank documents based both on term frequency for words in the query as well as inverse document frequency for words in the query. Once we’ve found the most relevant documents, there many possible metrics for scoring passages, but we’ll use a combination of inverse document frequency and a query term density measure (described in the Specification).

More sophisticated question answering systems might employ other strategies (analyzing the type of question word used, looking for synonyms of query words, lemmatizing to handle different forms of the same word, etc.) but we’ll leave those sorts of improvements as exercises for you to work on if you’d like to after you’ve completed this project!

The **specifications** for the project as mentioned at: https://cs50.harvard.edu/ai/2020/projects/6/questions/
### Specification

Complete the implementation of **load_files**, **tokenize**, **compute_idfs**, **top_files**, and **top_sentences** in questions.py.

• The **load_files** function should accept the name of a directory and return a dictionary mapping the filename of each .txt file inside that directory to the file’s contents as a string.
1. Your function should be platform-independent: that is to say, it should work regardless of operating system. Note that on macOS, the / character is used to separate path components, while the \ character is used on Windows. Use os.sep and os.path.join as needed instead of using your platform’s specific separator character.
2. In the returned dictionary, there should be one key named for each .txt file in the directory. The value associated with that key should be a string (the result of reading the corresonding file).
3. Each key should be just the filename, without including the directory name. For example, if the directory is called corpus and contains files a.txt and b.txt, the keys should be a.txt and b.txt and not corpus/a.txt and corpus/b.txt.

• The **tokenize** function should accept a document (a string) as input, and return a list of all of the words in that document, in order and lowercased.
1. You should use nltk’s word_tokenize function to perform tokenization.
2. All words in the returned list should be lowercased.
3. Filter out punctuation and stopwords (common words that are unlikely to be useful for querying). Punctuation is defined as any character in string.punctuation (after you import string). Stopwords are defined as any word in nltk.corpus.stopwords.words("english").
4. If a word appears multiple times in the document, it should also appear multiple times in the returned list (unless it was filtered out).

• The **compute_idfs** function should accept a dictionary of documents and return a new dictionary mapping words to their IDF (inverse document frequency) values.
1. Assume that documents will be a dictionary mapping names of documents to a list of words in that document.
2. The returned dictionary should map every word that appears in at least one of the documents to its inverse document frequency value.
3. Recall that the inverse document frequency of a word is defined by taking the natural logarithm of the number of documents divided by the number of documents in which the word appears.

• The **top_files** function should, given a query (a set of words), files (a dictionary mapping names of files to a list of their words), and idfs (a dictionary mapping words to their IDF values), return a list of the filenames of the the n top files that match the query, ranked according to tf-idf.
1. The returned list of filenames should be of length n and should be ordered with the best match first.
2. Files should be ranked according to the sum of tf-idf values for any word in the query that also appears in the file. Words in the query that do not appear in the file should not contribute to the file’s score.
3. Recall that tf-idf for a term is computed by multiplying the number of times the term appears in the document by the IDF value for that term.
4. You may assume that n will not be greater than the total number of files.

• The **top_sentences** function should, given a query (a set of words), sentences (a dictionary mapping sentences to a list of their words), and idfs (a dictionary mapping words to their IDF values), return a list of the n top sentences that match the query, ranked according to IDF.
1. The returned list of sentences should be of length n and should be ordered with the best match first.
2. Sentences should be ranked according to “matching word measure”: namely, the sum of IDF values for any word in the query that also appears in the sentence. Note that term frequency should not be taken into account here, only inverse document frequency.
3. If two sentences have the same value according to the matching word measure, then sentences with a higher “query term density” should be preferred. Query term density is defined as the proportion of words in the sentence that are also words in the query. For example, if a sentence has 10 words, 3 of which are in the query, then the sentence’s query term density is 0.3.
4. You may assume that n will not be greater than the total number of sentences.

A video Demonstrating the Functionality of this Project and be found at: https://youtu.be/0o918afhEdE
