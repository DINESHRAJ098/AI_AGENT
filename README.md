# AI_AGENT
This repository contains the completed project from Day 1 of the Kaggle 5-Day AI Agents Intensive Course. The project involves building, running, and interacting with a simple AI agent using Google's Agent Development Kit (ADK) and the Gemini model.

📖 Project Overview
This project serves as a "Hello, World!" for AI agents. The agent is a helpful_assistant powered by the gemini-2.5-flash-lite model. It's given instructions to be helpful and a "tool" (Google Search) that allows it to access real-time information from the internet to answer questions.

>The project demonstrates two primary ways to run the agent:
1.Directly in a notebook: Using the InMemoryRunner to get quick, debug-style responses.
2.Via a web interface: Using the adk web command to spin up a local chat UI for interactive testing.

✨ Features
>LLM-Powered: Uses Google's gemini-2.5-flash-lite model for reasoning and instruction following.
>Tool-Equipped: The agent can use Google Search to find current information it doesn't know, such as weather, news, or recent events.
>Interactive Chat: A web-based UI (via adk web) allows for continuous, stateful conversations with the agent.

🛠️ Technologies Used
>Google Agent Development Kit (ADK): The open-source framework for building and orchestrating agents.
>Google Gemini: The family of generative AI models powering the agent's "brain."
>Python: The programming language used for the ADK and the notebook.
>Kaggle Notebooks: The environment used for the original course lab.
