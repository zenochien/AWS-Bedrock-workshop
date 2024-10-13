---
title : "Typical componets of a generative AI application"
weight : 3
chapter : false
pre : " <b> 3 </b> "
---

![Bedrock](../images/3/1.png?featherlight=false&width=90pc)

A foundation model (FM) is in the center surrounded by components. These include frontend web application or mobile app, FM interface, machine learning (ML) environment, model training, enterprise datasets, vector database, text and image embeddings, and long-term memory store. Governance and security are integrated into all components.

#### Foundation models interface

At the heart of a generative AI application is the foundation model that powers it. Foundation models are models trained on broad data at scale that can be adapted to various downstream tasks. 

![Bedrock](../images/3/2.png)

Foundation models provide the base on which you can build various generative AI applications. Large language models (LLMs) are a subset of foundation models that are trained on a large corpus of text data. 

![Bedrock](../images/3/3.png)

#### Interface and prompts

To use a foundation model, you need an interface that provides access to it. The interface is generally an API that is managed, or it can be self-hosted using an open source or proprietary model. Self-hosting often involves procuring access to a machine learning environment that is supported by purpose-built accelerated computing instances to host the model. Using the API call, you can pass prompts to the foundation model and receive inference responses back.

![Bedrock](../images/3/4.png)

#### Working with Datasets and Embeddings

Although foundation models can generate human-like text, images, audio, and more from your prompts, this might not be sufficient for enterprise use cases. To power customized enterprise applications, the foundation models need relevant data from **enterprise datasets**.

![Bedrock](../images/3/5.png)

Enterprises accumulate huge volumes of internal data, such as documents, presentations, user manuals, reports, and transaction summaries, which the foundation model has never encountered. Ingesting and using enterprise data sources provide the foundation model with domain-specific knowledge to generate tailored, highly relevant outputs that align with the needs of the enterprise.

You can supply enterprise data to the foundation models as context along with the prompt, which will help the model to return more accurate outputs. How do you figure out the context to pass? For that, you need a way to search the enterprise datasets using the prompt text that is passed. This is where **vector embeddings** help.

**Vector embeddings**

Embedding is the process by which text, images, and audio are given numerical representation in a vector space. Embedding is usually performed by a machine learning model. The following diagram provides more details about embedding. 

![Bedrock](../images/3/6.png?featherlight=false&width=90pc)

Enterprise datasets, such as documents, images and audio, are passed to ML models as tokens and are vectorized. These vectors in an n-dimensional space, along with the metadata about them, are stored in purpose-built vector databases for faster retrieval. 

**Vector databases**

The core function of **vector databases** is to compactly store billions of high-dimensional vectors representing words and entities. Vector databases provide ultra-fast similarity search across these billions of vectors in real time. 

The most common algorithms used to perform the similarity search are k-nearest neighbors (k-NN) or cosine similarity.

![Bedrock](../images/3/7.png)

Amazon Web Services (AWS) offers the following as viable vector database options:
- Amazon OpenSearch Service (provisioned)
- Amazon OpenSearch Serverless
- pgvector extension in Amazon Relational Database Service (Amazon RDS) for PostgreSQL
- pgvector extension in Amazon Aurora PostgreSQL - Compatible Edition

{{< callout "" >}}
For more information, refer to the following resources:
* [K-Nearest Neighbor (k-NN) Search in Amazon OpenSearch Service](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/knn.html)
* [Vector Engine for Amazon OpenSearch Serverless (Preview)](https://aws.amazon.com/opensearch-service/serverless-vector-engine/)
* [Using PostgreSQL Extensions with Amazon RDS for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Appendix.PostgreSQL.CommonDBATasks.Extensions.html)
* [Amazon Aurora PostgreSQL Now Supports pgvector for Vector Storage and Similarity Search](https://aws.amazon.com/about-aws/whats-new/2023/07/amazon-aurora-postgresql-pgvector-vector-storage-similarity-search/)
{{< /callout >}}

AWS also offers Pinecone in the AWS Marketplace, and there are open source, in-memory options, like Facebook AI Similarity Search (FAISS), Chroma, and many more.

{{< callout "" >}}
For more information, refer to the following resources:
* [Pinecone](https://aws.amazon.com/marketplace/pp/prodview-xhgyscinlz4jk)
* [FAISS](https://github.com/facebookresearch/faiss)
* [Chroma](https://www.trychroma.com/)
{{< /callout >}}

**Vectorized enterprise data**

After enterprise data is vectorized, you can search the given prompt in a vector database. You can supply the relevant chunks of information as context to improve the output of the generative AI model. This can reduce hallucinations, a phenomenon in which an LLM confidently generates plausible sounding but false information. Vector databases and context are used in Retrieval Augmented Generation (RAG).

#### Prompt history store

A prompt history store is another essential component in a generative AI application, particularly applications used for conversational AI, like chatbots. A prompt history store helps with contextually aware conversations that are both relevant and coherent. Many foundation models have a limited context window, which means you can only pass so much data as input to them. Storing state information in a multiple-turn conversation becomes difficult, which is why a prompt history store is needed. It can persist the state and make it possible to have long-term memory of the conversation.

![Bedrock](../images/3/8.png)

By storing the history of prompts and responses, you can look up prompts from a previous conversation and avoid repetitive requests to the foundation model. This helps with requests from your audit and compliance teams about adherence to company policy and regulations. You can also debug prompt requests and responses to diagnose errors and warnings from your applications.

#### Frontend web applications and mobile apps

Often, you need to build a frontend application or app that acts as an interface for your users to use generative AI capabilities from the foundation model. The application or app is responsible for constructing prompts and calling the foundation model API. The responses from the foundation model are sanitized and filtered by the application or app before the users see them on their screens. The application or app should also handle failures and other unintended consequences in a seamless manner so the user experience is not affected.

![Bedrock](../images/3/9.png)
