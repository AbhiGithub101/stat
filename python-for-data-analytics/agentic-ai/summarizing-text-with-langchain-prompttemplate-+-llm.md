---
description: >-
  In this section, we'll build our first real LangChain chain — one that takes a
  block of text and generates a summary along with interesting facts about the
  subject. Along the way, you'll learn two of
---

# Summarizing Text with LangChain: PromptTemplate + LLM

### 1. The Problem We're Solving

We have a long piece of text (for example, a Wikipedia biography) and we want an LLM to:

1. Generate a short summary
2. Extract a few interesting facts

Instead of hardcoding the text into a prompt every time, we want a **reusable, dynamic** way to plug different inputs into the same prompt structure.

***

### 2. Why Not Just Use an F-String?

A plain Python f-string could technically do the job:

```python
prompt = f"given the information {information} about a person, create a summary."
```

This works, but it doesn't scale well for production applications. LangChain provides a dedicated `PromptTemplate` class instead, for four key reasons:

| Benefit                 | Description                                                                                                                                                                        |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Validation**          | Enforces that you supply exactly the variables the template expects. A missing or misspelled variable raises a clear error instead of silently sending a broken prompt to the LLM. |
| **Reusability**         | The same template object can be reused across multiple chains.                                                                                                                     |
| **First-class citizen** | Prompts built with `PromptTemplate` are automatically logged and traced by tools like LangSmith, making debugging much easier.                                                     |
| **Safety**              | Enforced structure makes the prompt more resistant to prompt injection — especially important when combined with output parsers later in the course.                               |

> **Rule of thumb:** F-strings are fine for quick scripts. For reliable, production-grade LangChain applications, use `PromptTemplate`.

***

### 3. Defining the Input and the Template

```python
information = """...long biography text..."""

summary_template = """
    given the information {information} about a person I want you to create:
    1. A short summary
    2. Four interesting facts about them
    """
```

* `information` — the raw text we want the LLM to process.
* `summary_template` — a string containing a **placeholder**, `{information}`, which will be substituted with real data at runtime.

***

### 4. Creating the PromptTemplate Object

```python
from langchain_core.prompts import PromptTemplate

summary_prompt_template = PromptTemplate(
    input_variables=["information"], template=summary_template
)
```

| Parameter         | Purpose                                                                                                         |
| ----------------- | --------------------------------------------------------------------------------------------------------------- |
| `input_variables` | A list of variable names the template expects. Must exactly match the placeholders (`{...}`) inside `template`. |
| `template`        | The actual prompt string containing one or more placeholders.                                                   |

> ⚠️ **Common mistake:** If `input_variables` doesn't match the placeholder names in `template` (e.g. a typo), `PromptTemplate` raises an error immediately — which is intentional. It's far better to catch this at template-creation time than to send an incomplete prompt to the LLM.

***

### 5. Creating the LLM Object

```python
llm = ChatNVIDIA(temperature=0, model="meta/llama-3.1-8b-instruct")
```

> The same pattern works with `ChatOpenAI`, `ChatOllama`, or any other LangChain-supported chat model — only the class changes, the rest of your code stays identical.

#### Understanding `temperature`

`temperature` controls how deterministic vs. creative the model's output is:

| Range       | Behavior                           | Best for                                              |
| ----------- | ---------------------------------- | ----------------------------------------------------- |
| `0.0 – 0.3` | Deterministic, factual, repeatable | Summarization, code generation, instructions, testing |
| `0.8 – 1.0` | Creative, varied, less predictable | Poetry, fiction, brainstorming                        |

For this summarization task, we use `temperature=0` since we want consistent, factual output.

> **Note on API keys:** LangChain automatically looks for the relevant environment variable (e.g. `OPENAI_API_KEY`, `NVIDIA_API_KEY`) once it's loaded via `load_dotenv()`. You don't need to pass it manually.

***

### 6. Building the Chain — LCEL and the Pipe Operator

```python
chain = summary_prompt_template | llm
```

This single line uses **LCEL (LangChain Expression Language)**. The `|` operator connects two components so that:

> **The output of the left-hand component becomes the input of the right-hand component.**

In this case:

1. `summary_prompt_template` formats the `information` input into a complete prompt string.
2. That formatted prompt string is automatically passed as input to `llm`.
3. `llm` processes the prompt and generates a response.

#### The "Runnable" Concept

When you combine components with `|`, LangChain creates a new object called a **Runnable**. Every Runnable shares a common interface, which gives you a standard method: `.invoke()`.

> 💡 **Analogy:** Think of it as an assembly line. Station 1 (`PromptTemplate`) takes raw material (`information`) and produces a packaged product (a formatted prompt). The conveyor belt (`|`) carries it to Station 2 (`llm`), which produces the final output (the response).

This is also the origin of the name **"LangChain"** — components are _chained_ together so output flows automatically into the next step's input.

***

### 7. Running the Chain with `.invoke()`

```python
response = chain.invoke(input={"information": information})
```

What happens internally when this runs:

1. LangChain calls `summary_prompt_template.invoke()` with the dictionary `{"information": information}`.
2. The placeholder is filled in, producing a `PromptValue` (essentially a formatted string).
3. That `PromptValue` is passed — via the pipe operator — into `llm.invoke()`.
4. The LLM processes the final prompt string and returns a response.

```python
print(response.content)
```

`response` is an object, not a plain string. The `.content` attribute holds the actual generated text.

***

### 8. Full Code Reference

```python
from dotenv import load_dotenv
from langchain_core.prompts import PromptTemplate
from langchain_nvidia_ai_endpoints import ChatNVIDIA

load_dotenv()

def main():
    information = """...biography text..."""

    summary_template = """
        given the information {information} about a person I want you to create:
        1. A short summary
        2. Four interesting facts about them
        """

    summary_prompt_template = PromptTemplate(
        input_variables=["information"], template=summary_template
    )

    llm = ChatNVIDIA(temperature=0, model="meta/llama-3.1-8b-instruct")
    chain = summary_prompt_template | llm

    response = chain.invoke(input={"information": information})
    print(response.content)

main()
```

***

### 9. Key Takeaways

* Use `PromptTemplate` instead of f-strings for validation, reusability, traceability, and safety against prompt injection.
* `temperature` controls how deterministic (`0`) vs. creative (`1`) the model's output is.
* The `|` operator builds a **Runnable** chain: left-hand output becomes right-hand input.
* `.invoke()` runs the chain end-to-end and returns a response object; use `.content` to get the generated text.

***

### What's Next

* **Debugging and Tracing** this chain to inspect each step visually
* **LangSmith Integration** for automatic tracing of every chain run
* **Local Open-Weights Models with Ollama** — running models locally without an API key
