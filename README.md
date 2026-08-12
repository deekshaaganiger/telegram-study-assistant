# 🤖 Telegram AI Study Notes Bot

An AI-powered Telegram study assistant built with **n8n**, **Google Gemini 2.5 Flash**, **Tavily**, **Google Docs**, **Google Drive**, and **Google Sheets**.

The bot allows a user to simply send a study topic through Telegram. The workflow uses an AI agent to generate comprehensive study material, optionally searches the web when additional information is required, remembers previous conversations, creates a formatted Google Doc, converts it into a PDF, logs the interaction, and sends the generated PDF back to the user through Telegram.

---

## 📌 Project Overview

The **Telegram AI Study Notes Bot** automates the process of creating study material from a simple Telegram message.

For example, a user can send:

```text
Binary Search Tree
```

The automation processes the topic and generates educational content covering concepts such as:

* Definition
* Why the topic matters
* Key concepts
* Working
* Examples
* Real-world applications
* Advantages
* Disadvantages
* Best practices
* Common mistakes
* Interview questions
* Multiple-choice questions
* Flashcards
* Quick revision notes
* Key takeaways
* Related topics
* Summary
* Flowchart
* Mind map

The completed study material is converted into a PDF and delivered directly to the user on Telegram.

---

## ✨ Features

### 📚 AI-Generated Study Notes

Generates structured educational content for any topic provided by the user.

### 🧠 AI Study Assistant

Uses **Google Gemini 2.5 Flash** through an n8n AI Agent to generate and organize the study material.

### 🔎 Intelligent Web Search

Uses **Tavily** as a web-search tool.

The AI agent can use Tavily when external or up-to-date information is required instead of performing a web search for every request.

### 💭 Conversation Memory

Uses n8n **Simple Memory** to maintain conversation context.

This allows the assistant to remember previous interactions within the user's conversation session.

### ❓ MCQ Generation

Generates multiple-choice questions with:

* Four options
* Correct answer
* Explanation

### 📝 Flashcards

Generates revision flashcards based on the requested topic.

### 🔄 Flowcharts

Generates Mermaid-based flowchart content to visually explain processes and concepts.

### 🧠 Mind Maps

Generates a Mermaid-based mind map at the end of the study material for quick revision.

### 📄 Automatic PDF Generation

The generated content is inserted into a Google Doc and exported as a PDF automatically.

### ☁️ Google Drive Integration

Generated documents/PDFs can be stored through Google Drive.

### 📊 Google Sheets Logging

Every interaction is logged into Google Sheets with information such as:

* Timestamp
* Telegram User ID
* Username
* Topic
* PDF link
* Status

### 📲 Telegram Delivery

The generated PDF is automatically sent back to the user through Telegram.

---

## 🔄 Workflow Architecture

```text
                    ┌─────────────────────┐
                    │   Telegram Trigger  │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │   Prepare Question  │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │   Study Notes Agent │
                    └──────┬──────┬───────┘
                           │      │
             ┌─────────────┘      └─────────────┐
             ▼                                  ▼
   ┌──────────────────┐               ┌─────────────────┐
   │ Gemini 2.5 Flash │               │ Simple Memory   │
   └──────────────────┘               └─────────────────┘
                           │
                           ▼
                    ┌─────────────────┐
                    │      Tavily     │
                    │   Web Search    │
                    └─────────────────┘
                           │
                           ▼
                    ┌─────────────────┐
                    │  Prepare Content│
                    └───────┬─────────┘
                            │
                ┌───────────┴───────────┐
                ▼                       ▼
      ┌──────────────────┐    ┌────────────────────┐
      │  Create Google   │    │ Log Interaction    │
      │      Doc         │    │   to Google Sheet  │
      └────────┬─────────┘    └────────────────────┘
               │
               ▼
      ┌──────────────────┐
      │ Insert Doc       │
      │ Content          │
      └────────┬─────────┘
               │
               ▼
      ┌──────────────────┐
      │ Export Doc       │
      │ as PDF           │
      └────────┬─────────┘
               │
               ▼
      ┌──────────────────┐
      │ Send PDF to      │
      │ Telegram         │
      └──────────────────┘
```

---

## 🧩 Workflow Nodes

| Node                         | Purpose                                         |
| ---------------------------- | ----------------------------------------------- |
| **Telegram Trigger**         | Receives the user's study topic                 |
| **Prepare Question**         | Prepares the Telegram input for the AI workflow |
| **Study Notes Agent**        | Main AI processing and content generation       |
| **Google Gemini Chat Model** | Provides Gemini 2.5 Flash as the LLM            |
| **Telegram Chat Memory**     | Maintains conversation context                  |
| **Tavily Web Search**        | Provides external information when required     |
| **Prepare Content**          | Processes the generated study material          |
| **Create Google Doc**        | Creates the document for the generated notes    |
| **Insert Doc Content**       | Inserts the generated content into Google Docs  |
| **Export Doc as PDF**        | Converts the Google Doc into a PDF              |
| **Log Interaction to Sheet** | Records the request in Google Sheets            |
| **Send PDF to Telegram**     | Sends the completed PDF to the user             |

