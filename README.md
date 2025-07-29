
# 🧩 n8n Automation Workflows

This repository contains a collection of my custom-built n8n automation workflows in `.json` format. These workflows can be imported directly into an n8n instance to automate various tasks such as data syncing, email notifications, API integrations, and more.

---

## 📂 Repository Structure

Each `.json` file in this repo represents a single n8n workflow. Filenames are descriptive to help identify their purpose.

    workflows/
    ├── sheets-to-email.json
    ├── api-data-fetcher.json
    ├── daily-summary-to-telegram.json
    └── ...

---

## 🚀 Getting Started

To use any of these workflows:

1. Download or clone this repository:
   git clone https://github.com/shivasubrahmanya/n8n-Automations.git

2. Open your n8n instance (cloud or self-hosted).

3. Import a workflow:
   - Go to the n8n editor.
   - Click the ☰ menu → Import Workflow.
   - Upload the `.json` file of the workflow you want to use.

4. Customize as needed:
   - Add your own credentials, webhook URLs, sheet IDs, etc.
   - Activate the workflow if needed.

---

## 🛠 Requirements

- A running instance of n8n
- Proper credentials set up in your n8n credentials manager for each service used (Google Sheets, Gmail, Telegram, etc.)

---

## ✍️ Contribution

Feel free to open issues or pull requests if:
- You find a bug in a workflow.
- You want to suggest a new automation.
- You want to contribute your own n8n workflows.

---

## 🙌 Acknowledgments

Thanks to the n8n community and all open-source tool builders that help make automation easier and more accessible.

---

## 💡 About n8n

n8n (pronounced "n-eight-n") is an extendable workflow automation tool that lets you connect various services via low-code/no-code flows.

Learn more: https://n8n.io
