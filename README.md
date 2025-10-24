# Friday AI Assistant

[![Ask DeepWiki](https://devin.ai/assets/askdeepwiki.png)](https://deepwiki.com/GarvGangwani/Friday-AI-Assistant-Livekit-Agent)

This repository contains the source code for "Friday," a voice-based AI assistant built using the [LiveKit Agents](https://docs.livekit.io/agents/) framework. Inspired by the AI from the *Iron Man* movies, Friday acts as a classy yet sarcastic personal assistant capable of performing various tasks through natural conversation.

## Features

*   **Real-time Voice Interaction**: Engage in spoken conversations with the assistant, powered by LiveKit's real-time infrastructure.
*   **Distinct Persona**: Friday is configured to respond like a classy, sarcastic butler, providing a unique user experience.
*   **Extensible Tools**: The assistant can perform actions using a set of integrated tools:
    *   **Get Weather**: Fetches the current weather for any city.
    *   **Search Web**: Uses DuckDuckGo to search the web for information.
    *   **Send Email**: Composes and sends emails through your Gmail account.

## Setup and Installation

Follow these steps to get your own instance of Friday running.

### 1. Prerequisites

*   Python 3.9+
*   A LiveKit server instance. You can get one from [LiveKit Cloud](https://cloud.livekit.io/) or self-host.
*   A Google API Key for the LLM.
*   A Gmail account with an [App Password](https://support.google.com/accounts/answer/185833) for sending emails.

### 2. Clone the Repository

```bash
git clone https://github.com/GarvGangwani/Friday-AI-Assistant-Livekit-Agent.git
cd Friday-AI-Assistant-Livekit-Agent
```

### 3. Install Dependencies

Install the required Python packages using `pip`.

```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables

Create a `.env` file in the root of the project directory by copying the `env.txt` template.

```bash
cp env.txt .env
```

Now, open the `.env` file and fill in the following values:

*   `LIVEKIT_URL`: Your LiveKit server URL (e.g., `wss://your-project.livekit.cloud`).
*   `LIVEKIT_API_KEY`: Your LiveKit project API key.
*   `LIVEKIT_API_SECRET`: Your LiveKit project API secret.
*   `GOOGLE_API_KEY`: Your Google API key.
*   `GMAIL_USER`: The Gmail address you want to send emails from.
*   `GMAIL_APP_PASSWORD`: The 16-character App Password you generated for your Gmail account. **Do not use your regular account password.**

## Running the Agent

With the setup complete, you can start the agent with the following command:

```bash
python agent.py
```

The agent will connect to your LiveKit server and be ready to join a room and assist users. When a user joins the room, the agent will introduce itself and await commands.

## How It Works

*   **`agent.py`**: This is the main entry point. It defines the `Assistant` class, which configures the agent with its instructions, LLM (Google's `RealtimeModel`), and tools. It also handles the LiveKit session management.
*   **`prompts.py`**: This file contains the core personality and instructions for the AI. The `AGENT_INSTRUCTION` prompt defines the "Friday" persona, while `SESSION_INSTRUCTION` provides the initial task and greeting.
*   **`tools.py`**: This file implements the functions the agent can execute. Each tool is decorated with `@function_tool` from the LiveKit Agents SDK, allowing the LLM to call them based on user requests.
*   **`requirements.txt`**: Lists all the necessary Python packages for the project.