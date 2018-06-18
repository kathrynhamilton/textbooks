# W266 - Natural Language Processing

## 1 - Introduction

## 2 - Classification and Sentiment

### Course Content

#### Sentiment Analysis

Sentiment Analysis is computationally identifying and categorizing opinions expressed in a piece of text, especially in order to determine the writer's attitude towards a particular topic.

Reviews are a good way to explore sentiment and text understanding.

Scherer Typology of Affective States:

- **Emotion**, brief feeling
- **Mood**, low intensity and long duration
- **Interpersonal**, stance toward another person
- **Attitude**, enduring beliefs towards objects or persons
- **Personality traits**, stable dispositions and typical behavior

Sentiment analysis detects **attitudes**.

Some common terms:

- **Holder** (source) of attitude
- **Target** (aspect) of attitude
- **Type** of attitude (like, love, hate, value, desire, etc. or more simply a weighted polarity of good or bad)
- **Text** containing attitude

Kinds of Sentiment Analysis:

- **Polarity task**, is attitude positive, negative, or neutral?
- **Subjectivity vs objectivity task**, phrases that are influenced and not influenced by attitude
- **Feature/aspect task**, associate attitude with a particular aspect (price, ease of use, setup, etc.)
- **Contextual task**, detect source of attitude

Removing nonsubjective phrases can improve the accuracy of a polarity classifier.

**Sentiment Lexicons** assign general sentiment to words outside of context. They can be used as a mapping of individual words to typical sentiment. Some examples are: *General Inquirer*, *LIWC*, *MPQA*, *Bing Liu Opinion Lexicon*, *SentiWordNet*. There is a wide range of dissagreement between these lexicons.

#### Convolutional Neural Networks for NLP

Combining machine learning models that take different approaches or try to solve different projects is typically a good way to go. You can **create multiple classifiers and weigh their outputs**. 

Additionally, **layering different processes** for example as a neural network, also works well as natural language processing is a multi-dimensional problem. Layering can be effective as it is similar yo how humans perceive text: evaluating individual word sentiment along with context, negations, idioms, and meaning taken over the length of numerous sentences.

**Pooling layers**, such as a maximum layer, are a way to highlight the most relevant information. We can also use convulational filters, which use sliding filters

**Activation Function: p = tanh(W\*C + b)** where *tanh* is a nonlinearity, *W* is an NxD parameter matrix, *C* is a Dx1 embedding vector, *b* is a bias term, *N* is the n-gram size, and *D* is the embedding dimention

<p align="center">
  <img src="https://github.com/kathrynhamilton/textbooks/blob/master/MachineLearning/images/2.8%20image.png" width="500">
</p>

### Readings

## 3 - Language Modeling I

### Course Content

#### Noisy Channel Model

 Consider the problem of next word prediction on phone keyboards. We want to estimate `P(word | context)`. Things to consider:
 
 - context: who is typing, where and when they are typing, what has been typed before
 - phone memory: affects vocabulary size, character sets (some languages have large alphabets)
 - inference speed/latency: needs to be fast enough to be useful
 - internationalization: adapt one model be adapted to multiple languages, allow for multiple languages to be used together
 
 The "correct" word sequence maximizes `P(word sequence | keystrokes)`. Using Bayes rule, this is approximately equivalent to maximizing `P(keystrokes | word sequence) * P(word sequence)`. This is called the **noisy channel model**.
 
 It turns out we need two models:
 
 1. *Keystroke model* `P(keystrokes | word sequence)`, which scores letters based on screen taps
 2. *Language model* `P(word sequence)`, which scores word sequences based on how realistic they are
 
Now let's look at the model applied to a generic translation problem. The correct English translation given a sequence of words in French maximizes `P(English Sequence | French sequence) =~ P(French sequence | English sequence) * P(English sequence)`.

Again, we have two models:

 1. *Translation model* `P(French sequence | English sequence)`, which scores French translation given an English sequence
 2. *Language model* `P(English sequence)`, which scores English sequences based on how realistic they are
 
 The noisy channel model works in many other applications, for example:
 
 * Speech Recognition: `P(words | audio) =~ P(audio | words) * P(words)`
 * Optical character recognition: `P(character | pixels) =~ P(pixels | character) * P(character)`
 * Spelling correction: `P(word | character sequence) =~ P(character sequence | word) * P(word)`
 * Handwriting recognition: `P(word or letters | pixels) =~ P(pixels | word or letter) * P(word or letter)`
 
