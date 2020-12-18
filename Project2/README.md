# PageRank and Heredity
### PageRank
When search engines like Google display search results, they do so by placing more “important” and higher-quality pages higher in the search results than less important pages. But how does the search engine know which pages are more important than other pages?

One heuristic might be that an “important” page is one that many other pages link to, since it’s reasonable to imagine that more sites will link to a higher-quality webpage than a lower-quality webpage. We could therefore imagine a system where each page is given a rank according to the number of incoming links it has from other pages, and higher ranks would signal higher importance.

But this definition isn’t perfect: if someone wants to make their page seem more important, then under this system, they could simply create many other pages that link to their desired page to artificially inflate its rank.

For that reason, the PageRank algorithm was created by Google’s co-founders (including Larry Page, for whom the algorithm was named). In PageRank’s algorithm, a website is more important if it is linked to by other important websites, and links from less important websites have their links weighted less. This definition seems a bit circular, but it turns out that there are multiple strategies for calculating these rankings.

The **specifications** for the project as mentioned at: https://cs50.harvard.edu/ai/2020/projects/2/pagerank/
### Specification
Complete the implementation of **transition_model**, **sample_pagerank**, and **iterate_pagerank**.

The **transition_model** should return a dictionary representing the probability distribution over which page a random surfer would visit next, given a corpus of pages, a current page, and a damping factor.

•	The function accepts three arguments: corpus, page, and damping_factor.
1. The corpus is a Python dictionary mapping a page name to a set of all pages linked to by that page.
2. The page is a string representing which page the random surfer is currently on.
3. The damping_factor is a floating point number representing the damping factor to be used when generating the probabilities.

•	The return value of the function should be a Python dictionary with one key for each page in the corpus. Each key should be mapped to a value representing the probability that a random surfer would choose that page next. The values in this returned probability distribution should sum to 1.
1. With probability damping_factor, the random surfer should randomly choose one of the links from page with equal probability.
2. With probability 1 - damping_factor, the random surfer should randomly choose one of all pages in the corpus with equal probability.

•	For example, if the corpus were {"1.html": {"2.html", "3.html"}, "2.html": {"3.html"}, "3.html": {"2.html"}}, the page was "1.html", and the damping_factor was 0.85, then the output of transition_model should be {"1.html": 0.05, "2.html": 0.475, "3.html": 0.475}. This is because with probability 0.85, we choose randomly to go from page 1 to either page 2 or page 3 (so each of page 2 or page 3 has probability 0.425 to start), but every page gets an additional 0.05 because with probability 0.15 we choose randomly among all three of the pages.

•	If page has no outgoing links, then transition_model should return a probability distribution that chooses randomly among all pages with equal probability. (In other words, if a page has no links, we can pretend it has links to all pages in the corpus, including itself.)


The **sample_pagerank** function should accept a corpus of web pages, a damping factor, and a number of samples, and return an estimated PageRank for each page.

•	The function accepts three arguments: corpus, a damping_factor, and n.
1. The corpus is a Python dictionary mapping a page name to a set of all pages linked to by that page.
2. The damping_factor is a floating point number representing the damping factor to be used by the transition model.
3. n is an integer representing the number of samples that should be generated to estimate PageRank values.

•	The return value of the function should be a Python dictionary with one key for each page in the corpus. Each key should be mapped to a value representing that page’s estimated PageRank (i.e., the proportion of all the samples that corresponded to that page). The values in this dictionary should sum to 1.

•	The first sample should be generated by choosing from a page at random.

•	For each of the remaining samples, the next sample should be generated from the previous sample based on the previous sample’s transition model.
1. You will likely want to pass the previous sample into your transition_model function, along with the corpus and the damping_factor, to get the probabilities for the next sample.
2. For example, if the transition probabilities are {"1.html": 0.05, "2.html": 0.475, "3.html": 0.475}, then 5% of the time the next sample generated should be "1.html", 47.5% of the time the next sample generated should be "2.html", and 47.5% of the time the next sample generated should be "3.html".
3. You may assume that n will be at least 1.

The **iterate_pagerank** function should accept a corpus of web pages and a damping factor, calculate PageRanks based on the iteration formula described above, and return each page’s PageRank accurate to within 0.001.

•	The function accepts two arguments: corpus and damping_factor.
1. The corpus is a Python dictionary mapping a page name to a set of all pages linked to by that page.
2. The damping_factor is a floating point number representing the damping factor to be used in the PageRank formula.

•	The return value of the function should be a Python dictionary with one key for each page in the corpus. Each key should be mapped to a value representing that page’s PageRank. The values in this dictionary should sum to 1.

•	The function should begin by assigning each page a rank of 1 / N, where N is the total number of pages in the corpus.

•	The function should then repeatedly calculate new rank values based on all of the current rank values, according to the PageRank formula in the “Background” section. (i.e., calculating a page’s PageRank based on the PageRanks of all pages that link to it).
1. A page that has no links at all should be interpreted as having one link for every page in the corpus (including itself).

•	This process should repeat until no PageRank value changes by more than 0.001 between the current rank values and the new rank values.


