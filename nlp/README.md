# NLP

## Classic NLP tasks (古典NLP任务)

### Named Entity Recognition (NER)

Can be regarded as:
- text version of image segmentation.
- word, N-gram level classification. 
- start_index and end_index inference.

Classic problem:
- Part-of-Speech Tagging (POS Tagging)
- Structured information extraction

### Text classification
- Sentence-level
- Document-level

Sentence-level: Convolutional Neural Networks for Sentence Classification
code: https://github.com/dennybritz/cnn-text-classification-tf

Classic problem:
- Spam detection
- Sentiment analysis

### Text embedding

Mostly for similarity analysis.

### Doc2Doc

Input and output are both document. Classic problem are:
- Translation
- Summarization
- Article-based Q&A

## Concepts

### Stemming and Lemmatization
Stemming and lemmatization are normalizing techniques used to minimize the structural variation of words. 

- Stemming: **removes** the affixes added to the word and leaves it in base form. (Just a part)
- Lemmatization: **converts** the word into its lemma form as a root word. (still a word)


### Beam search
it is aim to find the most likely sequence of words, given a probabilistic model (such as a language model). 
It is an optimization over the simpler greedy search and exhaustive search methods, aiming to balance between search accuracy and computational efficiency. 

It only keeps B (beam-width) most likely candidates with there probablities in memory during the search.