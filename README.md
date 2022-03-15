# Chatbot_TF2_Transformer
Transformer chatbot built from scratch and implemented with Tensorflow 2 using greedy search- and top-k sampling to evaluate the model. 

# Project Goal

Build a chatbot using a Transformer model with attention that can generate natural sounding responses that simulate a conversation between humans.  To achieve this we will use natural language processing to preprocess data from the [Cornell Movie Dialogues Corpus](https://www.cs.cornell.edu/~cristian/Cornell_Movie-Dialogs_Corpus.html).  This database contains conversations between characters from various movies and tv-series and so provides a good starting point for such a model. 

Once the language model is trained I evaluate it by implementing natural language generation using greedy search and top-k sampling methods.  

# Model Architecture Overview

The chatbot implements a Transformer model architecture with attention to implement a sequence to sequence model.  It is based on the Google white paper ['Attention is All You Need'](https://arxiv.org/abs/1706.03762).  

Transformer models rely on attention mechanisms to compute representations of it's 'utterance - response' pairs which allows for greater parallelisation.  The main difference between Transformer models and traditional sequence to sequence models is that the transformer is able to look at the whole sequence at once.  

The model is implemented with TensorFlow 2.

# A quick word about the data

For this chatbot, we will use the Cornell Movie Dialogues Corpus This is a large metadata-rich collection of conversational exchanges between 10,292 pairs of movie characters, extracted from raw movie scripts.

The idea behind using this data is that movie conversations mimick everyday conversational exchanges between people.

Since the aim is to build a chatbot that can have a natural conversation with a human, we use this data to see if we can train a chatbot that sounds like a human in conversation.

# Evaluation

With the model built and trained it is now time to evaluate the quality of the text generation ability of the model.  I achieve this I feed an input utterance/sentence into the model which in turn generates a conditional probability distribution over the vocabulary of tokens according to the given input sequence.

We then sample a word from the probability distribution using two methods,  greedy search and/or top-k sampling. 

## General Model Performance

In general the chatbot generates reasonable responses and at times produces decent sounding conversations.  The responses do, however, tend to be over dramatic and is often strewn with sex, violence and strong language.  The model also has a tendency to generate erratic responses that will jump from buying shoes to gun violence two sentences later.  


The over-dramatic responses can probably be explained by the fact that the training data is taken from various movies and tv-series' conversations.  These conversations are created and curated to entice, entertain and keep the audience's attention at all times. 

The prevalence of erratic responses problem is possibly a result of the fact that we use conversations from different shows without providing any information to the model of the context or setting in which the conversation takes place.  


## Greedy Search Sampling 

Using greedy search to sample text from the probability distribution, the responses are mostly grammatically sound and makes sense most of the time.  Responses seem to be better for shorter sentences than longer, more complex ones. 

One downside of the greedy search responses are that the responses tend to be very generic.  The responses seldom conveys that it understands the context of the preceding sentence.  This leaves subsequent (2nd, 3rd, etc) replies to de-rail quickly resulting in non-sensical babbling.

Secondly, greedy search limits the number of responses and certain phrases like 'how about that' is repeated quite often in varying situations. 

## Top-K Sampling

With short sentences and small k-values the model again produces good quality responses that are grammatically sound.  Responses definitely illustrate a better understanding of the context, in other words the response will have one or more words that indicate that it 'understands' the utterance. 

For longer sentences still keeps the context, at least in the first response and in some cases even up until the second response but when the k-value becomes larger, the responses can become incoherent.

The current model seems to hit a sweet spot at three sentences deep, providing 'conversation-like' responses that seem more or less understandable. When using k-sampling, the context is kept better and the best results seem to appear when k=3.  
 
# Appreciation 
Much appreciation to the very generous online community and specifically the TensorFlow team for providing a tutorial that implements a chatbot from scratch in TF 2.  Also to [Murat Karakaya Academy](https://colab.research.google.com/drive/1BFaokL7uLEKRtl8rmR9RUfIVAjqhGEZR#:~:text=Murat%20Karakaya%20Akademi%20YouTube%20Channel) for covering the topic of text generation.
