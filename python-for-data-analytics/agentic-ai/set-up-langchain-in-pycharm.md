---
description: >-
  Set up a LangChain project in PyCharm, install dependencies, and configure
  .env and .gitignore files.
---

# Set up LangChain in PyCharm

## Set up LangChain in PyCharm

### Overview

This guide helps you create a LangChain project in PyCharm.

By the end, you will have:

* a new Python project
* LangChain installed
* one model provider installed
* a working test script

### What is LangChain

LangChain is a Python library for building apps with AI models.

It is not a model itself.

It helps you organize prompts, model calls, tools, memory, and external data.

Use it when you want more than one simple API call.

Common use cases:

* chatbots
* PDF or document Q\&A
* agents that use tools step by step

Why use it:

* it keeps AI app code structured
* it makes provider integration easier
* it helps you build larger workflows later

### Prerequisites

Install these tools before you start:

* PyCharm
* Python `3.10+`
* `uv`
* an API key for your model provider
* Git — optional

### Step 1: Create a new project

Run these commands in a terminal:

```bash
mkdir langchain-project
cd langchain-project
git init
```

This creates a new project folder.

`git init` starts a Git repository.

If you do not want Git yet, skip `git init`.

### Step 2: Open the project in PyCharm

Open PyCharm.

Click **Open** and select the `langchain-project` folder.

You should now see the project in the left sidebar.

### Step 3: Initialize the Python project

Run this command in the PyCharm terminal:

```bash
uv init
```

This creates the project files.

You should now see a `pyproject.toml` file.

### Step 4: Install LangChain

Run this command:

```bash
uv add langchain python-dotenv
```

This installs:

* `langchain` for AI app development
* `python-dotenv` for loading values from `.env`

{% hint style="info" %}
`black` and `isort` are useful, but optional. Install them later if needed.
{% endhint %}

If you want code formatting tools, run:

```bash
uv add black isort
```

These tools help keep Python code clean:

* `black` formats code automatically
* `isort` sorts imports automatically

### Step 5: Install one model provider

LangChain uses separate packages for each provider.

Choose one provider and install its package.

{% tabs %}
{% tab title="OpenAI" %}
Run:

```bash
uv add langchain-openai
```

Add this to `.env`:

```bash
OPENAI_API_KEY=your_api_key_here
```
{% endtab %}

{% tab title="NVIDIA" %}
Run:

```bash
uv add langchain-nvidia-ai-endpoints
```

Add this to `.env`:

```bash
NVIDIA_API_KEY=nvapi-your_api_key_here
```

This is a good option if you want a free starter model.
{% endtab %}
{% endtabs %}

### Step 6: Create a `.gitignore` file

Create a `.gitignore` file in the project root.

Add this content:

```gitignore
.venv/
.env
__pycache__/
```

This prevents local and secret files from being committed.

### Step 7: Create `main.py`

Create a file named `main.py` in the project root.

Add one of these examples.

{% tabs %}
{% tab title="OpenAI" %}
```python
from dotenv import load_dotenv
from langchain_openai import ChatOpenAI

load_dotenv()

llm = ChatOpenAI(model="gpt-4o-mini")
response = llm.invoke("Hello")

print(response.content)
```
{% endtab %}

{% tab title="NVIDIA" %}
```python
from dotenv import load_dotenv
from langchain_nvidia_ai_endpoints import ChatNVIDIA

load_dotenv()

llm = ChatNVIDIA(
    model="nvidia/llama-3.3-nemotron-super-49b-v1"
)
response = llm.invoke("Hello")

print(response.content)
```
{% endtab %}
{% endtabs %}

This script loads your API key and sends a test prompt.

### Step 8: Run the test

Run this command in the terminal:

```bash
uv run python main.py
```

If everything is correct, the model returns a short response.

### Step 9: Verify the setup

Check these points:

* The project opens in PyCharm
* `pyproject.toml` exists
* `.env` contains your API key
* `main.py` runs without import errors
* The model returns a response

### Troubleshooting

#### `uv` command not found

Install `uv` First, then restart the terminal.The

#### API key is not working

Check the key name in `.env`.

Make sure there are no extra spaces around `=`.

#### Import error for provider package

Make sure you installed the same provider package that your code uses.

For example, `ChatOpenAI` needs `langchain-openai`.

### Next step

Your LangChain setup is now ready.

You can now build a chatbot, connect a document, or create your first agent.
