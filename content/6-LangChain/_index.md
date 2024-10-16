---
title : "Optimizing LLM Performance"
weight : 6
chapter : false
pre : " <b> 6 </b> "
---

#### LLM performance challenges

Large language models (LLMs) are pretrained on large data collections, and they can perform multiple tasks, such as text generation, text summarization, question answering, and sentiment analysis. However, the models do not perform well when the task requires dealing with out-of-domain data or remembering conversational context.

These challenges lead to hallucinations or inaccurate responses. A single prompt to the LLM might not always provide the expected result. It might require the chaining of requests to the model to produce accurate results.

#### Simplifying LLM development with LangChain

LangChain provides the software building blocks to reduce the complexity of building functionality from scratch. You can use it to take full advantage of the power of the LLMs.

![Bedrock](../images/5/1.png?featherlight=false&width=90pc)

LLMs do not retain state between invocations, so the application must manage any context. For example, to give a chat experience, the LLM needs the conversation as part of the context to produce the correct results. Additionally, LLMs can develop reasoning to solve problems, such as multistep problems where the application needs to find information in steps to solve a problem. LangChain provides components to make it more efficient to perform the common tasks of managing context or the sequencing of steps when interacting with an LLM.

#### Using LangChain components

LangChain is open source and is currently available in three programming languages: Python, TypeScript, and JavaScript. LangChain consists of components such as schema, models, prompts, indexes, memory, chains, and agents.

You can use these components to build applications, such as the Retrieval Augmented Generation (RAG) based question answering chatbots. You can also use these components for text summarization, code generation, and interacting with APIs. 

![Bedrock](../images/5/2.png)

#### Supported integrations for AWS

LangChain supports integrations with numerous software providers, including Amazon. Some of the most important integrations related to Amazon include LLMs, prompt templates, chains, chat models, text embedding models, document loaders, retrievers, and agents. 

*Schema* The schema provides the structure for the conversation to construct the prompts generated by LangChain that are sent to the LLM. For example, the ChatMessages schema describes how to construct chat prompts with human messages, artificial intelligence (AI) messages, examples, and documents.

In the following lessons, you will learn about the most important AWS and LangChain integrations for models, prompt templates, indexes, memory, chains, and agents.

![Bedrock](../images/5/3.png)

**LLMs**

LLMs take text as input and generate text as output, and LangChain provides LLM components to interact with different language models. The LLM class is an abstraction for working across different providers and is used by LangChain to interact with an LLM model.

![Bedrock](../images/5/5.jpg)

**Amazon Bedrock**

LangChain supports Amazon Bedrock as an LLM. For more information, refer to the API. Amazon Bedrock currently supports Titan Text models from Amazon, Jurassic models from AI21, Claude from Anthropic, Cohere Command and Embed, Llama models from Meta, Stable Diffusion models from Stability AI, and Mistral models from Mistral AI.

The following example demonstrates how to create an instance of the Amazon Bedrock class and invoke an Amazon Titan LLM from the LangChain LLM module. The model_id is the value of the selected model available in Amazon Bedrock.

```
import boto3
from langchain_aws import BedrockLLM
bedrock_client = boto3.client('bedrock-runtime',region_name="us-east-1")


inference_modifiers = {"temperature": 0.3, "maxTokenCount": 512

llm = BedrockLLM(
     client = bedrock_client,
     model_id="amazon.titan-tg1-large",
     model_kwargs =inference_modifiers
)

response = llm.invoke("What is the largest city in Vermont?")
print(response)
```

**Chat models**

Conversational interfaces, such as chatbots and virtual assistants, can lower the cost of customer support, while improving customer experience. LangChain provides a chat models component to build conversational applications. This component accepts content in the form of messages that contain input text.

![Bedrock](../images/5/6.png)

**Chat models example**

The following example demonstrates how you can get a response from an LLM by passing a user request to the LLM.

```
Input

from langchain_aws import ChatBedrock as Bedrock
from langchain.schema import HumanMessage
chat = Bedrock(model_id="anthropic.claude-3-sonnet-20240229-v1:0", model_kwargs={"temperature":0.1})

messages = [
     HumanMessage(
          content="I would like to try Indian food, what do you suggest should I try?"
     )
]
chat.invoke(messages)
```

