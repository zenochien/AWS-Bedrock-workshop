---
title : "Amazon Bedrock FMs"
weight : 5
chapter : false
pre : " <b> 5 </b> "
---

Amazon Bedrock offers a wide choice of foundation models (FMs) from leading artificial intelligence (AI) startups and Amazon. Each of these FMs cater to different generative artificial intelligence (generative AI) use cases, such as summarization, language translation, coding, and image generation.

Note: For users with screen readers, use table mode to read the table.

| **Company**  | **Foundation Model** | **Description**                                                                                                                                                                          |
|--------------|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Amazon       | Amazon Titan         | Family of models built by Amazon that are pretrained on large datasets, which makes them powerfull, general-purpose models.                                                              |
| AI21 Labs    | Jurassic-2           | Multilingual large language models (LLMs) for text generation in Spanish, French, German, Portuguse, Italian, and Dutch.                                                                 |
| Anthropic    | Claude 2             | LLM for thoughtful dialogue, content creation, complex reasioning, creativity, and coding based on Constitutional AI and harmlessness training.                                          |
| Cohere       | Command and Embed    | Text generation model for business applications and embeddings model for search, clustering, or classification in more than 100 languages. Now available: Stable Diffusion XL (SDXL) 1.0 |
| Stability AI | Stable Diffusion     | Text-to-image model for generation fo uinque, realistic, high-quality images, art, logos, and designs.                                                                                   |

#### Working with Amazon Bedrock FMs

Some inference parameters are common across most models, such as temperature, Top P, Top K, and response length. You will dive deep into unique model-specific parameters and I/O configuration you can tune to achieve the desired output based on the use case. 

**Amazon Titan**

Amazon Titan models are Amazon foundation models. Amazon offers the Amazon Titan Text model and the Amazon Titan Embeddings model through Amazon Bedrock.

Amazon Titan models support the following unique inference parameters in addition to temperature, Top P, and response length, which are common parameters across multiple models.

**Stop sequences**

With stop sequences (stopSequences), you can specify character sequences to indicate where the model should stop. Use the pipe symbol (|) to separate different sequences (maximum 20 characters).

**Amazon Titan Text**

Amazon Titan Text is a generative LLM for tasks such as summarization, text generation, classification, open-ended question answering, and information extraction. The text generation model is trained on many different programming languages and Rich Text Format (RTF), like tables, JSON, comma-separated values (CSV), and others. 

``` 
Input
{
     "inputText": "<prompt>",
     "textGenerationConfig" : {
          "maxTokenCount": 512,
          "stopSequences": [],
          "temperature": 0.1,
          "topP": 0.9
     }
} 
```

The following example shows the output from Amazon Titan Text for the input supplied in the previous code block. The model returns the output along with parameters, such as the number of input and output tokens generated. 

```
Output
{
     "inputTextTokenCount": 613,
     "results": [{
          "tokenCount": 219,
          "outputText": "<output>"
     }]
} 
```

**Amazon Titan Embeddings**

The Amazon Titan Embeddings model translates text inputs (words and phrases) into numerical representations (embeddings). Applications of this model include personalization and search. Comparing embeddings produces more relevant and contextual responses than word matching.

```
Input
{
     body = json.dumps({"inputText": <prompt>,})
     model_id = 'amazon.titan-embed-text-v1'
     accept = 'application/json'
     content_type = 'application/json'
     response = bedrock_runtime.invoke_model(
          body=body,
          modelId=model_id,
          accept=accept,
          contentType=content_type )
     response_body = json.loads(response['body'].read())
     embedding = response_body.get('embedding')
} 
```

This will generate an embeddings vector consisting of numbers that look like the following output.

```
Output
[0.82421875, -0.6953125, -0.115722656, 0.87890625, 0.05883789, -0.020385742, 0.32421875, -0.00078201294, -0.40234375, 0.44140625, ...] 
```

**AI21 Jurassic-2 (Mid and Ultra)**
Common parameters for Jurassic-2 models include temperature, Top P, and stop sequences. Jurassic-2 models support the following unique parameters to control randomness, diversity, length, or repetition in the response:
- **Max completion length (maxTokens)**: Specify the maximum number of tokens to use in the generated response.
- **Presence penalty (presencePenalty)**: Use a higher value to lower the probability of generating new tokens that already appear at least once in the prompt or in the completion.
- **Count penalty (countPenalty)**: Use a higher value to lower the probability of generating new tokens that already appear at least once in the prompt or in the completion. The value is proportional to the number of appearances.
- **Frequency penalty (frequencyPenalty)**: Use a higher value to lower the probability of generating new tokens that already appear at least once in the prompt or in the completion. The value is proportional to the frequency of the token appearances (normalized to text length).
- **Penalize special tokens**: Reduce the probability of repetition of special characters. The default values are true as follows:
    - **Whitespaces (applyToWhitespaces)**: A **true** value applies the penalty to white spaces and new lines.
    - **Punctuations (applyToPunctuation)**: A **true** value applies the penalty to punctuation.
    - **Numbers (applyToNumbers)**: A **true** value applies the penalty to numbers.
    - **Stop words (applyToStopwords)**: A **true** value applies the penalty to stop words.
    - **Emojis (applyToEmojis)**: A **true** value excludes emojis from the penalty.

