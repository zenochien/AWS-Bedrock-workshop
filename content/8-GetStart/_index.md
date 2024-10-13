---
title : "How to get started with Amazon Bedrock"
weight : 8
chapter : false
pre : " <b> 8 </b> "
---

#### Amazon Bedrock tutorial

Let’s look at a demo to get a better taste of Bedrock’s capabilities. To follow along, check out this GitHub repository: [Amazon Bedrock – Introductory Demo](https://github.com/aws-samples/amazon-bedrock-intro-demo/tree/main). 

{{< callout "" >}}
 Running this demo will incur costs on your AWS account.
{{< /callout >}}

**Prerequisites**:

* AWS account (sandbox account recommended)
* IAM user or role with Administrator access or the required permissions to access Amazon Bedrock and its FMs. Configure this principal’s credentials in your environment’s default AWS profile (AWS_PROFILE). Also, ensure that you have enabled Model access on Amazon Bedrock.
* Python 3.9+
* Internet access

To get started, create a Python virtual environment:

```
python -m venv demo

cd demo

source bin/activate
```

Then, clone the repository and install the dependencies:

```
git clone https://github.com/aws-samples/amazon-bedrock-intro-demo.git

cd amazon-bedrock-intro-demo

pip install -r requirements.txt
```

Finally, launch the [streamlit](https://streamlit.io/) application:

```
streamlit run main.py
```

This command will open a new browser tab with the deployed application that looks like this:

![Bedrock](/images/9/1.png)

There, you will find several applications and use cases calling the Bedrock APIs for different models. Let’s take a look at some of them.

On the left side panel, select `QA – FM Comparison`, where you can choose any of the available models and compare them for QA use cases. In this case, I am comparing the `amazon.titan-tg1-large` and `anthropic.claude-v2`:

![Bedrock](/images/9/2.png)

Feel free to play around and experiment with different models and different questions. Next, let’s check the `Chat – FMs` option. This time, I opted for the `meta.llama2-13b-chat-v1` model and asked it to explain cloud computing like I am five years old.

![Bedrock](/images/9/3.png)

Moving to the `Code Translation` option allows us to translate code blocks from one programming language to another. I used a Javascript function that checks if a number is prime and opted to translate it to Python as an example:

![Bedrock](/images/9/4.png)

Lastly, let’s explore the `RAG – Document(s)` option, which allows you to upload a PDF document and answer questions or retrieve information based on the document. It even shows you a comparison of the model’s answer with and without the RAG technique. 

As for the document to use, I uploaded the [European’s Parliament Artificial Intelligence Act](https://www.europarl.europa.eu/doceo/document/TA-9-2023-0236_EN.pdf) and asked it to summarize the contents of the document. Note that the model is unaware of this document without using RAG, and its answer is entirely irrelevant. On the other hand, using the RAG method and leveraging the document, the answer was quite on point:

![Bedrock](/images/9/5.png)
