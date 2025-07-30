# Autonomous Release Notes Intelligence System

This project deploys an autonomous multi-agent system designed to streamline the entire process of tracking and understanding software release notes. It operates in two distinct modes: a proactive newsletter dispatcher that keeps your team updated, and a reactive Q&A email bot that provides intelligent, on-demand answers about specific updates.

The system leverages AI agents built with crewAI, a sophisticated Retrieval-Augmented Generation (RAG) pipeline for Q&A, and a robust data collection engine using Selenium and various APIs.

---

### System Architecture & User Flow

QnA User Flow Diagram

![User Flow Diagram](https://github.com/Bayhaqieee/ReleaseNotes_GenAI/blob/main/User.jpg)

QnASystem Flow Diagram

![System Flow Diagram](https://github.com/Bayhaqieee/ReleaseNotes_GenAI/blob/main/System.jpg)

Full System & User Documentation

You can check
bash
System-User_Flow.pdf

---

### Key Features

This solution is composed of two primary, independent workflows:

* Proactive Weekly Newsletter:
    * Autonomous Data Collection: Automatically scrapes release notes from multiple sources (websites, GitHub Releases) on a schedule.
    * Intelligent Summarization: AI agents analyze and summarize the raw text, extracting the most critical updates.
    * Product-Specific Emails: Generates and dispatches separate, personalized HTML newsletters for each product (e.g., Langflow, SimpliDots, Anthropic).
    * Managed Mailing List: Reads recipient information from a simple recipients.csv file for easy management.

* Reactive Q&A Email Bot:
    * Email-Based Interface: Users can ask questions by sending an email to a dedicated inbox with a specific subject line.
    * RAG-Powered Answers: The system uses a Retrieval-Augmented Generation (RAG) pipeline with a FAISS vector store to find the most relevant information from the entire knowledge base of release notes.
    * Formatted HTML Replies: The AI generates a detailed, well-structured HTML email in response, directly answering the user's question.
    * Automated Inbox Management: The bot automatically reads new questions and marks them as read after replying.

---

### Technologies Used

#### Core Frameworks & Libraries
* Python: The core programming language for the entire system.
* CrewAI: A framework for orchestrating autonomous multi-agent systems to perform complex, chained tasks (used for the newsletter generation).
* LangChain: The framework used to build the powerful Retrieval-Augmented Generation (RAG) chain for the Q&A bot.
* Selenium: Used for robust, browser-based web scraping of dynamic JavaScript-heavy websites.
* BeautifulSoup4: Used for parsing HTML content during the scraping process.

#### Data & Infrastructure
* Azure OpenAI: Provides the powerful LLMs (GPT series) used for the analysis, summarization, and Q&A generation tasks.
* FAISS (Facebook AI Similarity Search): A library for efficient similarity search, used to create the vector store for our RAG knowledge base.
* Google API (Gmail): Used by the Q&A bot to read incoming questions from a Gmail inbox and send replies.
* Google Colab: The development and execution environment for the notebook.
* Pandas & NumPy: Used for data manipulation and handling.

---

### Setup and Usage

To run this project, you will need access to Azure OpenAI and a dedicated Google account for the Q&A bot.

1. Prerequisites
* A Google Cloud Project with the Gmail API enabled.
* An Azure account with access to the OpenAI service.
* A dedicated Gmail account that the Q&A bot will use to receive questions and send replies.

2. Clone the Repository
bash
git clone [https://github.com/Bayhaqieee/ReleaseNotes_GenAI](https://github.com/Bayhaqieee/ReleaseNotes_GenAI)
cd ReleaseNotes_GenAI


3. Install Dependencies
bash
pip install -r requirements.txt


4. Configure Environment Variables
Create a .env file in the root directory of the project by copying the example file. Then, fill in your secret credentials.
bash
cp .env.example .env

Now, edit the .env file with your credentials.

5. Configure Google Authentication
* Follow the official guide to create an OAuth 2.0 Client ID for a Desktop app.
* Download the JSON key file and rename it to credentials.json.
* Place this file in the location specified in the notebook (e.g., a specific folder in your Google Drive if running on Colab).

6. Running the System
Open the ReleaseNote_email.ipynb notebook in Google Colab or another Jupyter environment.

* To Run the Proactive Newsletter: Execute the cells sequentially up to and including the "Main Newsletter Execution Loop". This will scrape the latest data and send the weekly emails.
* To Run the Reactive Q&A Bot:
    1.  Execute the cells in the "Shared Data Pipeline" section to scrape data and build the vector store.
    2.  Execute the cells in the "Reactive Q&A Email Bot" section. The final cell will initialize the bot, which will check for new emails and send replies.

---

### Demo Video

More Details on this Demo!
[Link to Demo Video]

---

### Important Notes for Reviewers

* API Key Dependency: This system is heavily dependent on external APIs (Azure OpenAI, Google API). It will not run without the necessary credentials configured in the .env file and the credentials.json file.
* Two Distinct Workflows: The notebook contains two powerful workflows. Be sure to test both the proactive newsletter generation and the reactive Q&A bot by sending an email to the configured inbox.
* Agentic System: The proactive newsletter is not a simple script; it is an example of a multi-agent system where different AI agents with specific roles (Analyst, Writer, Dispatcher) collaborate to achieve a goal.
* First-Time Google Auth: The first time you run the Q&A bot, you will be prompted to go through a one-time Google authentication flow in your browser to grant the script permission.