**Sample response**

> **AIMessage(content=**"Here are some delicious and popular Indian dish recommendations for someone trying Indian food for the first time:\n\n- Butter Chicken (Murgh Makhani) - Tender chicken in an aromatic tomato-based curry with butter and cream. It's flavorful but not too spicy.\n\n- Chicken Tikka Masala - Chunks of roasted marinated chicken in a creamy tomato-based sauce.\n\n- Palak Paneer - A vegetarian dish with paneer (fresh cheese cubes) cooked in a thick spinach-based curry.\n\n- Chana Masala - A vegetarian chickpea curry flavored with spices like cumin, coriander and garam masala.\n\n- Samosas - Fried or baked pastry pockets stuffed with a savory potato/vegetable filling.\n\n- Naan - Leavened oven-baked flatbread, perfect for soaking up curries. Try garlic or butter naan.\n\n- Biryani - A flavorful mixed rice dish with meat/vegetables and aromatic spices.\n\nI'd recommend getting a combination platter or thali to sample a variety of dishes on your first visit. Start with milder dishes and work your way up if you want more heat/spice. Indian food has incredible depth of flavor!", additional_kwargs={'usage': {'prompt_tokens': 23, 'completion_tokens': 300, 'total_tokens': 323}}, response_metadata={'model_id': 'anthropic.claude-3-sonnet-20240229-v1:0', 'usage': {'prompt_tokens': 23, 'completion_tokens': 300, 'total_tokens': 323}}, id='run-09f0ef8a-90c0-47c3-b172-546b084d1288-0')

**Text embedding models**

Text embedding models take text as input and then output numerical representations of the text in the form of a vector of floating-point numbers. The numerical representations are called word embeddings, and they capture the semantic meaning of the text.

The embeddings are used in various natural language processing (NLP) tasks, such as sentiment analysis, text classification, and information retrieval. You can save the embeddings in a vector database to improve search accuracy and for faster retrieval.

![Bedrock](../images/5/7.jpg)

**Embedding example**

The following example demonstrates how to call a BedrockEmbeddings client to send text to the Amazon Titan Embeddings model to get embeddings as a response.

```
from langchain.embeddings import BedrockEmbeddings

embeddings = BedrockEmbeddings(
     region_name="us-east-1",
     model_id="amazon.titan-embed-text-v1"
)
 
embeddings.embed_query("Cooper is a puppy that likes to eat beef")
```

In the following example, the baseline sentence is about a dog that likes to eat beef. A list of candidate phrases is compared against the baseline and sorted by similarity, with 0 being most similar and 1 being least similar.

**Baseline: Cooper is a dog that likes to eat beef.**

| **Score** | **Text**                                                                                            |
|-----------|-----------------------------------------------------------------------------------------------------|
| 0.035882  | Cooper is a puppy that likes to eat beef.                                                           |
| 0.083690  | Beef is what a dog named Cooper likes.                                                              |
| 0.109997  | Cooper is a dog that hates eating beef.                                                             |
| 0.135489  | Cooper is a dog that hates eating beef.                                                             |
| 0.184443  | Cooper is a dog that likes to eat chicken                                                           |
| 0.192230  | Fido is a dog that likes to eat beef                                                                |
| 0.194594  | Cooper is a cat that likes to eat beef                                                              |
| 0.228607  | Spot is a dog that likes to eat beef.                                                               |
| 0.264782  | Cooper is a man that likes to eat beef                                                              |
| 0.351404  | Cooper ist ein Hund, der gerne Rindfleisch frisst.                                                  |
| 0.799773  | A cooper is someone that makes barrels.                                                             |
| 1.016293  | Amazon Web Services provides on-demand cloud computing solutions and APIs on a pay-as-you-go basis. |

#### Prompt templates in LangChain

LangChain provides predefined prompt templates in the form of text strings that can take a set of parameters from the user and generate a prompt. Prompt templates make prompt engineering more efficient and make it possible to reuse prompts.

