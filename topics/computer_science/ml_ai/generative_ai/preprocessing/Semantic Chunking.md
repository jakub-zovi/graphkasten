---
tags:
  - gen_ai
  - gen_ai/rag
created: 2025-02-07T16:39
modified: 2026-08-02T10:12
published:
sources:
  - "[Pinecone Chunking Strategies](https://www.pinecone.io/learn/chunking-strategies/)"
topics:
  - Chunking
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Semantic Chunking
A new experimental technique for approaching chunking was first introduced by [Greg Kamradt](https://www.linkedin.com/in/gregkamradt/). [In his notebook](https://github.com/FullStackRetrieval-com/RetrievalTutorials/blob/main/tutorials/LevelsOfTextSplitting/5_Levels_Of_Text_Splitting.ipynb), Kamradt rightfully points to the fact that a global chunking size may be too trivial of a mechanism to take into account the **meaning** of segments within the document. If we use this type of mechanism, we can’t know if we’re combining segments that have anything to do with one another.

Here are the steps that make semantic chunking work:
1. Break up the document into sentences.
2. Create sentence groups: for each sentence, create a group containing some sentences before and after the given sentence. The group is essentially “anchored” by the sentence use to create it. You can decide the specific numbers before or after to include in each group - but all sentences in a group will be associated with **one** “anchor” sentence.
3. Generate embeddings for each sentence group and associate them with their “anchor” sentence.
4. Compare distances between each group sequentially: When you look at the sentences in the document sequentially, as long as the topic or theme is the same - the distance between the sentence group embedding for a given sentence and the sentence group preceding it will be **low**. On the other hand, **higher** semantic distance indicates that the theme or topic has changed. This can effectively delineate one chunk from the next.

[LangChain](https://python.langchain.com/docs/get_started/introduction) has created a [semantic chunking splitter](https://python.langchain.com/docs/modules/data_connection/document_transformers/semantic-chunker/) implemented based on Kamradt’s work. You can also try out [our notebook for advanced chunking methods for RAG](https://github.com/pinecone-io/examples/blob/master/learn/generation/better-rag/02b-semantic-chunking.ipynb).
