# 🧪 AI Perfume Consultant (Agentic RAG System)

![n8n](https://img.shields.io/badge/n8n-Workflow-ff6d5a?style=for-the-badge&logo=n8n)
![OpenAI](https://img.shields.io/badge/LLM-GPT--4o--mini-412991?style=for-the-badge&logo=openai)
![Google Sheets](https://img.shields.io/badge/Database-Google%20Sheets-34A853?style=for-the-badge&logo=google-sheets)

## 🛍️ Overview

This project is an **AI-powered Sales Assistant** designed for perfume shops and e-commerce websites. Unlike complex RAG systems that require vector databases, this solution uses **n8n** and **Google Sheets** to create a lightweight, highly accurate recommendation engine.

It acts as a knowledgeable shopkeeper that understands customer preferences (scent, price range, gender) and suggests products **strictly from the available inventory**.

## 💡 Why this approach?

For small to medium businesses, fine-tuning an LLM is expensive and maintaining a vector database is complex.
* **Cost-Effective:** No GPU or heavy infrastructure required.
* **Easy Maintenance:** The shop owner simply updates the Google Sheet (price/stock), and the AI updates instantly.
* **Zero Hallucinations:** The AI is strictly prompted to **only** recommend products that exist in the database.

## ✨ Key Features

* **Intelligent Search:** Connects OpenAI directly to a Google Sheet inventory.
* **Smart Currency Handling:** Automatically converts user input (e.g., "15 million Tomans") to the database format (Rials).
* **Gender Logic:** Implements smart filtering (e.g., if a user asks for "Men's perfume," it searches for both "Male" and "Unisex" categories).
* **Conversational Memory:** Remembers context (e.g., user can say "Show me cheaper ones" after the first result).

## 🛠️ Workflow Architecture

The system uses an **AI Agent** pattern within n8n:

1.  **Chat Trigger:** Receives the user's message.
2.  **AI Agent (The Brain):** Analyzes the request using a custom System Prompt.
3.  **Google Sheets Tool:** The Agent "calls" this tool to fetch real-time data from the inventory.
4.  **Response Generation:** The Agent filters the data and formulates a friendly, human-like recommendation.

## 🧠 System Prompt & Logic

The core power of this project lies in the **Prompt Engineering**. The model is instructed to follow strict business logic:

text
You are a smart perfume sales assistant.
RULES:
1. ONLY recommend items found in the Google Sheet.
2. Currency: Convert "Tomans/Millions" from user to "Rials" for search.
   (e.g., User: "10 Million" -> Agent searches: "100,000,000 Rials")
3. Gender: 
   - User asks for "Men's" -> Search "Male" + "Unisex"
   - User asks for "Women's" -> Search "Female" + "Unisex"


## 📦 How to Use

### Prerequisites
* **n8n** installed (Self-hosted or Cloud).
* **OpenAI API Key**.
* **Google Cloud Console** setup (Service Account with access to Sheets).

### Installation

1.  **Import Workflow:** Download the `workflow.json` file from this repository and import it into n8n.
2.  **Setup Google Sheet:**
    * Create a new Google Sheet.
    * Add columns: `Name`, `Price` (in Rials), `Gender`, `Smell_Profile`, `Stock`.
    * **Crucial:** Share the sheet with your Google Service Account email (Client Email).
3.  **Configure Credentials:**
    * In n8n, add your **OpenAI API Key**.
    * Add your **Google Service Account** credentials.
4.  **Update Node:** Open the "Get row perfume data" node and select your specific Sheet ID / Name.

## 👨‍💻 Author

**Bardia Azvanian**
*Solo AI Builder & Automation Engineer*
