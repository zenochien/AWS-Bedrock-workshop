---
title : "Introduction to Architecture Patterns"
weight : 7
chapter : false
pre : " <b> 7 </b> "
---

#### Architecture patterns

In this module, you will learn about various architecture patterns that can be implemented with Amazon Bedrock for building useful generative AI applications such as the following: 

* Text generation
* Text summarization
* Question answering
* Chatbots
* Code generation
* LangChain agents
* Agents for Amazon Bedrock

![Bedrock](../images/7/1.png)

#### Text generation

Text generation is a term used for any use case where the output of the model is newly generated text. You can use it to write articles, poems, blogs, books, emails, and so forth. In Amazon Bedrock, you can use various foundation models (FMs) for text generation tasks. 

The architecture pattern for text generation using Amazon Bedrock is illustrated in the following image. You can pass the Amazon Bedrock foundation model a prompt using an Amazon Bedrock playground or an Amazon Bedrock API call. The model will generate text based on the input prompt you provide. 

![Bedrock](../images/7/2.png)

**Text generation with LangChain**

For text generation, you can also use a LangChain layer to add a conversation chain to specific text generation use cases. LangChain is a powerful open source library. It pairs well with some of the strongest text generation FMs on Amazon Bedrock to efficiently create conversations, text generation, and more. The architecture pattern for text generation with LangChain is illustrated in the following figure.

![Bedrock](../images/7/3.png)

#### Text summarization

Text summarization is a natural language processing (NLP) task that condenses the text from a given input while preserving the key information and meaning of the text. The following are the two ways to do summarization:

* Select a subset of text from input that represents key ideas.
* Create new sentences that capture the key concepts and elements of the source text.

With advances in generative AI and large language models (LLMs), the field of text summarization has witnessed significant improvements. LLMs are well suited for the task of generating summaries because of their effectiveness in understanding and synthesizing text. In this section, you will explore concepts, applications, and architecture patterns related to text summarization with large language models.

#### Question answering architecture

Question answering is an important task that involves extracting answers to factual queries posed in natural language. Typically, a question answering system processes a query against a knowledge base containing structured or unstructured data and generates a response with accurate information. Ensuring high accuracy is key to developing a useful, reliable, and trustworthy question answering system, especially for enterprise use cases. 

![Bedrock](../images/7/4.png)

RAG involves the following steps:

1. The user asks a question.
2. Domain-specific documents are converted into embeddings using the Amazon Titan Embeddings model. The embeddings are stored in a knowledge base (vector database) for subsequent retrieval.
3. The user's question is used to retrieve the relevant chunks of data, which will act as the context, from the knowledge base. The user's question and the context are then passed to the FM to get an accurate response to the user.
4. When the user poses a prompt, the FM identifies the context and refers to the knowledge base to get the relevant chunks of data. The FM then interacts with another FM to get an accurate response to the user. 

![Bedrock](../images/7/5.png)

#### Chatbots

Chatbots use NLP and machine learning (ML) algorithms to understand and respond to user queries. You can use chatbots in a variety of application, such as customer sevice, sales, and ecommerce, to provide quick and efficient responses to users. You can access chatbots through various channels, such as websites, social media platforms, and messaging apps.

A basic architectural pattern of a chatbot use case with Amazon Bedrock is illustrated in the following diagram. 

![Bedrock](../images/7/6.png)

This architecture includes the following steps:

1. The user queries the chatbot.
2. The chat history (if there is any) is passed on to the Amazon Bedrock model along with the user’s current query.
3. The model then generates a response.
4. The model passes the response back to the user.

**Chatbot use cases**

You can categorize the chatbot use cases as follows:

* **Chatbot (Basic)**: This is a zero-shot chatbot with an FM model.
* **Chatbot using a prompt template (LangChain)**: This is a chatbot with some context provided in the prompt template.
* **Chatbot with a persona**: This is a chatbot with defined roles, such as a career coach with human interactions.
* **Contextual-aware chatbot**: This is a chatbot that passes context through an external file by generating embeddings.

**Architecture for a context-aware chatbot**

A simple architecture for a context-aware chatbot is shown in the following diagram. This architecture includes the following steps: 

1. The user asks a question (user query) to the LLM on Amazon Bedrock.
2. Step 2:

    - a. The LLM sends the modified question to the embeddings model.

    - b. The chat history is updated.

    - c. The user query is converted to a vector embedding using the Amazon Titan Embeddings model.

3. A similarity search is performed. The result of the search is a set of relevant text chunks.
4. Based on the stored information, an answer to the prompt (user query) is generated from the final FM.
5. Step 5:

    - a. The user query and the response from the FM are added to the chat history.

    - b. The response (answer) is given to the user at the same time.

![Bedrock](../images/7/7.png)

#### Code Generation

You can also use the foundation models in Amazon Bedrock for various coding and programming related tasks. Examples include code and SQL query generation, code explanation and translation, bug fixing, code optimization, and so forth. Using foundation models for coding related tasks helps developers and data scientists rapidly prototype their ideas and use cases. 

The following architecture pattern illustrates the use case of using the FMs in Amazon Bedrock for coding and programming. 

The steps are as follows: 

1. The user enters a code prompt.
2. A foundation model processes the input data.
3. The model returns the generated code.

![Bedrock](../images/7/8.png)

#### LangChain agents

Foundation models undergo extensive training on vast amounts of data. Despite their substantial natural language understanding capabilities, they cannot independently perform tasks like processing insurance claims or making flight reservations. This limitation arises from the necessity for access to the latest company or industry-specific data, which foundation models cannot obtain from up-to-date knowledge sources by default. Additionally, FMs cannot take specific actions to fulfill requests without a great deal of manual programming. 

Certain applications demand an adaptable sequence of calls to language models and various utilities depending on user input. The agent interface provides flexibility for these applications. An agent has availability to a range of resources and selects which ones to use based on the user input. Agents can use multiple tools, and they can use the output of one tool as the input for the next.

The architecture is illustrated in the following image.

**Using ReAct to run agents on LangChain**

You can run agents on LangChain by using one of two techniques: plan and execute or ReAct, which stands for **reasoning** and **acting**. The ReAct technique will evaluate the prompt and determine the next step in solving the problem. It will then run that step and then repeat the process until the LLM can answer the question. Plan and execute works a little differently in that it determines the steps needed ahead of time and performs them sequentially. 

**Example: Connecting foundation models to your company data sources with agents for Amazon Bedrock**

1. **Use RAG**

- Agents for Amazon Bedrock use RAG to provide agents access to a knowledge base in Amazon Bedrock. The knowledge base is created in Amazon Bedrock and points to a data source on Amazon Simple Storage Service (Amazon S3) that contains your data. You have the option to sync your knowledge base in Amazon Bedrock to your data on Amazon S3. 

2. **Select an embeddings model and vector database**

- Next, you will select an embeddings model and provide details for a vector database. For the vector database, you can choose between Amazon OpenSearch Serverless, Pinecone, and Redis Enterprise Cloud.  

3. **Add the knowledge base**

- You can add the knowledge base when creating or updating agents for Amazon Bedrock. 

4. **Create and add action groups**

- When adding the knowledge base to the agent, you can also create and add action groups to it. Action groups are tasks that an agent can perform autonomously. You can provide Lambda functions that represent your business logic and the related API schema to run those functions. Although action groups are not required to create an agent, they can augment model performance to yield better outputs. 

