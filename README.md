# AI-Agents-Course-by-HuggingFace
 # Foundations of AI Agents — Key Takeaways
This project is based on knowledge gained from the Foundations of Agents Course by Hugging Face, which offers a detailed and structured approach to understanding and building AI agents.

📌 Key Concepts Covered:
smol-ai/smolagents Library
Utilizes the ```smol-ai/smolagents``` library, which is built on the ReAct framework — a method that connects Reasoning ("Think") with Acting ("Act") for effective agent behavior.

Install the Library First
``` pip install smolagents huggingface_hub```

You should create your HF_TKON for the Following to set up.
``` python
from huggingface_hub import notebook_login
notebook_login()
```

Prompt Design
Focuses on writing prompts that guide agents to generate a plan rather than just a final answer.

```python
# This system prompt is a bit more complex and actually contains the function description already appended.
# Here we suppose that the textual description of the tools has already been appended
SYSTEM_PROMPT = """Answer the following questions as best you can. You have access to the following tools:

get_weather: Get the current weather in a given location

The way you use the tools is by specifying a json blob.
Specifically, this json should have a `action` key (with the name of the tool to use) and a `action_input` key (with the input to the tool going here).

The only values that should be in the "action" field are:
get_weather: Get the current weather in a given location, args: {"location": {"type": "string"}}
example use :
```
```
{{
  "action": "get_weather",
  "action_input": {"location": "New York"}
}}

ALWAYS use the following format:

Question: the input question you must answer
Thought: you should always think about one action to take. Only one action at a time in this format:
Action:
```
```
$JSON_BLOB
```
```
Observation: the result of the action. This Observation is unique, complete, and the source of truth.
... (this Thought/Action/Observation can repeat N times, you should take several steps when needed. The $JSON_BLOB must be formatted as markdown and only use a SINGLE action at a time.)

You must always end your output with the following format:

Thought: I now know the final answer
Final Answer: the final answer to the original input question

Now begin! Reminder to ALWAYS use the exact characters` `Final Answer:`` when you provide a definitive answer. """
Agent Core Components

Thought — internal reasoning about the problem.

Action — selecting and executing the next step.

Observation — receiving and interpreting feedback.

Types of Agents
Exploration of different agent types and their use cases.

Workflows for AI Agents

Prompt Chaining

Routing

Parallelization

Orchestration

Evaluation Techniques
Learn how to evaluate the generated text based on the input query to ensure reliable performance.

Frameworks for Building Agents

LangGraph (from LangChain)

Amazon Bedrock's AI Agent Framework

Rivet (Drag & Drop GUI for LLM workflow building)

Designing Agent Tools
Each tool should include:

A textual description of what the function does.

A callable implementation for the agent to execute.