#### N-Gram Language Modelling

Language models assign useful (indicating plausibility and not grammaticallity) probabilities `P(x)` to sentences `x`. There is a lot of free text on the internet (corpuses) and from other sources that we can give to these models as training data.

`P(wn) = P(w0) P(w1|w0) P(w2|w1, w0)...P(wn|wn-1,...w0)` has a sparsity restriction. How likely is it that this specific sentence is in the training set?

So we use the Markov assumption, knowing that it is wrong, to make an estimation:

* Unigram: `P(w1, w2,..., wn) = Π P(wi)`
* Bigram: `P(w1, w2,..., wn) = Π P(wi|wi-1)`
* Trigram: `P(w1, w2,..., wn) = Π P(wi|wi-1, wi-2)`

Unigram models are not great because `P(the the the the)` is greater than basically all other probabilities. 

Word-based Language models can be very large; the average adult english vocabulary is 30k words. Word-based N-grams that require a high N, to look back at previous words for context, are computationally intensive.

We could also try character-based N-grams because the vocabulary is very small, A to Z. This might also work well with small morphological components like -ing, -ed, etc. However, character-based N-grams are not good at predicting the next word.

#### Measuring Quality

We don't want to generate fake text. We want generated sentences to improve as we increase order (so long as we don't overfit). A bad sentence doesn't mean ungrammatical. It means an unlikely sentence, a sentence we know is wrong but that the translation model likes.

We can use entropy of the distribution of possible predicted words to measure how good the language model is. An improvement of 0.1 bits is impressive. The solution here is **perplexity*: `perp(X,Θ) = 2^{H(X|Θ)}` where `X` is a sentence and `Θ` is a language model. Lower perplexity is better. The best possible perplexity is 1, where entropy would be 0 as there is no uncertainty in the next word.

Extrinisic evaluation is also possible. For example, we might use *word error rate* to assess a speech to text converter. It assesses the difference between a recognized sentence and the true sentence in terms of normalized number of insertions, deletions, and substitutions.

#### Smoothing

We want to make estimates from spare statistics. What if, in the whole corpus, we only have a handful of observations for a certain P(w3|w1,w2)? We smooth by flattening spikey distributions for better generalization. We reduce the amount of probability mass from things that we have seen and distributed it on things that we have not seen.

Typically, we run into the following problems if the corpus is not large enough:

* known words in unknown contexts
* unknown words

To combat this, we aim to use higher-order n-grams when possible, and lower-order n-grams when necessary.

Some common smoothing methods:

* Use a larger corpus
* **Katz smoothing**: If count of history is less than some threshold, then reduce size of N in N-gram. Can have different thresholds for different N's.
* **Interpolation**: Use a weighted combination of uni-, bi- and tri-gram probabilities
* **Laplace Smoothing**: Choose a small number and add it to all of the counts.
* **Unknowns**: Lump n-grams that don't have probability into a single entry called unknown. Or even better, draw an inference from the letters
* **Kneser-Ney**: Considers frequency of unigram in relation to possible words preceding it. It is widely considered the most effective.

Other smoothing ideas:

* **Word classes**: noun, verb, adjective, name, place, animal, etc.
* **Caching model**: recent words are more likely to appear again.
* **Trigger/topic model**: some words are triggers for others, or the entire passage relates to a particular topic.
* **Structural zeros**: some n-grams should never appear, eg. "the the". Gives these P(w) = 0, even for example in Laplace smoothing where we might artifically add probability mass.
* **Syntactic models**: syntax trees that capture long-range dependencies, ie. conditioning or sentence structure

### Readings

## 4 - Clusters and Distributions

### Course Content

Relationships among words are poorly modeled. How can we more accurately express the meaning of words? How can we learn these representations from the data?

#### WordNet

Goal: a lexical database that aimed to be a machine-readable combination of a dictionary and a thesaurus. This consists of:

* synsets, grouping of words that are synonymous in a particular context
* semantic relations, which connect synsets. For example: hypernym (class, eg. canine is a hypernym of dog) and hyponym (specific instance, eg. dog is a hyponym of canine)

Unfortunately, WordNet is only available in English, requires lots of manual labor, assumes that words in a synset are precisely equivalent, and has a hard time incorporating new words or usages.

#### Distributional Similarity