A video Demonstrating the Functionality of this Project and be found at: https://youtu.be/fodBEsP6cE4

# Heredity
Mutated versions of the GJB2 gene are one of the leading causes of hearing impairment in newborns. Each person carries two versions of the gene, so each person has the potential to possess either 0, 1, or 2 copies of the hearing impairment version GJB2. Unless a person undergoes genetic testing, though, it’s not so easy to know how many copies of mutated GJB2 a person has. This is some “hidden state”: information that has an effect that we can observe (hearing impairment), but that we don’t necessarily directly know. After all, some people might have 1 or 2 copies of mutated GJB2 but not exhibit hearing impairment, while others might have no copies of mutated GJB2 yet still exhibit hearing impairment.

Every child inherits one copy of the GJB2 gene from each of their parents. If a parent has two copies of the mutated gene, then they will pass the mutated gene on to the child; if a parent has no copies of the mutated gene, then they will not pass the mutated gene on to the child; and if a parent has one copy of the mutated gene, then the gene is passed on to the child with probability 0.5. After a gene is passed on, though, it has some probability of undergoing additional mutation: changing from a version of the gene that causes hearing impairment to a version that doesn’t, or vice versa.

We can attempt to model all of these relationships by forming a Bayesian Network of all the relevant variables, as in the one below, which considers a family of two parents and a single child.

The **specifications** for the project as mentioned at: https://cs50.harvard.edu/ai/2020/projects/2/heredity/
### Specification
Complete the implementations of **joint_probability**, **update**, and **normalize**.

The **joint_probability** function should take as input a dictionary of people, along with data about who has how many copies of each of the genes, and who exhibits the trait. The function should return the joint probability of all of those events taking place.

•	The function accepts four values as input: people, one_gene, two_genes, and have_trait.
1. people is a dictionary of people as described in the “Understanding” section. The keys represent names, and the values are dictionaries that contain mother and father keys. You may assume that either mother and father are both blank (no parental information in the data set), or mother and father will both refer to other people in the people dictionary.
2. one_gene is a set of all people for whom we want to compute the probability that they have one copy of the gene.
3. two_genes is a set of all people for whom we want to compute the probability that they have two copies of the gene.
4. have_trait is a set of all people for whom we want to compute the probability that they have the trait.
5. For any person not in one_gene or two_genes, we would like to calculate the probability that they have no copies of the gene; and for anyone not in have_trait, we would like to calculate the probability that they do not have the trait.

•	For example, if the family consists of Harry, James, and Lily, then calling this function where one_gene = {"Harry"}, two_genes = {"James"}, and trait = {"Harry", "James"} should calculate the probability that Lily has zero copies of the gene, Harry has one copy of the gene, James has two copies of the gene, Harry exhibits the trait, James exhibits the trait, and Lily does not exhibit the trait.

•	For anyone with no parents listed in the data set, use the probability distribution PROBS["gene"] to determine the probability that they have a particular number of the gene.

•	For anyone with parents in the data set, each parent will pass one of their two genes on to their child randomly, and there is a PROBS["mutation"] chance that it mutates (goes from being the gene to not being the gene, or vice versa).

•	Use the probability distribution PROBS["trait"] to compute the probability that a person does or does not have a particular trait.

The **update** function adds a new joint distribution probability to the existing probability distributions in probabilities.

•	The function accepts five values as input: probabilities, one_gene, two_genes, have_trait, and p.
1. probabilities is a dictionary of people as described in the “Understanding” section. Each person is mapped to a "gene" distribution and a "trait" distribution.
2. one_gene is a set of people with one copy of the gene in the current joint distribution.
3. two_genes is a set of people with two copies of the gene in the current joint distribution.
4. have_trait is a set of people with the trait in the current joint distribution.
5. p is the probability of the joint distribution.

•	For each person person in probabilities, the function should update the probabilities[person]["gene"] distribution and probabilities[person]["trait"] distribution by adding p to the appropriate value in each distribution. All other values should be left unchanged.

•	For example, if "Harry" were in both two_genes and in have_trait, then p would be added to probabilities["Harry"]["gene"][2] and to probabilities["Harry"]["trait"][True].

•	The function should not return any value: it just needs to update the probabilities dictionary.

The **normalize** function updates a dictionary of probabilities such that each probability distribution is normalized (i.e., sums to 1, with relative proportions the same).

•	The function accepts a single value: probabilities.
1. probabilities is a dictionary of people as described in the “Understanding” section. Each person is mapped to a "gene" distribution and a "trait" distribution.

•	For both of the distributions for each person in probabilities, this function should normalize that distribution so that the values in the distribution sum to 1, and the relative values in the distribution are the same.

•	For example, if probabilities["Harry"]["trait"][True] were equal to 0.1 and probabilities["Harry"]["trait"][False] were equal to 0.3, then your function should update the former value to be 0.25 and the latter value to be 0.75: the numbers now sum to 1, and the latter value is still three times larger than the former value.

•	The function should not return any value: it just needs to update the probabilities dictionary.


A video Demonstrating the Functionality of this Project and be found at: https://youtu.be/f3g2b-KyFcw
