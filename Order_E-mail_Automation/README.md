# 📦 Order Email Automation with n8n, Google Sheets & Ollama (LLaMA3)

This project automates the process of sending structured email summaries based on new customer orders submitted to a Google Sheet. It uses **n8n** to orchestrate the workflow, integrates with **Ollama (LLaMA3)** for intelligent email generation, and sends emails via **Gmail**.

---

## 🔧 Tech Stack

- n8n – Workflow automation platform
- Google Sheets – Order data source
- Gmail API – To send the emails
- Ollama (LLaMA3) – Local LLM for generating structured email content
- JSON – Used for API request/response between nodes

---

## 📌 Features

- ⏱️ Polls a Google Sheet every minute for new entries.
- 🧠 Uses LLaMA3 (via Ollama) to analyze and summarize order data.
- 📧 Sends professional email summaries to a specified email address.
- 🔁 Fully automated, end-to-end.
- 🛡️ Keeps data local and private using a self-hosted LLM.

---

## ⚙️ Workflow Overview

1. **Google Sheets Trigger**
   - Monitors a specific Google Sheet every minute for new order rows.
   - Sheet example:
     ```
     Order ID | Customer Name | Product | Quantity | Price (₹) | Order Date | Status
     ```

2. **Ollama Model (HTTP Request)**
   - Sends order data to a locally running Ollama instance (`http://127.0.0.1:11434/api/generate`) using the `llama3` model.
   - Prompt instructs the model to return:
     ```json
     {
       "EmailSubject": "...",
       "EmailBody": "..."
     }
     ```

3. **Send a Message (Gmail Node)**
   - Sends the generated subject and body to the predefined email address using Gmail API.

---

## 🧪 Example Email Output

**Subject:**
New Order Received: #ORD1234

**Body:**
Dear Team,

We have received a new order from Mr. Ramesh Kumar for 3 units of 'Bluetooth Speakers' priced at ₹1500 each.

Order Date: 2025-08-01
Status: Pending

Please take the necessary steps to process this order.

Regards,
Order Automation Bot

---

## 🛠️ Setup Instructions

1. Clone or open this project in n8n.

2. Set up credentials:
   - Google Sheets OAuth2
   - Gmail OAuth2
   - Make sure your sheet is shared with the service account if needed.

3. Run Ollama locally:
ollama run llama3


4. Update the Google Sheet ID and Sheet Name in the trigger node.

5. Deploy and activate the workflow.

---

## 🗂️ Project Files

Order_E-mail_automation/
├── README.md <-- This file
├── workflow.json <-- n8n workflow JSON

---

## 🤖 Prompt Template Used for LLaMA3

You are in charge of client orders. Your job is to summarize new orders in a structured JSON format for email communication.

Please return a JSON response with two fields:

EmailSubject: a short email subject line

EmailBody: a polite, professional email message for the team

Here is the information on the new order:
Order ID: {{ Order ID }}
Customer Name: {{ Customer Name }}
Product: {{ Product }}
Quantity: {{ Quantity }}
Price: {{ Price (₹) }}
Order Date: {{ Order Date }}
Status: {{ Status }}

Respond only with JSON, nothing else.


---

## 📬 Author

Made with ❤️ by Shivasubrahmanya K C