Goal: Represent a word by statistical properties of its context. There are several important ideas here:

* cluster words based on their context (Brown clustering algorithm)
* use co-occurence matrix representation (Latent semantic analysis)
* Train a model that predicts context words (word2vec, continuous bag-of-words, skip-gram)

#### Brown Clustering

Similar words appear in similar contexts. By trying to match distributions of words to the immediate left and right, Brown Clustering:

* Partitions/Clusters words into classes, which are words appearing in similar contexts. Each word can only be in one cluster.
* Provides hierarchical clustering of words

The Brown Clustering model is as follows:

* **Vocabulary** `V = w1, w2,..., wn`, the set of all words in the corpus. 
* **Partition function** `C`, that maps vocabulary `V` into classes `{1, 2,..., k}`. `k` is typically about 1000.
* **Emission probability** `e`, where `e(w1 | 2)` is the probability `class 1` emits the word `w1`.
* **Transition probability** `q`, where `q(3 | 5)` is the probability of transitioning from a word in `class 5` to a word in `class 3` (ie. `<5>` precedes `<3>`).

We have `p(w1, w2,...,wt) =  ∏ e(wi|C(wi)) * q(C(wi)|C(wi-1))` where `C(w)` is the cluster/class of `w`. We want to choose `C` that maximizes the courpus.

The quality of a given partition is `Quality(C) = ∑ log e(wi|C(wi)) * q(C(wi)|C(wi-1))`. This is an equivalent metric to mutual information between classes, `∑ p(c,c') * log p(c,c')/(p(c)p(c'))`, which is an indicator of how much `c` tells us about `c'`.

A slow algorithm, O(|V|^5):

1. Start with `|V|` clusters, each word by itself
2. Try to merge all pairs of clusters and pick the merge that maximizes `Quality(C)`
3. Repeat (2) until desired number of clusters, `|V|-k` times
4. Repeat (2) until all clusters merge and a heirarchy is formed

A faster algorithm, O(|V|m^2), and the one that is most commonly used in practice:

1. Start with the `m` most popular words each in their own cluster
2. Take an unclustered word and make a new cluster for it (there are now `m+1` clusters)
3. Try to merge all pairs of clusters and pick the merge that maximized `Quality(C)` (there are now `m` clusters)
4. Repeat (2), (3) until all words are in a cluster
5. Repeat (3) until all clusters merge and a heirarchy is formed

Clusters can help make use of large, unlabeled datasets and understand rare words. However, clustering representation is not the best for NLP, for example because each word can only appear in one cluster. We can correct this with a co-occurrence matrix: a matrix with both a column and a row for each word in the vocabulary, where entries are a count of how many times a pair of words appears in the same sentence. We can also use Pearson correlations instead of counts, setting negative numbers to zero, to reduce the impact of very common words.

Co-occurence matrices are sparse, so we represent them more densely using Singular Value Decomposition:
$X_{n,m} = U_{n,r} S_{r,r} V^T_{r,m}$

<p align="center">
  <img src="https://github.com/kathrynhamilton/textbooks/blob/master/MachineLearning/images/svd.png" width="500">
</p>

We choose $r$ to an appropriate number of components and then we can use columns of $U$ as word vectors. We can plot these and use them to make word clusters. SVD can be quite computationally expensive, O(n^3) as the co-occurence matrix needs to be inverted.

Choose co-occurence count window: smaller windows capture more syntax, larger windows capture more semantics. LSA uses whole documents. Typically, window is [-5,5] words.

Word2Vec architectures:

* CBOW (Continuous Bag of Words)
* Skip-gram

<p align="center">
  <img src="https://github.com/kathrynhamilton/textbooks/blob/master/MachineLearning/images/cbowsg.png" width="500">
</p>

Skip-gram maximizes the probability of context words in a window of length $m$ given a center word. The input words predicts an output word when the product of their vector representations is large. Skip-gram is better at capturing semantic relationships.

CBOW uses the average vector representation of context words to predict the center word. CBOW is better are capturing syntactic relationships.

### Readings

## 5 - Language Modelling II

The meaning of a word can be summarized with statistical properties of context (words around it), for example by using Brown's algorithm, co-occurence matrices, or word-2-vec.

What can we do with word vectors?

Classification

We have: a training dataset containing samples $(xi, yi)$ of inputs and labels for $i$ in $1,\dots,N$
What if: we make the label the next word(s)?