![Bedrock](../images/5/8.png)

**Prompt example**

```
from langchain import PromptTemplate

# Create a prompt template that has multiple input variables
multi_var_prompt = PromptTemplate(
     input_variables=["customerName", "feedbackFromCustomer"],
     template="""
     Human: Create an email to {customerName} in response to the following customer service feedback that was received from the customer: 
     <customer_feedback> 
          {feedbackFromCustomer}
     </customer_feedback>
     Assistant:"""
)
# Pass in values to the input variables
prompt = multi_var_prompt.format(customerName="John Doe",
          feedbackFromCustomer="""Hello AnyCompany, 
     I am very pleased with the recent experience I had when I called your customer support.
      I got an immediate call back, and the representative was very knowledgeable in fixing the problem. 
     We are very happy with the response provided and will consider recommending it to other businesses.
     """
)
```

#### Structuring Documents with Indexes

**Document loaders**

When building generative AI applications using the RAG approach, documents must be loaded from different sources to the LLMs to generate embeddings.  

LangChain provides the document loaders component, which is responsible for loading documents from various sources. Sources can include a database, an online store, or a local store. You can index and use information from these sources for information retrieval. You can use the document loaders to load different types of documents, such as HTML, PDF, and code.

**Document loaders example**

The following example demonstrates the loading of a document from Amazon Simple Storage Service (Amazon S3) using the S3FileLoader module.

```
from langchain.document_loaders import S3FileLoader

loader = S3FileLoader("mysource_bucket","sample-file.docx")
data = loader.load()
```

**Retriever**

LangChain includes a retriever component for fetching relevant documents to combine with language models. When a user submits a query, the retriever searches through the document index to find the most relevant documents. It then sends the results to the application for further processing.

When building RAG applications on AWS, you can use Amazon Kendra to index and query various data sources. Amazon Kendra is a fully managed service that provides semantic search capabilities for state-of-the-art ranking of documents and passages.

Amazon Kendra also comes with pre-built connectors to popular data sources, such as Amazon S3, SharePoint, Confluence, and websites. It supports common document formats, such as HTML, Microsoft Word, PowerPoint, PDF, Excel, and PureText files.

**Retriever example**

The following example demonstrates the use of the AmazonKendraRetriever to query an Amazon Kendra index and pass the results from that call to an LLM as context along with a prompt.

```
from langchain.retrievers import AmazonKendraRetriever
from langchain.chains import ConversationalRetrievalChain
from langchain.prompts import PromptTemplate
from langchain_aws import ChatBedrock 


llm = ChatBedrock(
     model_kwargs={"max_tokens_to_sample":300,"temperature":1,"top_k":250,"top_p":0.999,"anthropic_version":"bedrock-2023-05-31"},
     model_id="anthropic.claude-3-sonnet-20240229-v1:0"
)

retriever = AmazonKendraRetriever(index_id=kendra_index_id,top_k=5,region_name=region)

prompt_template = """ Human: This is a friendly conversation between a human and an AI.
The AI is talkative and provides specific details from its context but limits it to 240 tokens.
If the AI does not know the answer to a question, it truthfully says it
does not know.

Assistant: OK, got it, I'll be a talkative truthful AI assistant.

Human: Here are a few documents in <documents> tags:
<documents>
{context}
</documents>
Based on the above documents, provide a detailed answer for, {question}
Answer "do not know" if not present in the document.

Assistant:
 """

PROMPT = PromptTemplate(
     template=prompt_template, input_variables=["context", "question"]
)

response = ConversationalRetrievalChain.from_llm(
     llm=llm,
     retriever=retriever,
     return_source_documents=True,
     combine_docs_chain_kwargs={"prompt":PROMPT},
     verbose=True)
```

**Vector stores**

When building generative AI applications, such as question answering bots, the LLMs produce accurate results when relevant company-specific or user-specific data is given as context.

You can use the RAG approach, and follow these steps: 

