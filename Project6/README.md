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