Softmax (Logistic Regression)

Creates linear boundaries, which is good for little data, but not good for large amounts of data.

$p(y|x) = \frac{\exp{W_y*x}}{\sum_c \exp{W_c*x}}$ for classes $y, c$ in $1,...,C$
Loss function over the dataset: $J(\theta) = - \frac{1}{N} \sum_i \log \frac{e^{W_{y_i}x}}{\sum_i e^{W_{c}x}+\lambda \sum \theta_k^2$ where $\lambda \sum \theta_k^2$ is a regularization term to reduce overfitting, and $\theta$ is a parameter of the model, aka an entry in $W$.

Neural Networks

Neural networks can learn complex, non-linear decision boundaries.

A single neuron computes $h_{w,b}(x) = f(Wx+b), where the neuron will fire or not fire given the result of the activation function $f$. 

<p align="center">
  <img src="https://github.com/kathrynhamilton/textbooks/blob/master/MachineLearning/images/neuron.png" width="500">
</p>

A neural network runs many logistic regressions (layers) at the same time, where in each layer, $a=f(Wx+b)$.

<p align="center">
  <img src="https://github.com/kathrynhamilton/textbooks/blob/master/MachineLearning/images/neuralnetwork.png" width="350">
</p>

Rather than using a step function as the activation function, we typically use a sigmoid function (because it's continuous), $f(z) = frac{1}{1+e^{-z}}$. Alternatively, $tanh(x) = 2\sigma(2x)-1$ and $reLU(x)=max(0,x)$ are popular.

Without non-linear functions, deep neural networks can only learn linear tansforms (ie. linear algebra because all that happens is combinations of matrices). 

Here is an example feedforward neural network using a vocabulary of 8 words, and resulting in a 4x1 matrix listing the probabilities of *Paris* being in each of the four classes (PER, POC, PRG, NON).

<p align="center">
  <img src="https://github.com/kathrynhamilton/textbooks/blob/master/MachineLearning/images/feedforward.png" width="500">
</p>

Training a neural network is a an extension of training logistic regression:

1. Initialize Parameters
2. Run model on a set of data to acquire output
3. Calculate error
4. Back propogate error to update parameters
5. Repeat until error is sufficiently small

We want to maximize the log-likelihood of parameters (ar alternatively as a cost function, minimize the negative log-likelihood).
In neural network training, cross-entropy loss (from information theory) is the same as log-likelihood loss (from probability theory).

Cross-entropy

Consider a classification problem where the correct distribution over four classes is [0,0,1,0] and the predicted disrribution is [0.1,0.4,0.3,0.2]. Cross entropy is $H(p,q)=-\sum_c p(c) \log q(c)=H(p)+D_{KL}(p||q)$.

$D_{KL}(p||q)$, KL divergence, is a nonsymmetric measure of the difference between p and q.

Language Models

For n-gram language models using lots of data and smoothing techniques, 5-gram models were nearly impossible to beat. However, there were still problems with long-range dependencies and sparsity.

With neural network language models, we predict the current word given the previous k words. We use a hidden layer to reduce the dimensionality of the context. We need to make everything efficient enough to train with lots of data.

Dimensions:
* V - vocabulary size
* M - embedding size
* N - window size (words of context)
* H - hidden units 

Parameters
* Embeddings C: [V,M]
* Hidden layer W1: [NxM,H]
* Output layer: W2:[H,V]

Heirarchical Softmax

Form a tree in which every leaf is a word in the vocabulary. $p(w)$ is a product of the probability of the word's parents in the tree.
At each node we can evaluate the probability of branching left or right given the hidden state h. Heirarchical softmax is mostly used to speed up training.

### Course Content

### Readings

## 6 - Units of Meaning: Words, Morphology, Sentences

### Course Content

### Readings

## 7 - Parts-of-Speech Tagging I

### Course Content

### Readings

## 8 - Parts-of-Speech Tagging II

### Course Content

### Readings

## 9 - Parsing I

### Course Content

### Readings

## 10 - Parsing II

### Course Content

### Readings

## 11 - Information Retrieval

### Course Content

### Readings

## 12 - Entities

### Course Content

### Readings

## 13 - Machine Translation I

### Course Content

### Readings

## 14 - Machine Translation II

### Course Content

### Readings

## 15 - Summarization

### Course Content

### Readings
