hobbs.py
________

Enter `python hobbs.py demo` to see a demo.

Otherwise, enter a file containing parsed sentences to search, with
one sentence per line, and then enter the pronoun you'd like to resolve, e.g., 

	python hobbs.py demosents.txt "He"
	python hobbs.py demosents.txt "it"
	python hobbs.py demorefl.txt "herself"

The sentences must use Treebank tags and be parsed such that they can be converted into
NLTK Trees. The pronoun must be in the last sentence of the file.

This program uses Hobbs’ algorithm to find the antecedent of a pronoun.
It has also been expanded to handle reflexive pronouns. The algorithm is given below:

1.	Begin at the NP node immediately dominating the pronoun
2.	Go up the tree to the first NP or S node encountered. 
	Call this node X and the path used to reach it p.
3.	Traverse all branches below node X to the left of path p in a
	left-to-right, breadth-first fashion. Propose as an antecedent
	any NP node that is encountered which has an NP or S node between
	it and X. 
4.	If node X is the highest S node in the sentence, traverse the
	surface parse trees of previous sentences in the text in order of
	recency, the most recent first; each tree is traversed in a
	left-to-right, breadth-first manner, and when an NP node is 
	encountered, it is proposed as an antecedent. If X is not the highest
	S node in the sentence, continue to step 5.
5.	From node X, go up the tree to the first NP or S node encountered. 
	Call this new node X, and call the path traversed to reach it p. 
6.	If X is an NP node and if the path p to X did not pass through the 
	Nominal node that X immediately dominates, propose X as the antecedent.
7.	Traverse all branches below node X to the left of path p in a 
	left-to-right, breadth-first manner. Propose any NP node encountered 
	as the antecedent.
8.	If X is an S node, traverse all the branches of node X to the right 
	of path p in a left-to-right, breadth-first manner, but do not go 
	below any NP or S node encountered. Propose any NP node encountered 
	as the antecedent. 
9.	Go to step 4. 

Hobb’s Naїve Algorithm For Hindi
Based on the observations in previous section, we have adapted
to Hindi.
Hobbs Naïve Algorithm so that it can be applied
1. Begin at the NP node, which immediately dominates a pronoun ‘veh’, ‘yeh’, ‘uska/uski/uske’ or ‘apna/apne/apnii’.
If NP node immediately dominates a pronoun, continue to step 3.
2. Go up the tree to the first NP or VP node encountered. Call this node X and call the path used to reach it p.
3. If the pronoun is ‘apna/apnii/apne’, continue to step 6.
4. If X is an NP node of the Direct Object, traverse all branches below node X to the left of path p in a left-to-right,
breadth-first fashion. Propose as the antecedent any accusative NP node or nominative NP node, which is immediately
dominated by X, or propose as the antecedent any accusative NP node or nominative NP node that is encountered
which has an NP, VP or S node between it and X.
5. If X is an NP node of the Subject, traverse all branches below node X to the left of path p in a left-to-right, breadth-
first fashion. Propose as the antecedent any dative NP node, which is immediately dominated by X, or propose as the
antecedent any dative NP node that is encountered which has an NP, VP or S node between it and X.
6. From node X go up the tree to the first NP, VP or S node encountered. Call this new node X, and the path traversed to
reach it p. If X is an NP node or a VP node, continue to step 3. If X is an S node, continue to step 7.
7. If the pronoun is “apna/apne/apnii”, the antecedent is a dative, ergative or nominative case-marked NP node
preceding it or used later on in the sentence.
If the pronoun is not “apna/apne/apnii”, continue to step 8.8. If node X is the highest S node in the sentence, traverse the surface parse trees of previous sentences in the text in
order of recency, the most recent first; each tree is traversed in a left-to-right, breadth-first manner, and when an NP
node is encountered, it is proposed as the antecedent. If X is not the highest S node in the sentence, continue to step 9.
9. From node X, go up the tree to the first NP, VP or S node encountered. Call this new node X, and call the path
traversed to reach it p.
10. If X is an NP node and if the path p to X did not pass through the Nbar node that X immediately dominates, propose
X as the antecedent.
11. If X is an NP node and if the path p passed through the N-bar node that X immediately dominates, traverse all
branches below node X to the left of path p in a left-to-right, breadth-first manner. Propose any NP node encountered as
the antecedent.
12. If X is a VP or S node, traverse all branches of node X to the right of path p in left-to-right, breadth-first manner, but
do not go below any NP or VP or S node encountered. Propose any NP node encountered as the antecedent.
13. Go to step 8.
A tree is traversed in breadth-first search manner where every node of depth n is visited before any node of depth
n-1. Steps 3 and 7 of the algorithm take care of the level in the tree where a reflexive pronoun w


