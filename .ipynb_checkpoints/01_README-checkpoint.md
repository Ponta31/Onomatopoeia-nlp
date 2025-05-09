# Onomatopoeia-nlp
Class project to create a model for Japanese text equivalent to onomatopoeia


I am interested in creating a model which contribute to students in Japanese class to learn Japanese onomatopoeia since Japanese language is very rich with onomatopoeia. I would try creating a model that takes in text, and returns paraphrases of the text containing onomatopoeia equivalents.

1.	Dataset
I will collect data on onomatopoeia and sentences through web scraping from these websites.

- https://nihon5-bunka.net/onomatopoeia/
- https://www2.ninjal.ac.jp/Onomatope/category.html 
- Oscar-corpus(ja) > unshuffled_original_ja  "https://huggingface.co/datasets/oscar-corpus/oscar"

3.	Modeling approach
(1) Analyze POS of the input text (spaCy)
(2) Create a vector list for the onomatopoeia and verbs/adjectives (Word2Vec)
(3) If there is a similar vector word in the onomatopoeia list with the input text, retrieve it. 
(4) Reconstruct the sentence using the onomatopoeia.

4.	GitHub Repo
https://github.com/Ponta31/Onomatopoeia-nlp.git 
