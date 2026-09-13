---
tags:
  - ml_ai
  - ml_ai/neural_nets
created:
modified: 2026-02-15T10:14
published:
sources:
  - "[BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding](https://scholar.google.com/scholar?hl=en&as_sdt=0%2C5&q=+BERT%3A+Pre-training+of+Deep+Bidirectional+Transformers+for+Language+Understanding&btnG=)"
  - "[TowardsDatascience](https://towardsdatascience.com/bert-explained-state-of-the-art-language-model-for-nlp-f8b21a9b6270)"
topics:
  - Transformers
  - BERT
authors:
ai-assisted:
hidden:
public: true
---
# BERT
Introduced originally in  [BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding](https://scholar.google.com/scholar?hl=en&as_sdt=0%2C5&q=+BERT%3A+Pre-training+of+Deep+Bidirectional+Transformers+for+Language+Understanding&btnG=) paper.
[[ModernBERT]] improvement over the original BERT architecture.

Distilled explanation from [TowardsDatascience](https://towardsdatascience.com/bert-explained-state-of-the-art-language-model-for-nlp-f8b21a9b6270):
> BERT makes use of Transformer, an attention mechanism that learns contextual relations between words (or sub-words) in a text. In its vanilla form, Transformer includes two separate mechanisms — an encoder that reads the text input and a decoder that produces a prediction for the task. Since BERT’s goal is to generate a language model, only the encoder mechanism is necessary.
> 
> As opposed to directional models, which read the text input sequentially (left-to-right or right-to-left), the Transformer encoder reads the entire sequence of words at once. Therefore it is considered bidirectional, though it would be more accurate to say that it’s non-directional. This characteristic allows the model to learn the context of a word based on all of its surroundings (left and right of the word)

Like many other language models, BERT's training is split into two steps: pre-training and fine-tuning.
## Pre-Training
The pre-training is split into two task that are performed simultaneously: Masked Language Modeling (MLM) and Next Sentence Prediction (NSP).

### Masked Language Modeling
[TowardsDatascience](https://towardsdatascience.com/bert-explained-state-of-the-art-language-model-for-nlp-f8b21a9b6270):
> Before feeding word sequences into BERT, 15% of the words in each sequence are replaced with a [MASK] token. The model then attempts to predict the original value of the masked words, based on the context provided by the other, non-masked, words in the sequence. In technical terms, the prediction of the output words requires:
> 
> 1. Adding a classification layer on top of the encoder output.
> 2. Multiplying the output vectors by the embedding matrix, transforming them into the vocabulary dimension.
> 3. Calculating the probability of each word in the vocabulary with softmax.
> 
> The BERT loss function takes into consideration only the prediction of the masked values and ignores the prediction of the non-masked words. As a consequence, the model converges slower than directional models, a characteristic which is offset by its increased context awareness.

### Next Sentence Prediction
[TowardsDatascience](https://towardsdatascience.com/bert-explained-state-of-the-art-language-model-for-nlp-f8b21a9b6270):
> In the BERT training process, the model receives pairs of sentences as input and learns to predict if the second sentence in the pair is the subsequent sentence in the original document. During training, 50% of the inputs are a pair in which the second sentence is the subsequent sentence in the original document, while in the other 50% a random sentence from the corpus is chosen as the second sentence. The assumption is that the random sentence will be disconnected from the first sentence.
> 
> To help the model distinguish between the two sentences in training, the input is processed in the following way before entering the model:
> 
> 1. A [CLS] token is inserted at the beginning of the first sentence and a [SEP] token is inserted at the end of each sentence.
> 2. A sentence embedding indicating Sentence A or Sentence B is added to each token. Sentence embeddings are similar in concept to token embeddings with a vocabulary of 2.
> 3. A positional embedding is added to each token to indicate its position in the sequence. The concept and implementation of positional embedding are presented in the Transformer paper.
> To predict if the second sentence is indeed connected to the first, the following steps are performed:

<img src="https://miro.medium.com/v2/resize:fit:720/format:webp/0*m_kXt3uqZH9e7H4w.png">

> 1. The entire input sequence goes through the Transformer model.
> 2. The output of the [CLS] token is transformed into a 2×1 shaped vector, using a simple classification layer (learned matrices of weights and biases).
> 3. Calculating the probability of IsNextSequence with softmax.

### How MLM and NSP Work Together
ChatGPT[^1]:
> During pre-training, both MLM and NSP are done concurrently. For each batch of input:
> 
> 1. **MLM** is applied by masking tokens in the input sentences.
> 2. **NSP** is applied by pairing the sentence with another sentence (either the next one or a random one) and predicting whether the second sentence follows logically.
> 3. The loss function for pre-training is a combination of:
>     - **MLM loss**: The model's error in predicting the masked tokens.
>     - **NSP loss**: The model's error in determining if the second sentence is a true continuation of the first.
> 
> The model learns from both types of tasks simultaneously to improve its understanding of both word-level and sentence-level semantics.

<img src="https://assets-global.website-files.com/5fbd459f3b05914cf70496d7/60cbd6ed9171c578740353f1_bert.png">

[^1]: Prompt: BERT is pre-trained for two tasks MLM and Next Sentence Prediction. But how is this done in practice? Is the pre-training first done for MLM and then we do the next sentence prediction? And then we finally proceed to fine-tuning?