**Jurassic-2 Mid**
This is a mid-sized model that is optimized to follow natural language instructions and context, so there is no need to provide it with any examples. It is ideal for composing human-like text and solving complex language tasks, such as question answering, and summarization. 

**Jurassic-2 Ultra**
Ultra is a large-sized model that you can apply to language comprehension or generation tasks. Use cases include generating marketing copy, powering chatbots, assisting with creative writing, performing summarization, and extracting information.

```
Input
{
     "prompt": "<prompt>",
     "maxTokens": 200,
     "temperature": 0.5,
     "topP": 0.5,
     "stopSequences": [],
     "countPenalty": {"scale": 0},
     "presencePenalty": {"scale": 0},
     "frequencyPenalty": {"scale": 0}
} 
```

```
Output
{
     "id": 1234,
     "prompt": {
          "text": "<prompt>",
          "tokens": [
               {
                    "generatedToken": {
                         "token": "\u2581who\u2581is",
                         "logprob": -12.980147361755371,
                         "raw_logprob": -12.980147361755371
                    },
                    "topTokens": null,
                    "textRange": {"start": 0, "end": 6}
               },
               //...
          ]
     },
     "completions": [
          {
               "data": {
                    "text": "<output>",
                    "tokens": [
                         {
                              "generatedToken": {
                                   "token": "<|newline|>",
                                   "logprob": 0.0,
                                   "raw_logprob": -0.01293118204921484
                              },
                              "topTokens": null,
                              "textRange": {"start": 0, "end": 1}
                         },
                         //...
                    ]
               },
               "finishReason": {"reason": "endoftext"}
          }
     ]
} 
```

**Anthropic Claude 2**
Anthropic Claude 2 is another model available for text generation on Amazon Bedrock. Claude is a generative AI model by Anthropic. It is purpose built for conversations, summarization, question answering, workflow automation, coding, and more. It supports everything from sophisticated dialogue and creative content generation to detailed instruction following.

Claude uses common parameters, such as temperature, Top P, Top K, and stop sequences. In addition, Claude models use the following unique parameter to further tune the response output. 
- Maximum length (max_tokens_to_sample): Specify the maximum number of tokens to use in the generated response.

The following example shows an input configuration used to invoke a response from Anthropic Claude 2 using Amazon Bedrock.

```
Input

{
     "prompt": "\n\nHuman:<prompt>\n\nAnswer:",
     "max_tokens_to_sample": 300,
     "temperature": 0.5,
     "top_k": 250,
     "top_p": 1,
     "stop_sequences": ["\n\nHuman:"]
} 
```

```
Output
{
     "completion": "<output>",
     "stop_reason": "stop_sequence"
} 
```

#### Cohere Command

Command is the flagship text generation model by Cohere. It is trained to follow user commands and be useful instantly in practical business applications, such as summarization, copywriting, dialogue, extraction, and question answering. Optimized for business priorities, Cohere is System and Organizations Control (SOC) 2 compliant and emphasizes security, privacy, and responsible AI.

In addition to temperature, Top P, Top K, maximum length, and stop sequences, the Cohere Command model supports the following unique controls: 
- **Return likelihoods (return_likelihoods)**: Specify how and if the token likelihoods are returned with the response. You can specify the following options:
    - **GENERATION**: This option only returns likelihoods for generated tokens.
    - **ALL**: This option returns likelihoods for all tokens.
    - **NONE**: This option doesn’t return any likelihoods. This is the default option.
- **Stream (stream)**: Specify true to return the response piece by piece in real time and false to return the complete response after the process finishes.

The following example shows an input configuration used to invoke a response from Cohere Command using Amazon Bedrock. 

```
Input 

{
"prompt": "string",
"temperature": float,
"p": float,
"k": float,
"max_tokens": int,
"stop_sequences": ["string"],
"return_likelihoods": "GENERATION|ALL|NONE",
"stream": boolean,
"num_generations": int
} 
```

#### Amazon Bedrock set up and configuration related APIs

***ListFoundationModels***

This method is used to provide a list of Amazon Bedrock foundation models that you can use. The following example demonstrates how to list the base models using Python.

``` 
Input

%pip install --upgrade boto3
import boto3
import json
bedrock = boto3.client(service_name='bedrock')
model_list=bedrock.list_foundation_models()
for x in range(len(model_list.get('modelSummaries'))):
     print(model_list.get('modelSummaries')[x]['modelId'])
```

You get a list of all the foundation models available on Amazon Bedrock and their respective metadata information. Following is an example of the output filtered on the model ID. 

