# Build a Real AI Job Search Agent with LangChain

***

### Watch the Video

If you prefer learning by watching the complete implementation first, you can watch the full tutorial here.

**YouTube:**<br>

***

## Overview

In the previous episodes, we understood what AI Agents are and how they differ from traditional chatbots.

Now it's time to build one.

In this project, we'll create a real AI Job Search Agent using **LangChain**, **NVIDIA LLM**, and the **JSearch API**. Instead of answering only from its own knowledge, our agent will fetch live job listings from the internet and present them in a readable format.

This project introduces one of the most important concepts in Agentic AI—**Tool Calling**. You'll also learn how an LLM decides when to use a tool and how external APIs make AI applications much more useful.

***

## What You'll Build

By the end of this project, you'll have a working AI Agent that can:

* Search live job openings
* Understand natural language queries
* Call an external API whenever required
* Return a clean response to the user

Although the application runs in the terminal for now, we'll convert it into a proper web application in the upcoming episodes.

***

## Technologies Used

| Technology    | Why We're Using It                |
| ------------- | --------------------------------- |
| Python        | Main programming language         |
| LangChain     | To build the AI Agent             |
| NVIDIA API    | Provides the Large Language Model |
| JSearch API   | Retrieves live job listings       |
| Requests      | Sends HTTP requests to the API    |
| python-dotenv | Keeps API keys secure             |

***

## How the Project Works

Our AI Agent follows a simple workflow.

```
User

↓

AI Agent

↓

LLM understands the request

↓

Decides whether a Tool is required

↓

Calls search_jobs()

↓

JSearch API

↓

Returns live job data

↓

LLM prepares the final answer

↓

User
```

The important thing to notice here is that the LLM never talks directly to the internet.

Whenever it needs live information, it asks a **Tool** to do the job.

***

## Project Structure

```
AI_Job_Search_Agent/
│
├── main.py
├── .env
├── requirements.txt
└── README.md
```

Keeping the project structure simple makes it easier to understand each component before we start building larger AI applications.

***

## Installing the Required Libraries

Install all required packages before running the project.

```bash
pip install langchain
pip install langchain-nvidia-ai-endpoints
pip install python-dotenv
pip install requests
```

***

## Setting Up the API Key

Create a `.env` file in the project folder.

```env
JSEARCH_API_KEY=YOUR_API_KEY
```

Instead of writing secrets directly inside the code, we store them in environment variables.

This is considered a standard practice in software development because it keeps sensitive information secure and prevents accidental exposure on GitHub.

***

## Loading Environment Variables

```python
load_dotenv()
```

This line reads the `.env` file and loads all environment variables into the current Python session.

Once loaded, we can access them using the `os` module.

***

## Reading the API Key

```python
JSEARCH_API_KEY = os.getenv("JSEARCH_API_KEY")
```

Rather than hardcoding the API key, we retrieve it from the environment.

If the key changes in the future, we only need to update the `.env` file instead of modifying the source code.

***

## Creating a Tool

```python
@tool
def search_jobs(query: str):
```

The `@tool` decorator tells LangChain that this function is available for the AI Agent.

Whenever the model realizes it needs live job information, it can call this function automatically.

Think of a Tool as a special ability that extends what an LLM can do.

Without tools, an LLM can only answer from its existing knowledge.

With tools, it can interact with external systems such as APIs, databases, search engines, or files.

***

## Calling the JSearch API

Inside our tool, we send an HTTP GET request.

The request contains three important parts:

* API URL
* Headers
* Query Parameters

Example:

```python
params = {
    "query": query,
    "country": "in",
    "date_posted": "today"
}
```

These parameters tell the API exactly what we want.

For example:

* `query` → Job title or keyword.
* `country` → Search jobs only in India.
* `date_posted` → Return only recently posted jobs.

The `requests` library automatically converts these parameters into URL query parameters before sending the request.

***

## Understanding the API Response

The JSearch API returns data in JSON format.

We convert that response into a Python dictionary.

```python
response.json()
```

Once converted, we can easily access individual fields such as:

* Job Title
* Company Name
* Location
* Employment Type
* Apply Link

This structured data is then returned to the AI Agent.

***

## Creating the LLM

```python
llm = ChatNVIDIA(
model= "meta/llama-3.1-8b-instruct"
)
```

The LLM is the brain of our AI Agent.

Its job is not to search for jobs.

Instead, it focuses on understanding the user's request, deciding whether a tool is needed, and generating the final response.

The actual job search is handled by the tool.

***

## Creating the AI Agent

```python
agent = create_agent(
    model=llm,
    tools=[search_jobs]
)
```

At this point, we connect the LLM with our custom tool.

Now the model knows that whenever it needs live job information, it has permission to use the `search_jobs()` function.

This is the step where our LLM becomes an AI Agent.

***

## Running the Agent

```python
result = agent.invoke(
    {
        "messages": [
            HumanMessage(content=""" Find Data Analyst jobs in India. For each job provide:

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



print(result["messages"][-1].content)
```

When the user sends a prompt, the agent performs several tasks automatically.

1. Reads the user's request.
2. Understands what the user is asking.
3. Decides whether a tool is required.
4. Calls the tool if necessary.
5. Receives live data from the API.
6. Generates a final response for the user.

Although this entire process looks like a single function call, multiple reasoning steps happen behind the scenes.

***

## Complete Execution Flow

```
User Prompt

↓

AI Agent

↓

Reasoning

↓

Tool Selection

↓

JSearch API

↓

JSON Response

↓

LLM

↓

Final Answer
```

This is the complete lifecycle of our AI Agent.

Understanding this flow is much more important than memorizing the code.

***

## Key Takeaways

After completing this project, you should be comfortable with the following concepts:

* What an AI Agent actually is.
* How Tool Calling works.
* Why LLMs need external tools.
* How to connect an AI Agent with a REST API.
* Why environment variables are important.
* How LangChain simplifies Agent development.

These concepts form the foundation for almost every modern Agentic AI application.

***

## Best Practices

* Keep API keys inside a `.env` file.
* Never upload secrets to GitHub.
* Keep each tool focused on a single task.
* Handle API errors before processing responses.
* Write clear prompts so the agent can reason effectively.

***

## Common Mistakes

Many beginners run into the same issues while building their first AI Agent.

* Forgetting to load environment variables.
* Using an invalid API key.
* Hardcoding secrets inside the code.
* Passing incorrect query parameters.
* Assuming every API request succeeds.

If you encounter any of these problems, check the API response before debugging the rest of the code.

***

## What's Next?

At the moment, our AI Agent returns a plain-text response.

That works fine for learning, but real applications usually require structured data that can be displayed inside a UI or stored in a database.

In the next project, we'll improve this agent by generating **structured JSON outputs using Pydantic Models**. We'll then use those structured responses to build a clean **Streamlit web application**, allowing users to interact with the AI Agent through a browser instead of the terminal.

***

### Final Thoughts

**Congratulations!**&#x20;

You've built your real AI Agent that can interact with an external API and retrieve live information.

More importantly, you've learned the core workflow that powers most modern AI Agents. As we move forward, we'll continue enhancing this project step by step until it evolves into a production-ready AI application.