---

## 🛠️ Technology Stack

### Automation

**n8n Cloud**

Used as the workflow automation platform and orchestration layer.

### Large Language Model

**Google Gemini 2.5 Flash**

Used for AI-powered study material generation.

### Web Search

**Tavily**

Used as an AI tool for retrieving external information when necessary.

### Messaging

**Telegram Bot API**

Used as the user interface for submitting topics and receiving generated PDFs.

### Memory

**n8n Simple Memory**

Used to maintain conversational context.

### Document Generation

**Google Docs**

Used to create and format the generated study material.

### PDF Generation

**Google Docs Export**

Used to convert the generated document into PDF format.

### Data Logging

**Google Sheets**

Used to maintain a record of user requests and generated documents.

### Storage

**Google Drive**

Used for storing generated documents/PDF files.

### Diagram Generation

**Mermaid**

Used for AI-generated flowcharts and mind maps.

---

## 🚀 How It Works

### 1. User Sends a Topic

The user sends a normal Telegram message.

Example:

```text
Binary Search Tree
```

No special command is required.

---

### 2. Telegram Trigger

The Telegram Trigger receives the incoming message and passes the topic into the workflow.

---

### 3. Question Preparation

The **Prepare Question** node extracts and prepares the user's request for the AI agent.

---

### 4. AI Study Agent

The **Study Notes Agent** processes the topic using:

* Gemini 2.5 Flash
* Conversation Memory
* Tavily Web Search

The AI determines when external web information is necessary.

---

### 5. Study Material Generation

The AI generates structured study material containing explanations, examples, applications, advantages, disadvantages, interview questions, MCQs, flashcards, revision content, flowcharts, and mind maps.

---

### 6. Content Preparation

The generated response is processed by the **Prepare Content** node so it can be inserted into the document.

---

### 7. Google Doc Creation

The workflow automatically creates a Google Doc.

---

### 8. Content Insertion

The generated study material is inserted into the newly created Google Doc.

---

### 9. PDF Generation

The completed Google Doc is exported as a PDF.

---

### 10. Interaction Logging

The request is recorded in Google Sheets.

The stored information includes:

```text
Timestamp
Telegram User ID
Username
Topic
PDF Link
Status
```

---

### 11. Telegram Response

The workflow sends the generated PDF back to the Telegram user.

The user receives their study material without manually downloading or converting anything.

---

## 💬 Example Interaction

### User

```text
Binary Search Tree
```

### Bot

```text
✅ Your study notes for "Binary Search Tree" are ready!
```

The bot then sends the generated PDF.

---

## 📖 Generated Study Material

The AI-generated document is structured around:

1. Definition
2. Why It Matters
3. Key Concepts
4. Working
5. Example
6. Real World Applications
7. Advantages
8. Disadvantages
9. Best Practices
10. Common Mistakes
11. Interview Questions
12. Multiple Choice Questions
13. Flashcards
14. Quick Revision Sheet
15. Key Takeaways
16. Related Topics
17. Summary
18. Flowchart
19. Mind Map

---

## 🔐 Credentials Required

To recreate this workflow, the following services/credentials are required:

* Telegram Bot credentials
* Google Gemini API credentials
* Tavily API credentials
* Google Docs / Google Drive access
* Google Sheets access

API keys and credentials should **never be committed to the GitHub repository**.

---

## 📥 Importing the Workflow

The repository contains the exported n8n workflow:

```text
telegram-study-notes-bot.json
```

To use it:

1. Open an n8n Cloud workspace.
2. Import the JSON workflow.
3. Configure the required credentials.
4. Connect the required Telegram, Google, Gemini, Tavily, Drive, Docs, and Sheets services.
5. Verify the node configurations.
6. Activate/publish the workflow.
7. Send a study topic through Telegram.

> Credential IDs and service-specific configuration may need to be updated when importing the workflow into another n8n workspace.

---

## ⚠️ Security

This repository contains the workflow configuration but should not contain:

* API keys
* Telegram bot tokens
* Passwords
* OAuth secrets
* Private credentials

Always configure credentials through n8n's credential management system rather than hardcoding secrets into workflow nodes.

---

## 🔮 Future Improvements

Possible future enhancements include:

* `/quiz` command for quiz-only generation
* `/flashcards` command for flashcard-only generation
* `/summary` command for short summaries
* `/revision` command for quick revision notes
* `/interview` command for interview preparation
* `/explain` command for simplified explanations
* Personalized difficulty levels
* Subject-specific study modes
* PDF customization
* Study progress tracking
* Topic history
* Scheduled revision reminders
* Multi-language study notes

---

## 🎯 Project Objective

The goal of this project is to demonstrate how **AI, workflow automation, conversational memory, web search, document generation, cloud storage, and messaging platforms** can be combined into a practical educational automation system.

Instead of manually researching a topic, writing notes, formatting a document, converting it into PDF, and sharing it, the entire process is automated through a single Telegram message.

---

## 👩‍💻 Author

**Deeksha Ganiger**

Built as an AI automation project using n8n and modern AI services.