```
Output
amazon.titan-tg1-large
amazon.titan-e1t-medium
amazon.titan-embed-g1-text-02
amazon.titan-text-express-v1
amazon.titan-embed-text-v1
stability.stable-diffusion-xl
stability.stable-diffusion-xl-v0
ai21.j2-grande-instruct
ai21.j2-jumbo-instruct
ai21.j2-mid
ai21.j2-mid-v1
ai21.j2-ultra
ai21.j2-ultra-v1
anthropic.claude-instant-v1
anthropic.claude-v1
anthropic.claude-v2
cohere.command-text-v14
```

#### Amazon Bedrock runtime-related APIs

***InvokeModel***
This API invokes the specified Amazon Bedrock model to run inference using the input provided in the request body. You use **InvokeModel** to run inference for text models, image models, and embedding models.

**Run inference on a text model**
You can send an invoke request to run inference on a model. Set the **accept** parameter to accept any content type in the response.

The following example details how to generate text with Python using the prompt **"What is Amazon Bedrock?"**

```
Input

bedrock_rt = boto3.client(service_name='bedrock-runtime')
prompt = "What is Amazon Bedrock?"
configs= {
"inputText": prompt,
"textGenerationConfig": {
"maxTokenCount": 4096,
"stopSequences": [],
"temperature":0,
"topP":1
}
}
body=json.dumps(configs)
modelId = 'amazon.titan-tg1-large'
accept = 'application/json'
contentType = 'application/json'
response = bedrock_rt.invoke_model(
     body=body,
     modelId=modelId,
     accept=accept,
     contentType=contentType
)
response_body = json.loads(response.get('body').read())
print(response_body.get('results')[0].get('outputText'))
```

**Sample output**

> Amazon Bedrock is a managed service that makes foundation models from leading AI startups and Amazon Titan models available through APIs. For up-to-date information on Amazon Bedrock and how to use it, see the provided documentation and relevant FAQs.

**InvokeModelWithResponseStream**
This API invokes the specified Amazon Bedrock model to run inference using the input provided. It returns the response in a stream.

For streaming, you can set **x-amzn-bedrock-accept-type** in the header to contain the required content type of the response. In the following example, the header is set to accept any content type. The default value is **application/json**.

The example details how to generate streaming text with Python. It uses the Amazon titan-tg1-large model and the prompt "**Write an essay for living on Mars using 10 sentences.**" 

```
Input

prompt = "Write an essay for living on Mars using 10 sentences."

configs= {
     "inputText": prompt,
     "textGenerationConfig": {
          "temperature":0
     }
}

body=json.dumps(configs)

accept = 'application/json'
contentType = 'application/json'
modelId = 'amazon.titan-tg1-large'

response = bedrock_rt.invoke_model_with_response_stream(
     modelId=modelId,
     body=body,
     accept=accept,
     contentType=contentType
)

stream = response.get('body')
if stream:
     for event in stream:
          chunk = event.get('chunk')
          if chunk:
               print((json.loads(chunk.get('bytes').decode())))
```

**Sample output**

> {'outputText': "\nIt is difficult to imagine life on Mars because the planet is so different from Earth. The environment on Mars is extremely cold, dry, and dusty, making it difficult for organisms to survive without specialized adaptations. The planet's low gravity also affec", 'index': 0, 'totalOutputTextTokenCount': None, 'completionReason': None, 'inputTextTokenCount': 12}
> {'outputText': 'ts human physical and mental health, requiring special accommodations. However, with proper planning and preparation, it is possible for humans to live on Mars. To establish a sustainable colony on Mars, astronauts would need to live in specially designed habitats, wear protective gear, and rely on artificial systems for food, water, and air. Communication with Earth would be limited, and astronauts would need to be self-sufficient', 'index': 0, 'totalOutputTextTokenCount': 128, 'completionReason': 'LENGTH', 'inputTextTokenCount': None}

#### Data Protection and Auditability

**Comprehensive data protection and privacy**

Amazon Bedrock provides comprehensive data protection and privacy. Your data used with Amazon Bedrock is not used for service improvement and is not shared with third-party model providers. You can use AWS PrivateLink with Amazon Bedrock to establish private connectivity between your FMs and your virtual private cloud (VPC) without exposing your traffic to the internet.

Your data is encrypted in transit and at rest. You can customize FMs privately so you can control how your data is used and encrypted. Amazon Bedrock makes a separate copy of the base foundation model and trains the private copy of the model.

**Secure your generative AI applications**

To secure your custom FMs, you can use AWS security services to form your defense in depth security strategy. Your customized FMs are encrypted using AWS Key Management Service (AWS KMS) keys, and they are stored encrypted.

By using AWS Identity and Access Management (IAM), you can control access to your customized FMs. You can allow or deny access to specific FMs, decide which services can get inferences, and choose who can log in to the Amazon Bedrock console.

**Support for governance and auditability**

Amazon Bedrock offers comprehensive monitoring and logging capabilities and tools you can use to address your governance and audit requirements.

You can use Amazon CloudWatch to track usage metrics and build customized dashboards with metrics that you require for your audit purposes. Use AWS CloudTrail to monitor API activity and troubleshoot issues as you integrate other systems into your generative AI applications.


