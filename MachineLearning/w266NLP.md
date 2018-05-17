# W266 - Natural Language Processing

## 1 - Introduction

## 2 - Classification and Sentiment

### Course Content

**Sentiment Analysis**: computationally identifying and categorizing opinions expressed in a piece of text, especially in order to determine the writer's attitude towards a particular topic

Reviews are a good way to explore sentiment and text understanding. <br><br>

Scherer Typology of Affective States:

- **Emotion**, brief feeling
- **Mood**, low intensity and long duration
- **Interpersonal**, stance toward another person
- **Attitude**, enduring beliefs towards objects or persons
- **Personality traits**, stable dispositions and typical behavior

Sentiment analysis detects **attitudes**. <br><br>

Some common terms:

- **Holder** (source) of attitude
- **Target** (aspect) of attitude
- **Type** of attitude (like, love, hate, value, desire, etc. or more simply a weighted polarity of good or bad)
- **Text** containing attitude <br><br>

Kinds of Sentiment Analysis:

- **Polarity task**, is attitude positive, negative, or neutral?
- **Subjectivity vs objectivity task**, phrases that are influenced and not influenced by attitude
- **Feature/aspect task**, associate attitude with a particular aspect (price, ease of use, setup, etc.)
- **Contextual task**, detect source of attitude

Removing nonsubjective phrases can improve the accuracy of a polarity classifier. <br><br>

**Sentiment Lexicons** assign general sentiment to words outside of context. They can be used as a mapping of individual words to typical sentiment. Some examples are: *General Inquirer*, *LIWC*, *MPQA*, *Bing Liu Opinion Lexicon*, *SentiWordNet*. There is a wide range of dissagreement between these lexicons. <br><br>

**Convolutional Neural Networks for NLP:**

Combining machine learning models that take different approaches or try to solve different projects is typically a good way to go. You can **create multiple classifiers and weigh their outputs**. 

Additionally, **layering different processes** for example as a neural network, also works well as natural language processing is a multi-dimensional problem. Layering can be effective as it is similar yo how humans perceive text: evaluating individual word sentiment along with context, negations, idioms, and meaning taken over the length of numerous sentences.

**Pooling layers**, such as a maximum layer, are a way to highlight the most relevant information. We can also use convulational filters, which use sliding filters

**Activation Function: p = tanh(W\*C + b)** where *tanh* is a nonlinearity, *W* is an NxD parameter matrix, *C* is a Dx1 embedding vector, *b* is a bias term, *N* is the n-gram size, and *D* is the embedding dimention

<p align="center">
  <img src="https://github.com/kathrynhamilton/textbooks/blob/master/MachineLearning/images/2.8%20image.png" width="500">
</p> <br><br>

### Readings

## 3 - Language Modeling I

### Course Content

**Noisy Channel model**

 Consider the problem of next word prediction on phone keyboards. We want to estimate `P(word | context)`. Things to consider:
 
 - context: who is typing, where and when they are typing, what has been typed before
 - phone memory: affects vocabulary size, character sets (some languages have large alphabets)
 - inference speed/latency: needs to be fast enough to be useful
 - internationalization: adapt one model be adapted to multiple languages, allow for multiple languages to be used together <br><br>
 
 The "correct" word sequence maximizes `P(word sequence | keystrokes)`. Using Bayes rule, this is equivalent to maximizing `P(keystrokes | word sequence) * P(word sequence)`. This is called the **noisy channel model**.
 
 It turns out we need two models:
 
 1. *Keystroke model* `P(keystrokes | word sequence)`, which scores letters based on screen taps
 2. *Language model* `P(word sequence)`, which scores word sequences based on how realistic they are
 
Now let's look at the model applied to a generic translation problem. The correct English translation given a sequence of words in French maximizes `P(French sequence | English sequence) * P(English sequence)`.

Again, we have two models:

 1. *Translation model* `P(French sequence | English sequence)`, which scores French translation given an English sequence
 2. *Language model* `P(English sequence)`, which scores English sequences based on how realistic they are
 
 The noisy channel model also works for:
 
 * Speech Recognition: `P(audio | words) * P(words)`
 * Optical character recognition: `P(pixels | words) * P(words)`
 * Spelling correction: `P(character sequence | word) * P(word)`
 * Handwriting recognition: `P(pixels | word or letter) * P(word or letter)`
 * etc. <br><br>

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
