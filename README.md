# 🦷 AI Dental Office Agent (n8n + AI)

This project implements an advanced **AI Agent** that manages a dental cabinet's operations. It acts as a virtual assistant capable of handling appointment scheduling, patient file management, and real-time communication.

The agent is designed to take autonomous action by using specific tools to interact with the [Medical Cabinet Platform](https://github.com/Mustapha-Kdb/ai_medical_cabinet_platform_endtoend) via API calls (CRUD operations) and communicating with patients through **WhatsApp**.

## 🚀 Key Features

* **Real-time Communication:** Uses Webhooks to listen to patient messages on WhatsApp and replies instantly.
* **Smart Scheduling:** * Retrieves service durations automatically.
    * Checks doctor availability for specific dates/times.
    * Proposes the closest alternative slots if the requested time is unavailable.
* **Patient Management:** Handles Identity Verification before allowing the agent to Create, Read, or Update patient files.
* **Proactive Reminders:** Automatically sends a reminder message to patients 24 hours before their consultation.

## 🏗️ System Architecture

The solution is divided into two specialized **n8n workflows**:

### 1. Data Sync & Optimization
This workflow collects medical service details from the main platform and stores them in a local n8n database.
* **Sync Frequency:** Daily.
* **Purpose:** Ensures the AI Agent has fast, permanent access to service data, optimizing response times and reducing API overhead.

![Data Sync Workflow](./screenshots/service_data_importation_workflow.png)

### 2. Core AI Agent & Task Handling
This is the "brain" of the project, responsible for executing logic and using tools:
* **Identity Verification:** Cross-checks patient answers with file details.
* **Appointment Logic:** Manages the full flow from service selection to final validation.
* **CRUD Operations:** Seamlessly updates the medical center platform based on user requests.

![Data Sync Workflow](./screenshots/agent_workflow.png)

## 🔒 Security & Context Management (Session Memory)

To ensure a personalized and secure experience, the agent implements a **Persistent Memory System** based on the sender's unique ID (e.g., WhatsApp Phone Number):

* **Isolated Sessions:** The AI keeps track of the conversation history specifically for each sender ID. This ensures the agent remembers past questions and context from the current user.
* **Data Privacy & Leak Prevention:** The memory architecture guarantees that user data is strictly isolated. The model cannot access or "leak" information from one user's session to another, ensuring that private medical inquiries remain confidential.
* **Context Accuracy:** By filtering memory through unique IDs, the agent avoids "hallucinating" details from other conversations, providing highly accurate and context-aware responses.

## 🛠️ Tech Stack
* **Automation:** [n8n.io](https://n8n.io/)
* **AI:** AI Agent with Tool Calling capabilities.
* **Channels:** WhatsApp (via Webhooks).
* **Backend:** Custom API ([Medical Center Platform](https://github.com/Mustapha-Kdb/ai_medical_cabinet_platform_endtoend)).
