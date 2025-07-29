A technique to transform data into a lower dimensional space, so that similarity can be easily measured on the transformed data.

We use embedding to figure out how similar datapoints are to each other, eg to categorise like movies. This is done by *embedding* the datapoints into a low-dimensional space created such that similar datapoints are nearby. Helpful in dealing with [[Sparse Tensors]].

> "An embedding is a matrix in which each column is the vector that corresponds to an item in your vocabulary. To get the dense vector for a single vocabulary item, you retrieve the column corresponding to that item." 

## Wowee, how magical, but how do we obtain this mythical embedding?

Weeeell, if we're specifically looking at word embeddings we can use Google's infamous word2vec algorithm. Which trains [[Neural Networks (NN)]] to distinguish co-occuring groups of words from randomly grouped words, but part of this process is that once the model is trained you actually have an embedding.

Other embeddings can be found using different algorithms.


See also:
- [[Multi-Class Neural Networks]]
- [[Matrix Multiplication]]
- [[Data Preparation]]
- https://www.tensorflow.org/tutorials/word2vec/index.html