1. You can convert the company-specific data, such as documents, into embeddings using the text embeddings model (described in the previous section). 
2. You can then store the embeddings in a vector database. 
3. You can extract the relevant documents based on the user request from the vector database. 
4. You can then pass them to the LLM as context for an accurate response. 

LangChain supports both open source and provider-specific vector stores. LangChain supports vector engine for Amazon OpenSearch Serverless and the pgvector extension available with Amazon Aurora PostgreSQL-Compatible Edition. LangChain provides the vector stores component to query the supported vector stores for relevant data.

**Vector store example**

The following example demonstrates how to create an instance of the VectorStore class and use OpenSearch Serverless as a vector store to query embeddings.

```
import os
from langchain.embeddings import BedrockEmbeddings
from langchain.vectorstores import OpenSearchVectorSearch

index_name = os.environ["AOSS_INDEX_NAME"]
endpoint = os.environ["AOSS_COLLECTION_ENDPOINT"]

embeddings = BedrockEmbeddings(client=bedrock_client)

vector_store = OpenSearchVectorSearch(
     index_name=index_name,
     embedding_function=embeddings,
     opensearch_url=endpoint,
     use_ssl=True,
     verify_certs=True,
)
retriever = vector_store.as_retriever()
```

#### LangChain memory

LangChain memory provides the mechanism to store and summarize (if needed) prior conversational elements that are included in the context on subsequent invocations. LangChain provides components in the form of helper utilities for managing and manipulating previous chat messages. These utilities are modular. You can chain them with other components and interact with different types of abstractions to build powerful chatbots.

In LangChain, there are different ways you can implement conversational memory for a chatbot as follows: 

* **ConversationBufferMemory**: The ConversationBufferMemory is the most common type of memory in LangChain. It includes past conversations that happened between the user and the LLM.

* **ConversationChain**: The ConversationBufferMemory is built on top of ConversationChain, which is designed for managing conversations. For a complete list of supported memory types

**Memory example**

The following example demonstrates the use of ConversationBufferMemory to store the previous conversation and have the LLM respond to subsequent questions by using the chat history.

```
from langchain.chains import ConversationChain
from langchain_aws import BedrockLLM
from langchain.memory import ConversationBufferMemory
bedrock_client = boto3.client('bedrock-runtime',region_name="us-east-1")


titan_llm = BedrockLLM(model_id="amazon.titan-tg1-large", client=bedrock_client)
memory = ConversationBufferMemory()

conversation = ConversationChain(
     llm=titan_llm, verbose=True, memory=memory
)

print(conversation.predict(input="hi! I am in Los Angeles. What are some of the popular site seeing places?"))
```

Ask a question without mentioning the city Los Angeles to find out how the model responds according to the previous conversation.

```
print(conversation.predict(input="What is closest beach that I can go to?"))
```

#### Chaining components

At its core, a chain is a set of components that run together. The component can be a call to an LLM, an API, or a sequence of other chains. The component has an input format and an output. For example, the LLMChain takes in an LLM, a prompt template, and parameters to the prompt template. It returns the output of the LLM call. The chain can parse the output of the LLM to a specific format and return the data in a more structured way.

**Processing large amounts of data**

Chains are also helpful when processing more data than can be contained in the context. For example, you might do a document summarization against a very large document. The chain will chunk up the document and make multiple calls to the LLM to produce a single summary.

There are different types of chains that LangChain supports, among which the LLMChain is a common one.

**Chain example**

The following example demonstrates how to use chains to call an LLM multiple times in a sequence.

```
from langchain import PromptTemplate
from langchain.chains import LLMChain
from langchain_aws import ChatBedrock as Bedrock

chat = Bedrock(
     region_name = "us-east-1",
     model_kwargs={"temperature":1,"top_k":250,"top_p":0.999,"anthropic_version":"bedrock-2023-05-31"},
     model_id="anthropic.claude-3-sonnet-20240229-v1:0"
)

multi_var_prompt = PromptTemplate(
     input_variables=["company"],
     template="Create a list with the names of the main metrics tracked in the reports of {company}?",
)
 
chain = LLMChain(llm=chat, prompt=multi_var_prompt)
answers = chain.invoke("Amazon")
print(answers)

answers = chain.invoke("AWS")
print(answers)
```

