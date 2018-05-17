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

We can use entropy of the distribution of possible predicted words to measure how good the language model is. An improvement of 0.1 bits is impressive. The solution here is *perplexity*: `perp(X,Θ) = 2^{H(X|Θ)}` where `X` is a sentence and `Θ` is a language model. Lower perplexity is better. The best possible perplexity is 1, where entropy would be 0 as there is no uncertainty in the next word.

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

### Readings

## 4 - Clusters and Distributions

### Course Content

### Readings

## 5 - Language Modelling II

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
