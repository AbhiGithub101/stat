---
description: >-
  Start your LangChain journey by learning Chat Models, Prompt Templates, and
  Chains. These core concepts are the foundation of modern AI applications.
---

# LangChain Fundamentals

## LangChain Fundamentals: Chat Models, Prompt Templates & Chains

Learn the three core building blocks of LangChain that are used to build modern AI applications. In this chapter, you’ll understand what LangChain is, why it is widely used, and how Chat Models, Prompt Templates, and Chains work together.

### What is LangChain?

LangChain is an open-source framework for building applications powered by Large Language Models (LLMs). Instead of writing complex logic from scratch, LangChain provides reusable components that simplify AI application development.

It helps developers:

* Work with different LLM providers using a common interface.
* Build dynamic prompts.
* Connect multiple AI components into workflows.
* Integrate external tools and data sources.
* Build scalable, production-ready AI applications.

### Why Use LangChain?

Making a single API call to an LLM is easy. Building a complete AI application is much more complex.

A real-world AI application often needs to:

* Generate prompts dynamically.
* Switch between different LLM providers.
* Process multiple steps in sequence.
* Connect with external tools.
* Work with custom documents and data.
* Keep the code clean and maintainable.

LangChain provides reusable modules that solve these problems.

## Core Building Blocks

In this chapter, we’ll focus on three fundamental LangChain components:

1. Chat Models
2. Prompt Templates
3. Chains (LCEL)

These building blocks are used in almost every LangChain application.

### Chat Models

A Chat Model is the interface used to communicate with an LLM.

Instead of learning a different API for every provider, LangChain provides a unified interface. This makes it easy to switch between providers such as Anthropic, OpenAI, Google Gemini, or local models running with Ollama.

#### Example

```
from langchain_anthropic import ChatAnthropic
model = ChatAnthropic( model="claude-sonnet-4-6")
response = model.invoke( "Explain LangChain in one sentence.")
print(response.content)
```

#### Benefits

* Unified interface
* Easy model switching
* Cleaner application code
* Less vendor lock-in

{% hint style="info" %}
Before using a Chat Model, make sure your API key is configured correctly.
{% endhint %}

### Prompt Templates

Prompt Templates allow you to create dynamic and reusable prompts.

Instead of writing a new prompt every time, you create a template once and provide different input values whenever needed.

#### Example

```
from langchain_core.prompts import ChatPromptTemplate
template = ChatPromptTemplate.from_template( "Write a Python function to {task}.")
prompt = template.invoke( { "task": "check whether a string is a palindrome" })
```

#### Benefits

* Dynamic prompts
* Reusable prompt structure
* Better maintainability
* Cleaner code

### Chains (LCEL)

A Chain connects multiple components into a single workflow.

The output of one component automatically becomes the input of the next component.

LangChain recommends using **LCEL (LangChain Expression Language)**, which connects components using the pipe (|) operator.

#### Example

```
from langchain_core.output_parsers import StrOutputParser
chain = template | model | StrOutputParser()
result = chain.invoke( { "task": "check whether a string is a palindrome" })
print(result)
```

#### Workflow

Prompt Template\
↓\
Chat Model\
↓\
Output Parser\
↓\
Final Response

{% hint style="warning" %}
Older tutorials may use the LLMChain class. It has been deprecated. Use the LCEL pipe (|) syntax for new projects.
{% endhint %}

### Putting Everything Together

The real power of LangChain comes from combining these components.

```
from langchain_core.prompts import ChatPromptTemplate
from langchain_anthropic import ChatAnthropic
from langchain_core.output_parsers import StrOutputParser
template = ChatPromptTemplate.from_template( "Write a Python function to {task}.")
model = ChatAnthropic( model="claude-sonnet-4-6")
chain = template | model | StrOutputParser()
result = chain.invoke( { "task": "check whether a string is a palindrome" })
print(result)
```

This workflow follows three simple steps:

1. Create a prompt.
2. Send it to an LLM.
3. Parse the response.

### Key Takeaways

* LangChain is an open-source framework for building LLM-powered applications.
* Chat Models provide a common interface for multiple LLM providers.
* Prompt Templates create reusable and dynamic prompts.
* Chains combine multiple components into a single workflow.
* LCEL is the modern and recommended way to build LangChain pipelines.

### What’s Next?

Now that you understand the fundamentals, you’re ready to build real LangChain applications.

In the next chapters, you’ll learn how to:

* Build a Text Summarization Chain
* Debug and Trace LangChain Applications
* Run Local Models with Ollama
* Monitor Applications using LangSmith

These topics will help you move from basic concepts to production-ready AI applications.
