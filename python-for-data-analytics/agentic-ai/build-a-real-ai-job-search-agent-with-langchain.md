# Build a Real AI Job Search Agent with LangChain

### Watch the Video

Follow along with the complete implementation on YouTube, then use these notes as a quick reference while building the project.

{% embed url="https://www.youtube.com/watch?v=JYTPzwguBPw" %}

***

## Overview

In this project, we'll build a real AI Job Search Agent using LangChain, an NVIDIA LLM, and the JSearch API.

Instead of relying only on the LLM's knowledge, the agent fetches live job listings using a custom tool and presents them in a readable format.

By the end of this project, you'll understand how AI Agents use Tool Calling to interact with external APIs.

***

## What You'll Build

* Search live jobs
* Understand natural language queries
* Call an external API automatically
* Generate a clean response

***

## Tech Stack

| Technology    | Purpose               |
| ------------- | --------------------- |
| Python        | Programming Language  |
| LangChain     | AI Agent Framework    |
| NVIDIA API    | Large Language Model  |
| JSearch API   | Live Job Search       |
| Requests      | API Calls             |
| python-dotenv | Environment Variables |

***

### Required APIs

#### NVIDIA API

https://build.nvidia.com/

#### JSearch API

https://openwebninja.com/api/jsearch

***

## Install Dependencies

```bash
pip install langchain
pip install langchain-nvidia-ai-endpoints
pip install requests
pip install python-dotenv
```

***

## Project Structure

```
AI-Job-Search-Agent/
│
├── .env
├── main.py
└── requirements.txt
```

***

## Configure Environment Variables

Create a `.env` file.

```env
NVIDIA_API_KEY=your_nvidia_api_key
JSEARCH_API_KEY=your_jsearch_api_key
```

<mark style="color:$danger;">Never commit this file to GitHub.</mark>

***

## How It Works

```
User
   │
   ▼
AI Agent
   │
   ▼
Needs Live Data?
   │
   ├── No → Answer Directly
   │
   └── Yes
         │
         ▼
   search_jobs()
         │
         ▼
    JSearch API
         │
         ▼
   Job Listings
         │
         ▼
Final Response
```

***

## Step 1. Import Libraries

```python
import os
import requests

from dotenv import load_dotenv

from langchain.agents import create_agent
from langchain.tools import tool
from langchain_core.messages import HumanMessage
from langchain_nvidia_ai_endpoints import ChatNVIDIA
```

These libraries help load environment variables, make API calls, create tools, interact with the LLM, and build the AI Agent.

***

## Step 2. Load Environment Variables

```python
load_dotenv()
```

This loads all variables from the `.env` file into the current Python session.

***

## Step 3. Read the API Key

```python
JSEARCH_API_KEY = os.getenv("JSEARCH_API_KEY")
```

Reading the API key from the environment is safer than hardcoding it.

***

## Step 4. Create a Tool

```python
@tool
def search_jobs(query: str):
    """
    Search for job postings based on the user's query.
    """
```

The `@tool` decorator tells LangChain that the AI Agent can call this function when it needs live job information.

⚠️ **Important:** You must write a **docstring inside the function** (like `"""Search for job postings..."""` above). LangChain uses this docstring as the tool description and tells the LLM what the tool does. The `@tool` decorator returns an error if the docstring is missing.

***

## Step 5. Call the JSearch API

```python
response = requests.get(
    "https://api.openwebninja.com/jsearch/search-v2",
    headers={"X-API-Key": JSEARCH_API_KEY},
    params={
        "query": query,
        "country": "in",
        "date_posted": "today"
    }
)
```

Here, we send a GET request to the JSearch API.

| Parameter    | Purpose              |
| ------------ | -------------------- |
| query        | Job title or keyword |
| country      | Search only in India |
| date\_posted | Return today's jobs  |

***

## Step 6. Validate & Return the Response

```python
response.raise_for_status()

return response.json()
```

`raise_for_status()` — stops execution if the API request fails.

`response.json()` — converts the API response into a Python dictionary.

***

## Testing the Tool Individually

Before creating the agent, it is best practice to test the tool independently:

```python
print(search_jobs.invoke({"query": "Python Developer"}))
```

This confirms the API key is correct and the tool works independently. It makes debugging easier before the agent is fully configured.

***

## Step 7. Create the LLM

```python
llm = ChatNVIDIA(
    model="meta/llama-3.1-8b-instruct"
)
```

The LLM understands the user's request, decides when to use the tool, and generates the final response.

***

## Step 8. Register the Tool

```python
tools = [search_jobs]
```

This makes the `search_jobs()` function available to the AI Agent.

***

## Step 9. Create the AI Agent

```python
agent = create_agent(
    model=llm,
    tools=tools
)
```

This connects the LLM with the available tools, creating an AI Agent.

***

## Step 10. Send the User Query

```python
result = agent.invoke(
    {
        "messages": [
            HumanMessage(
                content="""
Find Data Analyst jobs in India.

For each job provide:

- Job Title
- Company Name
- Location
- Job Type
- Posted Date
- Apply Link
"""
            )
        ]
    }
)
```

The agent understands the request, calls the tool when needed, and retrieves live job listings.

***

## Step 11. Print the Response

```python
print(result["messages"][-1].content)
```

This prints the AI Agent's final generated answer.

***

## Complete Execution Flow

```
User Prompt
      │
      ▼
LangChain Agent
      │
      ▼
Reasoning
      │
      ▼
Need Live Data?
      │
      ├── No
      │      ▼
      │ Final Response
      │
      └── Yes
             ▼
      search_jobs()
             ▼
        JSearch API
             ▼
        JSON Response
             ▼
      LangChain Agent
             ▼
      Final Response
```

***

## Expected Output

```
Job Title: Data Analyst

Company: ABC Technologies

Location: Bangalore

Job Type: Full-Time

Posted: Today

Apply Link:
https://example.com/job
```

***

## Best Practices

* Store secrets in a `.env` file.
* Never upload API keys to GitHub.
* Keep each tool focused on one task.
* Validate API responses before processing.
* Write clear prompts for better results.
* Write a docstring in every tool — LangChain uses it as the description.

***

## Common Errors

| Error                 | Solution                              |
| --------------------- | ------------------------------------- |
| 401 Unauthorized      | Check your API key                    |
| 429 Too Many Requests | Wait and retry                        |
| Empty Results         | Verify query and country              |
| API Key is None       | Ensure `.env` is loaded               |
| Tool not working      | Missing docstring in `@tool` function |

***

## Key Takeaways

* AI Agents extend LLMs with tools.
* Tools allow agents to access live data.
* LangChain automatically decides when to call a tool.
* Environment variables keep API keys secure.
* External APIs make AI applications far more useful.
* A docstring is mandatory with the `@tool` decorator.

***

## What's Next?

Our agent currently returns plain text.

In the next project, we'll use Pydantic to generate structured JSON responses and build a Streamlit interface so users can interact with the AI Agent through a web application.

***

**The full code will be shared on the next page - you can copy, paste, and run it directly.**
