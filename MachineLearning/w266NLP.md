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
- **Text** containing attitude

&nbsp;

Kinds of Sentiment Analysis:

- **Polarity task**, is attitude positive, negative, or neutral?
- **Subjectivity vs objectivity task**, phrases that are influenced and not influenced by attitude
- **Feature/aspect task**, associate attitude with a particular aspect (price, ease of use, setup, etc.)
- **Contextual task**, detect source of attitude

Removing nonsubjective phrases can improve the accuracy of a polarity classifier.

&nbsp;

**Sentiment Lexicons** assign general sentiment to words outside of context. They can be used as a mapping of individual words to typical sentiment. Some examples are: *General Inquirer*, *LIWC*, *MPQA*, *Bing Liu Opinion Lexicon*, *SentiWordNet*. There is a wide range of dissagreement between these lexicons.

&nbsp;

**Convolutional Neural Networks for NLP:**

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
