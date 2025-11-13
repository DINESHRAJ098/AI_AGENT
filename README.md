# AI_AGENT
This repository contains the completed project from Day 1 of the Kaggle 5-Day AI Agents Intensive Course. The project involves building, running, and interacting with a simple AI agent using Google's Agent Development Kit (ADK) and the Gemini model.

⚙️ Setup and Installation
To run this project on your local machine, follow these steps:
1.Clone the Repository:

git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME.git
cd YOUR_REPOSITORY_NAME

2.Install Dependencies: This project primarily relies on the google-adk library.

pip install google-adk
Get Your API Key: You need a Gemini API key to run this project.

Get your key from Google AI Studio.

Set Up Your API Key: The safest way to handle your API key is with an environment file.

Create a file named .env in the root of the project.

Add the following line to it:

GOOGLE_API_KEY="YOUR_API_KEY_HERE"
(Important) Add .env to your .gitignore file to avoid accidentally committing your key to GitHub.

🚀 How to Run
This project can be run in two main ways:

1. In the Notebook (Your First AI Agent.ipynb)
If you have the .ipynb file, you can run the agent directly inside a Jupyter-compatible notebook.

Ensure your GOOGLE_API_KEY is set as an environment variable (or use a method like python-dotenv to load your .env file).

Run the cells in order to define the agent, create the InMemoryRunner, and call the runner.run_debug() method.

Python

# Example from the notebook
response = await runner.run_debug("What's the weather in London?")
2. Via the ADK Web UI
The ADK includes a command-line tool to serve your agent in a simple web interface. This project is configured to run the sample-agent created in the notebook.

Ensure the sample-agent folder exists. If not, you can create it with the ADK CLI (make sure your API key is set as an environment variable first!):

# This command uses the .env file we created
adk create sample-agent --model gemini-2.5-flash-lite --api_key $GOOGLE_API_KEY
Run the web server:

adk web

Open the UI: Open your browser and navigate to http://127.0.0.1:8000 to start chatting with your agent.
