# NLP

## Fields

### Text classification
- Sentence-level
- Document-level

Sentence-level: Convolutional Neural Networks for Sentence Classification
code: https://github.com/dennybritz/cnn-text-classification-tf

## Concepts

### Stemming and Lemmatization
Stemming and lemmatization are normalizing techniques used to minimize the structural variation of words. 

- Stemming: **removes** the affixes added to the word and leaves it in base form. (Just a part)
- Lemmatization: **converts** the word into its lemma form as a root word. (still a word)


### Beam search
it is aim to find the most likely sequence of words, given a probabilistic model (such as a language model). 
It is an optimization over the simpler greedy search and exhaustive search methods, aiming to balance between search accuracy and computational efficiency. 

It only keeps B (beam-width) most likely candidates with there probablities in memory during the search.