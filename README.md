# Voice-Enabled AI Telegram Assistant (n8n Workflow)

A production-ready, autonomous AI assistant built using **n8n workflow automation**. The bot accepts both voice notes and text messages via Telegram, processes audio transcriptions with high-speed inference, retains conversational context using external memory, and leverages web-scraping tools to answer real-time queries with live data.

---

## 🚀 Key Features

* **Multi-Modal Input:** Seamlessly handles text prompts and voice notes.
* **High-Speed Voice Transcription:** Uses Groq API (Whisper-large-v3) via a custom Python data-formatting pipeline for near-instant audio-to-text processing.
* **Advanced Orchestration:** Powered by an n8n `AI Agent` node utilizing Google Gemini as the core LLM.
* **Persistent Memory:** Integrated with MongoDB to maintain user session state and chat history.
* **Live Web Browsing:** Equipped with a custom HTTP Request tool pointing to ScraperAPI, enabling the agent to bypass anti-bot protections and fetch real-time data from the web.

---

## 🛠️ System Architecture & Workflow Logic

![n8n Workflow Blueprint](./workflow-screenshot.png) *(Replace this with a screenshot of your n8n canvas)*

The workflow executes the following pipeline upon receiving a message:

1.  **Trigger (`Telegram Trigger`):** Listens for incoming `message` updates from the bot.
2.  **Conditional Routing (`If` Node):** Checks whether the message contains a voice note or plain text.
    * **Text Path:** Routes directly to the AI Agent.
    * **Voice Path:** Hits the Telegram API via `Get a file` to fetch the audio binary, processes the file payload through a custom `Python Code` block, and sends a `POST` request to the **Groq Audio Transcription API**.
3.  **Intellect & Tools (`AI Agent`):** * Uses **Google Gemini Chat Model** for reasoning and decision-making.
    * Queries **MongoDB Chat Memory** to recall past interactions.
    * Dynamically calls the **ScraperAPI HTTP Tool** if the prompt requires up-to-date internet data.
4.  **Response (`Send a text message`):** Dispatches the final AI-generated response back to the user on Telegram.

---

## 📋 Prerequisites & Environment Variables

To replicate this workflow, you will need active accounts and API credentials for the following services:

| Provider | Purpose | Required Credential/Env |
| :--- | :--- | :--- |
| **Telegram** | Bot Interface | `Bot Token` (via BotFather) |
| **Google AI** | Core LLM (Gemini) | `Gemini API Key` |
| **Groq** | Whisper Audio Transcription | `Groq API Key` |
| **ScraperAPI** | Live Web Scraping | `ScraperAPI Key` |
| **MongoDB** | Persistent Chat History | `MongoDB Connection URI` |

---

## 🚀 Setup & Installation

1.  **Clone this repository:**
    ```bash
    git clone [https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git](https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git)
    cd YOUR_REPO_NAME
    ```

2.  **Import the Workflow:**
    * Open your n8n instance.
    * Click the top-right menu icon (`...`) and select **Import from File**.
    * Choose the `workflow.json` file included in this repository.

3.  **Configure Credentials:**
    * Open each node with a red alert badge (Telegram, Gemini, Groq, MongoDB).
    * Add your specific API keys or connection strings into the respective n8n credential fields.
    * Save and toggle the workflow to **Active**.

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).
