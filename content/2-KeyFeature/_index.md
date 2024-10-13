---
title : "Key Features of Amazon Bedrock"
weight : 2
chapter : false
pre : " <b> 2 </b> "
---

#### Key features of Amazon Bedrock
**1. Access to a range of leading foundation models (FMs)**

Bedrock offers various FMs from prominent AI companies, such as Anthropic, AI21 Labs, Cohere, Meta, Mistral AI, Stability.ai, and Amazon's own modles. Since different models are best suited for different tasks, Bedrock gives teams flexibility regarding model choice for different scenarios.

**2. Simplified and managed experience for GenAI applications**

Amazon Bedrock is a fully managed and serverless service, entirely abstracting the need to manage infrastructure components for your foundation models. It provides a single API access regardless of the chosen model, simplifying integrations, operations, and model version upgrades.

**3. Model customization and Retrieval Augmented Generation (RAG)**

The actual value of the power of FMs comes when companies manage to privately and effectively customize and adapt these models with their own proprietary data. To customize these models, Bedrock offers fine-tuning features and creates a separate private copy of this model. To pair the models with recent and up-to-date information, companies leverage RAG, a technique to enhance a model’s context with proprietary data sources for more accurate and informed responses.

**4. Built-in security, privacy, and safety**

With Bedrock, the data never leave your AWS environments and are encrypted in transit and at rest. Users can leverage their existing AWS security controls and services, such as KMS for encryption, IAM policies, CloudWatch for monitoring, CloudTrail for governance, and network design based on Amazon VPC.

When a base model is fine-tuned, a private copy of that model is used, and the proprietary data aren’t used to improve the base model. Bedrock is in scope for common compliance standards, including ISO, SOC, CSA, STAR Level 2, is HIPAA eligible, and can be used in compliance with the GDPR.

Bedrock has released the Guardrails functionality that allows companies to enforce policies and safety for their model responses. Guardrails provide a layer of safeguards and policies to promote safe and responsible usage of FMs by blocking unsafe topics, avoiding harmful content, and redacting personally identifiable information.

**5. Leverage Agents for executing multi-step tasks**

There are use cases where companies would like to automate processes and execute complex multi-step tasks based on the model’s response. With Agents, users can fast-track their prompt creation with customized instructions, orchestrate a sequence of actions, call the necessary APIs to fulfill the desired task, and monitor and trace the agent’s reasoning and orchestration of complex tasks.

#### Course Models
**1. Application Components**

| **Objectives**                                                                                   | **Topics**                                         |
|--------------------------------------------------------------------------------------------------|----------------------------------------------------|
| In the module, you will learn how to do the following:                                           | The module is organized into the following topics: |
| * Describe the components of a generative AI application                                         | * Overview of Genaretive AI Application Components |
| * Work with embedding and vector databases.                                                      | * Foundation Models and the FM interface           |
| * Customize a foundation model using Retrieval Augmented Generation (RAG) and model fine-tuning. | * Working with Datasets and Embeddings             |
| * Explain the architecture of a typical generative AI application                                | * Additional Application Components                |
|                                                                                                  | * RAG                                              |
|                                                                                                  | * Model Fine-Tuning                                |
|                                                                                                  | * Securing Generative AI Applications              |
|                                                                                                  | * Generative AI Application Architecture           |

**2. Foundation Models**

| **Objective**                                                                                   | **Topics**                                         |
|-------------------------------------------------------------------------------------------------|----------------------------------------------------|
| In this module, you will learn how to do the following:                                         | The modules is organized the following topics:     |
|  * Identify the foundation models available with Amazon Bedrock.                                | * Introduction to Amazon Bedrock Foundation Models |
| * Describe how to control the inference parameters to tune desired output.                      | * Using Amazon Bedrock FMs for Inference           |
| * Describe how to use APIs to invoke foundation models or create customization jobs.            | * Amazon Bedrock Methods                           |
| * Identify monitoring and logging capabilities and tools for governance and audit requirements. | * Data Protection and Auditability                 |

**3. Using LangChain**

| **Objective**                                                                                                                                               | **Topics**                                          |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------|
| In this module, you will learn how to do the following:                                                                                                     | The module is organized into the following topics:  |
| * Identify common challenges practitioners face when developing LLMs.                                                                                       | * Optimizing LLM Performance                        |
| * Describe the benefits of using LangChain for training LLMs.                                                                                               | * Integrating AWS and LangChain                     |
| * Integrate LangChain with LLMs, prompt templates, chains, chat models, text embeddings models, document loaders, retrievers, and agents in Amazon Bedrock. | * Using Models with LangChain                       |
| * Use LangChain agents to manage external resources.                                                                                                        | * Constructing Prompts                              |
|                                                                                                                                                             | * Structuring Documents with Indexes                |
|                                                                                                                                                             | * Storing and Retrieving Data with Memory           |
|                                                                                                                                                             | * Using Chains to Sequence Components               |
|                                                                                                                                                             | * Managing External Resources with LangChain Agents |

**4. Architecture Patterns**

| **Objective**                                                                       | **Topics**                                         |
|-------------------------------------------------------------------------------------|----------------------------------------------------|
| In this module, you will learn how to do the following:                             | The module is organized into the following topics: |
| * Describe the text generation and text summarization architecture patterns.        | * Introduction to Architecture Patterns            |
| * Explain how to use the question answering pattern for generative AI applications. | * Text Generation and Text Summarization           |
| * Describe how the chatbot pattern is used to enhance the user experience.          | * Question Answering                               |
| * Understand how FMs can be used to generate code                                   | * Chatbots                                         |
| * Work with LangChain and agents for Amazon Bedrock.                                | * Code Generation                                  |
|                                                                                     | * LangChain and Agents Amazon Bedrock              |
