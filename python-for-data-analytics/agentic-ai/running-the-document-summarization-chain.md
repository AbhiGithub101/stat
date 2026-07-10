---
description: >-
  Learn how to connect PromptTemplate and Chat Models using LCEL, execute the
  workflow with invoke(), and generate structured summaries from PDF documents.
---

# Running the Document Summarization Chain

### Overview

In the previous lesson, you:

* Loaded a PDF using `PyPDFLoader`
* Extracted the document text
* Created a reusable Prompt Template
* Initialized a Chat Model

Now it's time to connect these components and generate a summary from the document.

By the end of this lesson, you'll learn how to:

* Build a LangChain Chain using LCEL
* Execute the chain
* Understand how data flows through the workflow
* Generate structured summaries from PDF documents

***

## Step 5: Build the Chain

Now that we have a Prompt Template and a Chat Model, we can connect them together.

```python
chain = summary_prompt_template | llm
```

This single line creates a LangChain workflow.

The pipe (`|`) operator connects both components together.

When the chain runs:

1. The Prompt Template creates the final prompt.
2. That prompt is automatically passed to the Chat Model.
3. The AI model generates the response.

You don't need to manually pass data between the components.

LangChain handles that automatically.

***

## How the Chain Works

The following diagram shows what happens behind the scenes.

```
PDF Document
      │
      ▼
PyPDFLoader
      │
      ▼
Extracted Text
      │
      ▼
Prompt Template
      │
      ▼
Chat Model
      │
      ▼
AI Response
```

Each component performs one specific task.

Together, they create a complete AI workflow.

***

## What is LCEL?

LCEL stands for **LangChain Expression Language**.

It is the modern and recommended way to build workflows in LangChain.

Instead of calling each component separately, LCEL allows you to connect them using the pipe (`|`) operator.

As your applications grow, you can continue adding more components to the same workflow.

***

## Step 6: Execute the Chain

Now execute the workflow.

```python
response = chain.invoke(
    {
        "document_text": document_text
    }
)
```

The `invoke()` method starts the entire workflow.

Behind the scenes, LangChain performs the following steps automatically.

1. The Prompt Template replaces the placeholder with the extracted document text.
2. The completed prompt is sent to the Chat Model.
3. The AI model analyzes the document.
4. The generated response is returned.

Everything happens with a single method call.

***

## Understanding `invoke()`

Think of `invoke()` as the **Start** button for your LangChain workflow.

Once you call it, every connected component executes in order.

```
document_text
      │
      ▼
Prompt Template
      │
      ▼
Chat Model
      │
      ▼
Response
```

As your future AI agents become more advanced, `invoke()` will continue to work in the same way.

The only difference is that your workflow will contain more components.

***

## Step 7: Display the Result

The Chat Model returns an AI response object.

To print only the generated text, use the `content` attribute.

```python
print(response.content)
```

Without `.content`, You'll receive the complete response object, which contains additional metadata.

For most applications, the generated text is what you need.

***

## Complete Code

```python
from dotenv import load_dotenv
from langchain_community.document_loaders import PyPDFLoader
from langchain_core.prompts import PromptTemplate
from langchain_nvidia_ai_endpoints import ChatNVIDIA

load_dotenv()

loader = PyPDFLoader("documents/income_tax_notice.pdf")
documents = loader.load()

document_text = ""

for document in documents:
    document_text += document.page_content + "\n"

summary_template = """
You are an expert document analyst.

Carefully analyze the following document.

{document_text}

Provide the following:

1. A concise 3–4 line summary.
2. The most important key points.
3. Any important dates, numbers, or figures.
4. Any action required.
5. Any risks or consequences mentioned.
"""

summary_prompt_template = PromptTemplate(
    input_variables=["document_text"],
    template=summary_template
)

llm = ChatNVIDIA(
    model="meta/llama-3.1-8b-instruct",
    temperature=0
)

chain = summary_prompt_template | llm

response = chain.invoke(
    {
        "document_text": document_text
    }
)

print(response.content)
```

***

## Sample Output

Your output will vary depending on the document.

For the income tax notice used in this lesson, the AI may generate a response similar to this.

```
Summary
The document is an Income Tax demand notice issued by the Income Tax Department for the Assessment Year 2023–24. It identifies discrepancies in the filed tax return and requests the taxpayer to respond within 30 days.

Key Points
• Interest income was not declared.
• Excess TDS credit was claimed.
• A portion of the Section 80C deduction was disallowed.
• Foreign remittance income was not reported.

Important Dates and Figures
• Assessment Year: 2023–24
• Response Deadline: Within 30 days
• Outstanding Tax Demand: ₹95,750

Action Required
Respond through the Income Tax e-filing portal by accepting or disputing the demand.

Risk
Failure to respond may result in recovery proceedings and penalties under the Income Tax Act.
```

***

## Think Like an AI Agent

An AI agent rarely performs a task in a single step.

Even this simple application follows a workflow.

* Read a document.
* Extract the text.
* Generate a prompt.
* Send it to the AI model.
* Return the response.

As you continue through this course, you'll expand this workflow by adding tools, memory, retrieval, and reasoning.

This is how modern AI agents are built.

***

## What You've Learned

After completing this project, you can now:

* Load PDF documents with LangChain.
* Extract text from a document.
* Create reusable Prompt Templates.
* Connect components using LCEL.
* Execute a LangChain workflow with `invoke()`.
* Generate structured summaries using an AI model.

***

## What's Next?

Congratulations! You've built your first LangChain application.

In the next chapter, you'll learn how to debug and trace your LangChain workflows using **LangSmith**, allowing you to inspect every step of your application's execution.
