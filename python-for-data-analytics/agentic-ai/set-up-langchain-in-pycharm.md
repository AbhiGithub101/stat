---
description: >-
  PyCharm me LangChain project setup karein, dependencies install karein, aur
  .env aur .gitignore configure karein.
---

# Set up LangChain in PyCharm

### Overview

Is guide me aap PyCharm me LangChain course repository clone karenge, required packages install karenge, aur project ko local development ke liye ready karenge.

### Prerequisites

Start karne se pehle ye tools installed hone chahiye:

* PyCharm
* Git
* Python
* `uv`
* API key for your model provider, jaise OpenAI

### Step 1: Repository clone karein

Sabse pehle LangChain course repository clone karein:

[Course repository](https://github.com/emarco177/langchain-course)

Terminal me ye command run karein:

```bash
git clone https://github.com/emarco177/langchain-course.git
```

Command successful hone ke baad aapko `Cloning into 'langchain-course'...` jaisa message dikhega.

<figure><img src="../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

### Step 2: Project ko PyCharm me open karein

Clone complete hone ke baad PyCharm me **Open** par click karein aur `langchain-course` folder select karein.

Ab project files PyCharm ke project panel me dikhni chahiye.

<figure><img src="../../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

### Step 3: `uv` aur LangChain install karein

Agar `uv` abhi installed nahi hai, to pehle system par install karein. Uske baad project terminal me dependencies add karein.

```bash
uv init
uv add langchain
```

`uv add langchain` run karne ke baad LangChain install ho jayega aur project me `.venv` folder create ho sakta hai.

<figure><img src="../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

### Step 4: Model provider package install karein

Agar aap OpenAI use kar rahe hain, to ye package install karein:

```bash
uv add langchain-openai
```

Ye package LangChain ke core package ke saath bundled nahi aata. Har model provider ka alag integration package hota hai. Example:

* OpenAI
* Anthropic
* Gemini

Isliye jo provider aap use karna chahte hain, uska package separately install karein.

### Step 5: Utility packages install karein

Ab environment variables aur code formatting ke liye ye packages install karein:

```bash
uv add python-dotenv black isort
```

Inka use:

* `python-dotenv` — `.env` file se environment variables load karta hai
* `black` — code formatting ke liye
* `isort` — imports ko sort karne ke liye

<figure><img src="../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

Installed packages ko aap `pyproject.toml` file me verify kar sakte hain.

<figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

### Step 6: `.gitignore` file banayein

Ab project root me `.gitignore` file create karein.

Reference ke liye ye example use kar sakte hain:

[Example .gitignore](https://github.com/emarco177/langchain-course/blob/3ec917104d438a5903db58c96abe18ab2103c6c8/.gitignore)

Is file me un folders aur files ko add kiya jata hai jinhe Git track nahi karega, jaise:

* `.venv`
* `.env`
* cache files

### Step 7: `.env` file banayein

Ab `.env` file create karein aur usme apni API keys store karein.

Example:

```bash
OPENAI_API_KEY=your_api_key_here
```

`.env` file sensitive values ke liye hoti hai. Isse public repository me commit nahi karna chahiye.

### Step 8: Setup verify karein

Setup complete hone ke baad ye check karein:

* repository PyCharm me open ho rahi hai
* dependencies `pyproject.toml` me dikh rahi hain
* `.venv` create ho chuka hai
* `.env` file me required API key present hai

### Next step

Ab aap basic LangChain scripts run kar sakte hain aur apna first agent ya chat model integration build kar sakte hain.
