---
description: >-
  Set up a LangChain project in PyCharm, configure .env and .gitignore, and
  connect the project to GitHub.
---

# Set up LangChain in PyCharm

## Set up LangChain in PyCharm

### Overview

This guide helps you create a LangChain project in PyCharm.

By the end, you will have:

* a new Python project
* LangChain installed
* one model provider installed
* a GitHub repository connected
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
* Git
* a GitHub account — optional if you do not want to push yet

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

If you want broader Python defaults, copy the Python `.gitignore` template from GitHub into your local `.gitignore`.

Use this when you want standard Python ignore rules from the start.

After pasting that template, make sure `.env` is still included.

### Optional: Connect the project to GitHub

Do this after `git init` and after your local `.gitignore` is ready.

Use this flow when you want to back up the project, collaborate, or push code to GitHub.

#### 1. Create an empty repository on GitHub

Create a new repository on GitHub.

Keep it empty if possible.

Do not add a README, `.gitignore`, or license yet.

This keeps the first push simple.

#### 2. Copy the repository HTTPS URL

Open the new repository page on GitHub.

Click **Code** and copy the HTTPS URL.

It looks like this:

```
https://github.com/your-username/your-repo.git
```

Use this URL in the next step.

#### 3. Connect the local project to GitHub

Run this command in the project folder:

```bash
git remote add origin <repo-url>
```

Example:

```bash
git remote add origin https://github.com/your-username/your-repo.git
```

Use this once per local repository.

It links your local Git project to the GitHub repository.

#### 4. Add all project files to Git

Run:

```bash
git add .
```

Use this when your initial files are ready to commit.

It stages the current project files.

#### 5. Create the first commit

Run:

```bash
git commit -m "initial project setup"
```

Use this after staging files with `git add .`.

It saves the current project state in Git history.

#### 6. Set the branch name to `main`

Run:

```bash
git branch -M main
```

Use this before the first push if you want the default branch to be `main`.

This renames the current branch to `main`.

#### 7. Push the project to GitHub

If the GitHub repository is empty, run:

```bash
git push -u origin main
```

Use `-u` on the first push only.

It sets `origin/main` as the default upstream branch.

If the remote repository already has its own first commit, and you want your local project to replace it, run:

```bash
git push -u origin main --force
```

Use `--force` only when you intentionally want to overwrite remote history.

{% hint style="warning" %}
`git push --force` replaces the remote branch history. Avoid it on shared repositories unless you are sure.
{% endhint %}

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
