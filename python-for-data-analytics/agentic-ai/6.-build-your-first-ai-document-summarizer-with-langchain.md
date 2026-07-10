---
description: >-
  Learn how to load a PDF, extract its content, create reusable prompts, and
  prepare an AI-powered document summarizer using LangChain.
---

# Build Your First AI Document Summarizer with LangChain

### Overview

Now that you've learned about Chat Models, Prompt Templates, and Chains, it's time to build your first real LangChain application.

In this lesson, you'll build an AI-powered document summarizer that can analyze a PDF and generate a structured summary.

Although this project is simple, it introduces the same workflow you'll use to build more advanced AI agents later in this course.

By the end of this lesson, you'll learn how to:

* Load a PDF document using LangChain
* Extract text from the document
* Create reusable prompts with Prompt Templates
* Connect the prompt to an AI model

***

## Final Output

Our application will take a PDF document as input.

For example:

* Tax Notice
* Invoice
* Research Paper
* Meeting Notes
* Legal Document

The AI will generate:

* A concise summary
* Key points
* Important dates and figures
* Required actions
* Risks or consequences

The same workflow can summarize almost any PDF document by simply changing the file.

***

## The Problem

Imagine you're building an AI Document Assistant.

A user uploads a PDF and asks:

> "Summarize this document and tell me the important information."

The document could be completely different every time.

One user uploads a tax notice.

Another uploads a research paper.

Someone else uploads meeting notes.

The instruction stays the same.

Only the document changes.

Instead of copying and pasting the document into our code every time, we'll load it directly from a PDF file and send it to the AI model.

This approach is much more practical and closer to how real-world AI applications work.

***

## Project Workflow

Our application follows this workflow.

```
PDF Document
      │
      ▼
PyPDFLoader
      │
      ▼
Extract Text
      │
      ▼
Prompt Template
      │
      ▼
Chat Model
      │
      ▼
Structured Summary
```

Each component has a specific responsibility.

* PyPDFLoader reads the PDF.
* PromptTemplate creates the prompt.
* Chat Model sends the prompt to the AI model.
* The AI returns a structured summary.

***

## Step 1: Load the PDF Document

The first step is loading the PDF.

LangChain provides different document loaders for different file types.

Since we're working with PDF files, we'll use **PyPDFLoader**.

```python
from langchain_community.document_loaders import PyPDFLoader

loader = PyPDFLoader("documents/income_tax_notice.pdf")

documents = loader.load()
```

`loader.load()` reads the PDF and returns a list of `Document` objects.

Each page of the PDF becomes a separate `Document`.

***

## Convert the PDF into Text

Our AI model expects plain text, not Document objects.

We'll combine all pages into a single string.

```python
document_text = "\n".join(
    document.page_content
    for document in documents
)
```

Now the entire PDF is stored inside the `document_text` variable.

This text will be sent to the Prompt Template in the next step.

> 💡 **Note**
>
> In this lesson, we're using **PyPDFLoader** because PDF is one of the most common document formats in real-world applications.
>
> LangChain also supports many other document loaders, including TXT, Word, CSV, Excel, HTML, websites, and entire folders.
>
> We'll explore those document loaders in detail later in this course.

***

## Step 2: Create the Prompt Template

Now let's create a reusable prompt.

```python
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
```

Notice the placeholder.

```
{document_text}
```

Every time a new PDF is loaded, LangChain replaces this placeholder with the extracted text.

The instructions stay the same.

Only the document changes.

***

## Step 3: Create the PromptTemplate Object

Convert the template into a LangChain `PromptTemplate`.

```python
from langchain_core.prompts import PromptTemplate

summary_prompt_template = PromptTemplate(
    input_variables=["document_text"],
    template=summary_template
)
```

Here:

* `template` stores the prompt.
* `input_variables` defines the placeholders that will be replaced at runtime.

The placeholder name must exactly match the name inside the template.

For example:

```
{document_text}
```

must match

```python
input_variables=["document_text"]
```

If the names don't match, LangChain raises an error before sending the prompt to the AI model.

This helps catch mistakes early.

***

## Step 4: Create the Chat Model

Now create the Chat Model.

```python
from langchain_nvidia_ai_endpoints import ChatNVIDIA

llm = ChatNVIDIA(
    model="meta/llama-3.1-8b-instruct",
    temperature=0
)
```

The Chat Model is responsible for communicating with the AI model.

Although this example uses NVIDIA, the same workflow works with other providers, such as:

* OpenAI
* Anthropic
* Google Gemini
* Ollama

Only the Chat Model class changes.

The rest of your LangChain workflow remains almost identical.

***

## Understanding Temperature

The `temperature` parameter controls how predictable or creative the AI model's responses are.

| Temperature | Output                      |
| ----------: | --------------------------- |
|         `0` | More consistent and factual |
|         `1` | More creative and varied    |

Since we're summarizing documents, we want accurate and consistent responses.

That's why we use:

```python
temperature=0
```

***

## What You've Learned

In this lesson, you learned how to:

* Load a PDF document using PyPDFLoader
* Extract text from the PDF
* Create a reusable Prompt Template
* Build a PromptTemplate object
* Create a Chat Model
* Understand the purpose of the `temperature` parameter

Your application is now ready.

In the next lesson, you'll connect these components together using **LCEL (LangChain Expression Language)** and execute your first LangChain workflow.