#### Using LangChain agents

LangChain agents can interact with external sources, such as search engines, calculators, APIs, or databases. The agents can also run code to perform actions to assist the LLMs in generating accurate responses. LangChain provides the chain interface to sequence multiple components to build an application. An LLMChain is an example of a basic chain.

The following mechanisms use basic chains:

* A RAG application can use an LLMChain to return a response. The response is based on two pieces of information: the user query and a context supplied as a set of documents retrieved from a vector store. 

* A RouterChain is an example of a complex chain. For example, you can use a RouterChain to select one prompt template from the available prompt templates based on user input. 

* The LangChain agents act as reasoning engines for the LLMs to decide the actions to take and the order in which to take the actions. An action can be a tool that uses the results from a search engine or a math calculator.

**LangChain agent features**

The LangChain agent follows a sequence of actions :
* LangChain provides tools and toolkits (a group of three to five different tools) in the form of functions for the agent to call. The agent is formed with access to an LLM, a set of tools, and a stopping condition.
* The agent uses the ReAct (reasoning and acting) prompting framework to choose the most relevant tool from the set of tools provided based on the user input.
* The agent repeatedly decides the action, runs the action, and observes the output of the tool until the stopping condition is met.

**Agent example**

The following example demonstrates how to initialize an Agent, Tool, and LLM to form a chain and have the ZERO_SHOT ReAct agent call the in-built tool LLMMathChain to do math calculations separately and pass the result to the LLM for the final response.

```
from langchain.agents import load_tools
from langchain.agents import initialize_agent, Tool
from langchain.agents import AgentType
from langchain import LLMMathChain
from langchain_aws import ChatBedrock
from langchain.agents import AgentExecutor, create_react_agent

chat = ChatBedrock(model_id="anthropic.claude-3-sonnet-20240229-v1:0", model_kwargs={"temperature":0.1})

prompt_template = """Answer the following questions as best you can.
You have access to the following tools:\n\n{tools}\n\n
Use the following format:\n\nQuestion: the input question you must answer\n
Thought: you should always think about what to do\n
Action: the action to take, should be one of [{tool_names}]\n
Action Input: the input to the action\nObservation: the result of the action\n...
(this Thought/Action/Action Input/Observation can repeat N times)\n
Thought: I now know the final answer\n
Final Answer: the final answer to the original input question\n\nBegin!\n\n
Question: {input}\nThought:{agent_scratchpad}
"""
modelId = "anthropic.claude-3-sonnet-20240229-v1:0"

react_agent_llm = ChatBedrock(model_id=modelId, client=bedrock_client)
math_chain_llm = ChatBedrock(model_id=modelId, client=bedrock_client)

tools = load_tools([], llm=react_agent_llm)

llm_math_chain = LLMMathChain.from_llm(llm=math_chain_llm, verbose=True)

llm_math_chain.llm_chain.prompt.template = """Human: Given a question with a math problem, provide only a single line mathematical expression that solves the problem in the following format. Don't solve the expression only create a parsable expression.
text
{{single line mathematical expression that solves the problem}}


Assistant:
Here is an example response with a single line mathematical expression for solving a math problem:
text
37593**(1/5)


Human: {question}
Assistant:"""

tools.append(
     Tool.from_function(
          func=llm_math_chain.run,
          name="Calculator",
          description="Useful for when you need to answer questions about math.",
     )
)

react_agent = create_react_agent(react_agent_llm,
     tools,
     PromptTemplate.from_template(prompt_template)
          # max_iteration=2,
          # return_intermediate_steps=True,
          # handle_parsing_errors=True,
     )

agent_executor = AgentExecutor(
agent=react_agent,
tools=tools,
verbose=True,
handle_parsing_errors=True,
max_iterations = 10 # useful when agent is stuck in a loop
)

agent_executor.invoke({"input": "What is the distance between San Francisco and Los Angeles? If I travel from San Francisco to Los Angeles with the speed of 40MPH how long will it take to reach?"})

```