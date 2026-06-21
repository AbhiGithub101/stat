---
description: >-
  Set up a LangChain project in PyCharm, install dependencies, and configure
  .env and .gitignore files.
---

# Set up LangChain in PyCharm

### Overview

This guide helps you set up LangChain in PyCharm.

You will clone the project, install packages, and prepare local files.

### Prerequisites

Install these tools before you start:

* PyCharm
* Git
* Python
* `uv`
* An API key for your model provider, such as OpenAI

### Step 1: Clone the repository

Clone the LangChain course repository first:

[Course repository](https://github.com/emarco177/langchain-course)

Run this command in the terminal:

```bash
git clone https://github.com/emarco177/langchain-course.git
```

If the command works, you will see a message like `Cloning into 'langchain-course'...`.

<figure><img src="../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

### Step 2: Open the project in PyCharm

After cloning, open PyCharm.

Click **Open** and select the `langchain-course` folder.

You should now see the project files in the sidebar.

<figure><img src="../../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

### Step 3: Initialize the project and install LangChain

If `uv` is not installed yet, install it first.

Then run these commands inside the project terminal:

```bash
uv init
uv add langchain
```

`uv init` creates the project setup files.

`uv add langchain` installs LangChain.

It may also create a `.venv` folder for the virtual environment.

<figure><img src="../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

### Step 4: Install the model provider package

If you use OpenAI, install this package:

```bash
uv add langchain-openai
```

This package is not included in the core LangChain package.

Each provider has its own integration package.

Examples:

* OpenAI
* Anthropic
* Gemini

Install the package for the provider you plan to use.

### Step 5: Install utility packages

Now install a few helpful packages:

```bash
uv add python-dotenv black isort
```

What they do:

* `python-dotenv` loads values from the `.env` file
* `black` formats your code
* `isort` sorts your imports

<figure><img src="../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

You can confirm the installed packages in `pyproject.toml`.

<figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

### Step 6: Create a `.gitignore` file

Create a `.gitignore` file in the project root.

You can use this example as a reference:

[Example .gitignore](https://github.com/emarco177/langchain-course/blob/3ec917104d438a5903db58c96abe18ab2103c6c8/.gitignore)

This file tells Git which files to ignore.

Common examples:

* `.venv`
* `.env`
* cache files

### Step 7: Create a `.env` file

Create a `.env` file for secret values.

Store your API keys in this file.

Example:

```bash
OPENAI_API_KEY=your_api_key_here
```

Do not commit this file to a public repository.

### Step 8: Verify the setup

Check these points after setup:

* The repository opens in PyCharm
* Dependencies appear in `pyproject.toml`
* The `.venv` folder exists
* The `.env` file contains your API key

### Next step

You can now run basic LangChain scripts.

You are also ready to build your first agent or chat model integration.
