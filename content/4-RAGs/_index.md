---
title : "RAG Overview"
weight : 4
chapter : false
pre : " <b> 4 </b> "
---

RAG is a framework for building generative AI applications that can make use of enterprise data sources and vector databases to overcome knowledge limitations. RAG works by using a retriever module to find relevant information from an external data store in response to a user's prompt. This retrieved data is used as context, combined with the original prompt, to create an expanded prompt that is passed to the language model. The language model then generates a completion that incorporates the enterprise knowledge. 

With RAG, language models can go beyond their original training data to use up-to-date, real-world information. RAG addresses the challenge of frequent data changes because it retrieves updated and relevant information instead of relying on potentially outdated sets of data.

![Bedrock](../images/4/1.png?featherlight=false&width=90pc)

The architecture diagram describes the components used in the RAG architecture and depicts the sequence of events. There are two distinct stages when using the RAG pattern. The lower portion of the diagram explains converting the existing knowledge documents into vector embeddings and storing them in a vector database. This phase is typically performed by a batch job. After it is complete, you can augment the user’s query with relevant information or documents using semantic search. You can then pass the user’s query and retrieved information into an LLM for completion.

**Phase 1**

The focus of this phase is to convert the enterprise data used to augment input prompts into a compatible format to perform a relevancy search. This is done using an embeddings machine learning model. The batch job calls the model to convert existing knowledge documents into its numerical representations. The batch job then stores the data in a vector database using the approach described in the following three steps. To learn more, choose each of the following three numbered markers.

![Bedrock](../images/4/2.png?featherlight=false&width=90pc)

**Phase 2**

Phase 2 comprises seven steps. To learn more, choose each of the following seven numbered markers.

![Bedrock](../images/4/3.jpg?featherlight=false&width=90pc)
