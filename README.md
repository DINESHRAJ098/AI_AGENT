# AI_AGENT
This repository contains the completed project from Day 1 of the Kaggle 5-Day AI Agents Intensive Course. The project involves building, running, and interacting with a simple AI agent using Google's Agent Development Kit (ADK) and the Gemini model.

Run these cells in order, one at a time.

1. Cell 1.2: Configure your Gemini API Key This cell reads the secret you just created and makes it available to your notebook's environment.

Python

import os
from kaggle_secrets import UserSecretsClient

try:
    GOOGLE_API_KEY = UserSecretsClient().get_secret("GOOGLE_API_KEY")
    os.environ["GOOGLE_API_KEY"] = GOOGLE_API_KEY
    print("✅ Gemini API key setup complete.")
except Exception as e:
    print(
        f"🔑 Authentication Error: Please make sure you have added 'GOOGLE_API_KEY' to your Kaggle secrets. Details: {e}"
    )
2. Cell 1.3: Import ADK components This cell imports the necessary libraries from the Agent Development Kit (ADK) and Google's AI library.

Python

from google.adk.agents import Agent
from google.adk.models.google_llm import Gemini
from google.adk.runners import InMemoryRunner
from google.adk.tools import google_search
from google.genai import types

print("✅ ADK components imported successfully.")
3. Cell 1.4: Helper functions This defines helper functions specifically for the Kaggle environment. You don't need to change anything, just run the cell.

Python

# Define helper functions that will be reused throughout the notebook
from IPython.core.display import display, HTML
from jupyter_server.serverapp import list_running_servers

# Gets the proxied URL in the Kaggle Notebooks environment
def get_adk_proxy_url():
    PROXY_HOST = "https://kkb-production.jupyter-proxy.kaggle.net"
    ADK_PORT = "8000"

    servers = list(list_running_servers())
    if not servers:
        raise Exception("No running Jupyter servers found.")

    baseURL = servers[0]["base_url"]

    try:
        path_parts = baseURL.split("/")
        kernel = path_parts[2]
        token = path_parts[3]
    except IndexError:
        raise Exception(f"Could not parse kernel/token from base URL: {baseURL}")

    url_prefix = f"/k/{kernel}/{token}/proxy/proxy/{ADK_PORT}"
    url = f"{PROXY_HOST}{url_prefix}"

    styled_html = f"""
    <div style="padding: 15px; border: 2px solid #f0ad4e; border-radius: 8px; background-color: #fef9f0; margin: 20px 0;">
        <div style="font-family: sans-serif; margin-bottom: 12px; color: #333; font-size: 1.1em;">
            <strong>⚠️ IMPORTANT: Action Required</strong>
        </div>
        <div style="font-family: sans-serif; margin-bottom: 15px; color: #333; line-height: 1.5;">
            The ADK web UI is <strong>not running yet</strong>. You must start it in the next cell.
            <ol style="margin-top: 10px; padding-left: 20px;">
                <li style="margin-bottom: 5px;"><strong>Run the next cell</strong> (the one with <code>!adk web ...</code>) to start the ADK web UI.</li>
                <li style="margin-bottom: 5px;">Wait for that cell to show it is "Running" (it will not "complete").</li>
                <li>Once it's running, <strong>return to this button</strong> and click it to open the UI.</li>
            </ol>
            <em style="font-size: 0.9em; color: #555;">(If you click the button before running the next cell, you will get a 500 error.)</em>
        </div>
        <a href='{url}' target='_blank' style="
            display: inline-block; background-color: #1a73e8; color: white; padding: 10px 20px;
            text-decoration: none; border-radius: 25px; font-family: sans-serif; font-weight: 500;
            box-shadow: 0 2px 5px rgba(0,0,0,0.2); transition: all 0.2s ease;">
            Open ADK Web UI (after running cell below) ↗
        </a>
    </div>
    """

    display(HTML(styled_html))

    return url_prefix

print("✅ Helper functions defined.")
4. Cell 1.5: Configure Retry Options This cell sets up automatic retries for the API, which is good practice for handling temporary network errors.

Python

retry_config=types.HttpRetryOptions(
    attempts=5,  # Maximum retry attempts
    exp_base=7,  # Delay multiplier
    initial_delay=1, # Initial delay before first retry (in seconds)
    http_status_codes=[429, 500, 503, 504] # Retry on these HTTP errors
)
🤖 Section 2: Your first AI Agent with ADK
1. Cell 2.2: Define your agent This is where you create your agent. You give it a model (gemini-2.5-flash-lite), instructions, and the Google Search tool.

Python

root_agent = Agent(
    name="helpful_assistant",
    model=Gemini(
        model="gemini-2.5-flash-lite",
        retry_options=retry_config
    ),
    description="A simple agent that can answer general questions.",
    instruction="You are a helpful assistant. Use Google Search for current info or if unsure.",
    tools=[google_search],
)

print("✅ Root Agent defined.")
2. Cell 2.3.a: Create the Runner The InMemoryRunner is what manages the conversation with your agent.

Python

runner = InMemoryRunner(agent=root_agent)

print("✅ Runner created.")
3. Cell 2.3.b: Run your agent This is your first agent run! The await keyword is used to run the agent asynchronously. It will ask the question and the agent will use Google Search to find the answer.

Python

response = await runner.run_debug(
    "What is Agent Development K-it from Google? What languages is the SDK available in?")
4. Cell 2.5: Your Turn! This is the second test run. You can change the question inside the quotes to anything you like.

Python

response = await runner.run_debug("What's the weather in London?")
💻 Section 3: Try the ADK Web Interface
This is the final section and the part that requires careful steps.

1. Cell 3.1: Create the agent files This command (starting with !) is run in the terminal. It creates a new folder named sample-agent with the Python files needed for the web UI.

Bash

!adk create sample-agent --model gemini-2.5-flash-lite --api_key $GOOGLE_API_KEY
2. Cell 3.2: Get the custom URL Run this cell. It will use the helper function from earlier to display a large button/link. Do NOT click the button yet!

Python

url_prefix = get_adk_proxy_url()
3. Cell 3.3: Run the ADK Web Server This is the final step. The "Aborted!" message you saw means the server was stopped. To run it successfully:

Run the cell below.

This cell will not "complete" with a green checkmark. It is supposed to keep running. It will show logs that look like INFO: Started server process...

Do not stop or interrupt this cell.

While this final cell is running, scroll back up to the output of Cell 3.2 (the one right above it).

Now, click the "Open ADK Web UI" button that appeared. It will open the chat interface in a new browser tab.

Bash

!adk web --url_prefix {url_prefix}
If you follow these steps in order, you will have a running web server (in Cell 3.3) and a new tab open with the ADK Web UI, allowing you to chat with your agent.
