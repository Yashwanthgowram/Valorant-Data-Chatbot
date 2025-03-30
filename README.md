# 🎮 Valorant Player Insights Chatbot  
[🔗 View Demo](https://github.com/Yashwanthgowram/valorant-player-insight-chatbot/blob/main/demo.gif)

---

## 🧠 Overview

This chatbot is a **Streamlit-powered web app** designed to let users ask natural language questions about **Valorant players**. It uses **Amazon Athena** to query data from **AWS S3**, and leverages **Amazon Bedrock (Claude)** and **LangChain** to dynamically generate SQL and return results with simple, natural explanations — no SQL knowledge required.

---

## ⚙️ Core Components & Workflow

### 🖥️ Streamlit Interface & Session Handling

- **Streamlit Chat UI**: Offers a clean, interactive chat interface for non-technical users.
- **Session Management**: Stores conversation history in Streamlit's session state.
- **Reset Option**: Includes a “Clear Chat” button to reset the session quickly.

---

### ☁️ AWS Infrastructure

- **Amazon Athena**: Runs SQL queries on Valorant data stored in **Amazon S3**.
- **Amazon Bedrock**: Interfaces with Claude (LLM) to generate queries and interpret responses.
- **Amazon S3**: Stores structured game data in parquet/CSV formats.

Athena uses a **SQLAlchemy** connection and an **S3 staging directory** for intermediate query results.

---

### 🧠 LangChain & Query Generation

- Uses **LangChain** to orchestrate query generation and validation.
- Claude (via Bedrock) builds and interprets SQL using:
  - ✅ Predefined table schema (e.g., `player_details`, `leagues`, `tour_details`)
  - ✅ Controlled join logic for accuracy

---

### 🔎 Input Understanding & Query Flow

#### ✅ Smart Input Detection
The chatbot detects keywords like **“what”**, **“how”**, **“when”** to determine if a SQL query should be generated.

#### 🛠️ Data Fetch Pipeline

1. User submits question → **Streamlit**
2. Sent to **Amazon Bedrock**
3. Forwarded to **LangChain**
4. LangChain returns SQL template
5. Bedrock executes it via **Athena**
6. **Athena** fetches data from **S3**
7. Results returned to **Bedrock**
8. Response formatted in natural language
9. Final answer displayed via **Streamlit**

If the input is unrelated to data, the chatbot switches to **casual conversation mode**.

