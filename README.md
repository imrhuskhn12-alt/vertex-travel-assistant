# Gemini Travel Chat Lab ✈️

A multi‑turn AI travel assistant built with Google’s Gemini model on Vertex AI and Streamlit. It remembers your conversation, calls tools when needed, and helps you plan trips using live data like weather and local info. [web:84][web:53]

---

## 🌍 Overview

This project turns a basic, one‑shot model call into a **tool‑enabled, multi‑turn chat experience**. Instead of treating each prompt in isolation, the app maintains a chat session, lets Gemini decide when to call external tools (like web search or weather), and then uses those results to give more useful travel suggestions. [web:84][web:82]

You can use it as:
- A travel brainstorming buddy (where should I go, what can I do there?).  
- An itinerary helper that refines plans over several messages.  
- A reference pattern for building production‑style LLM apps with Vertex AI.

---

## ✨ Features

- **Multi‑turn chat with memory**  
  Uses a persistent Vertex AI `ChatSession` so the assistant can remember previous questions, preferences, and constraints across turns. [web:84]

- **Function‑calling tools**  
  The model can ask to call Python functions (for example, `search_web`, `get_weather`), receive structured results, and incorporate them into its reply. This pattern is the core of “LLM + tools” apps. [web:82][web:53]

- **Travel‑focused assistant**  
  Prompts and tools are oriented toward trip planning: destinations, weather, things to do, and refining an itinerary gradually instead of all at once. [web:67][web:53]

- **Streamlit UI**  
  A lightweight web interface that lets you chat with the model, see responses, and iterate quickly without building a full frontend from scratch. [web:78]

---

## 🧠 How it works

At the heart of the app are two pieces of logic:

- `get_chat(model_name)`  
  - Sets up a **Gemini chat session** with system instructions and tool definitions.  
  - Stores the session in `st.session_state` so it persists across Streamlit reruns.  
  - This is where the app stopped being “single request/response” and became a proper multi‑turn conversation engine. [web:84][web:81]

- `call_model(prompt, model_name)`  
  - Sends the user’s message to Gemini through the chat session.  
  - Checks the response for `function_call` parts; if any are present, it dispatches to the matching Python tool with the provided arguments.  
  - Sends the tool output back into the chat so Gemini can use real‑world data (like travel info or weather) in its next message.  
  - Repeats this loop until the model stops requesting tools and returns a final answer. [web:82]

This design mirrors how many modern AI apps integrate LLMs with APIs and databases: the model is not just answering text, it is orchestrating calls to tools and then reasoning over the results. [web:84]

---

## 🧩 Tech stack

- Python 3  
- Streamlit (UI and session management) [web:78]  
- Google Cloud Vertex AI – Gemini models (chat + function calling) [web:84]  
- `google-cloud-aiplatform` / `vertexai` SDKs to talk to Gemini from Python [web:84]

---

## 🚀 Getting started

1. **Clone the repository**

   ```bash
   git clone https://github.com/<your-username>/<your-repo-name>.git
   cd <your-repo-name>
