# 🍔 CraveAI — AI-Powered Food Ordering Agent

[![m.png](https://i.postimg.cc/Gp3f2d45/m.png)](https://postimg.cc/xX75pryv)

**An AI-powered food ordering assistant built with ElevenLabs, n8n, and Google Sheets to demonstrate conversational ordering, menu discovery, delivery validation, customer management, and order processing.**

CraveAI is a portfolio prototype exploring how conversational AI and workflow automation can streamline a food ordering experience. A voice-enabled agent can help customers explore menu options, check delivery availability, provide customer details, and submit orders through connected workflows.

> **Status:** Functional prototype / proof of concept  
> **Stack:** ElevenLabs · n8n Cloud · Google Sheets · Webhooks  
> **Purpose:** Demonstrate AI agent integrations and workflow automation



**Watch the Full Project Demonstration:**
[▶️ Live Demo Video](https://elevenlabs.io/app/talk-to?agent_id=agent_4801m5wxk4e5fkcaan3pqf5319kh&branch_id=agtbrch_2001m5wxk5pnfd1rkrm2e7beq0tk)
---

## 📌 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [Architecture](#-architecture)
- [Technology Stack](#-technology-stack)
- [Workflows](#-workflows)
- [Order Flow](#-order-flow)
- [Repository Structure](#-repository-structure)
- [Getting Started](#-getting-started)
- [Configuration](#-configuration)
- [Testing](#-testing)
- [Security and Privacy](#-security-and-privacy)
- [Limitations](#-limitations)
- [Future Improvements](#-future-improvements)
- [Author](#-author)

---

## 🚀 Overview

CraveAI connects a conversational voice agent to backend automation workflows. Instead of treating the solution as a standalone chatbot, the project demonstrates how an AI agent can call tools to retrieve menu information, check delivery details, manage customer data, and process an order.

### Objectives

- Demonstrate voice-enabled AI interaction.
- Automate common food-ordering operations.
- Connect an AI agent to backend workflows using webhooks.
- Store structured customer and order data in Google Sheets.
- Explore a practical AI agent use case for food ordering.

---

## ✨ Key Features

### 🍽️ Menu Search
- Search for food items using customer queries.
- Retrieve matching menu items and prices.
- Present options to help customers make decisions.

### 📍 Delivery Zone Check
- Check delivery availability for a customer location.
- Retrieve applicable delivery fees.
- Provide an estimated delivery time when configured.

### 👤 Customer Management
- Handle customer information required for an order.
- Connect customer-management operations with Google Sheets.
- Support structured customer data handling.

### 🛒 Order Processing
- Process order details through a dedicated workflow.
- Calculate totals, including applicable delivery charges.
- Generate an order reference.
- Record order and item information in Google Sheets.
- Support cash-on-delivery in the demonstrated prototype.

### 🎙️ Voice-Based Interaction
- Integrate an ElevenLabs voice agent into the ordering experience.
- Allow customers to make conversational requests.
- Connect the voice interface to backend automation.

### 🔗 Modular Workflows
- Separate core operations into individual n8n workflows.
- Use webhooks to connect components.
- Keep workflow logic independently maintainable.

---

## 🏗️ Architecture

```text
                  ┌────────────────────────┐
                  │        Customer        │
                  └───────────┬────────────┘
                              │
                              ▼
                  ┌────────────────────────┐
                  │ ElevenLabs Voice Agent │
                  └───────────┬────────────┘
                              │ Tool / webhook calls
                              ▼
                  ┌────────────────────────┐
                  │      n8n Cloud         │
                  │ Workflow Orchestration │
                  └───────────┬────────────┘
                              │
             ┌────────────────┼────────────────┐
             ▼                ▼                ▼
      ┌─────────────┐  ┌─────────────┐  ┌──────────────┐
      │ Menu Search │  │ Delivery    │  │ Customer     │
      │             │  │ Zone Check  │  │ Management   │
      └─────────────┘  └─────────────┘  └──────────────┘
                              │
                              ▼
                     ┌────────────────┐
                     │ Order Processing│
                     └────────┬───────┘
                              │
                              ▼
                     ┌────────────────┐
                     │ Google Sheets  │
                     │ Data Storage   │
                     └────────────────┘
```

*This diagram shows the logical components. The actual execution paths depend on the imported workflow configurations and agent tool connections.*

---

## 🧰 Technology Stack

| Technology | Purpose |
|---|---|
| **ElevenLabs** | Voice-enabled conversational AI interface |
| **n8n Cloud** | Workflow automation and orchestration |
| **Google Sheets** | Structured menu, customer, and order data |
| **Webhooks** | Communication between the agent and n8n workflows |
| **JSON** | Workflow export, sharing, and version control |

---

## ⚙️ Workflows

This repository includes four exported n8n workflow JSON files.

| Workflow | Responsibility |
|---|---|
| **Menu Search** | Searches the menu and returns matching food items and prices. |
| **Delivery Zone Check** | Checks delivery availability and returns configured delivery details. |
| **Customer Management** | Handles customer information through the configured data workflow. |
| **Order Processing** | Processes order details and records the resulting order information. |

The exported JSON files contain workflow configurations. Credentials, spreadsheet references, webhook URLs, and other environment-specific values may need to be configured after import.

---

## 🔄 Order Flow

A typical interaction follows this sequence:

1. The customer tells the voice agent what they want.
2. The agent calls the **Menu Search** workflow to retrieve relevant menu items.
3. The **Delivery Zone Check** workflow checks the delivery location.
4. The **Customer Management** workflow handles the required customer information.
5. The agent submits order details to the **Order Processing** workflow.
6. The workflow processes item quantities, prices, and applicable delivery fees.
7. Google Sheets stores the configured order information.
8. The result can be returned to the agent for customer confirmation.

The exact behavior depends on the workflow nodes, request payloads, and integration settings.

---

## 📂 Repository Structure

Example structure (adjust filenames and folders to match this repository):

```text
CraveAI/
├── README.md
└── workflows/
    ├── menu-search.json
    ├── delivery-zone-check.json
    ├── customer-management.json
    └── order-processing.json
```

If your JSON files are stored in the repository root, update this example to reflect that.

---

## 🛠️ Getting Started

### Prerequisites

- An [n8n](https://n8n.io/) instance or n8n Cloud account.
- A [Google account](https://www.google.com/) for Google Sheets integration.
- An [ElevenLabs](https://elevenlabs.io/) account to reproduce the voice-agent experience.
- Access to the credentials and configuration values required by the workflows.

### 1. Clone the Repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd <YOUR_REPOSITORY_NAME>
```

Replace the placeholders with your actual repository URL and name.

### 2. Import the Workflows

For each JSON export:

1. Open your n8n instance.
2. Create or open a workflow.
3. Use n8n's workflow import option to import the JSON file.
4. Review the nodes, connections, and expected inputs.
5. Configure missing credentials and environment-specific values.
6. Save the workflow.

Repeat for all four workflows.

### 3. Configure Google Sheets

- Connect your Google account using the appropriate n8n credential.
- Select or create the required spreadsheet.
- Map the workflows to the correct sheets and columns.
- Confirm that the spreadsheet structure matches each workflow's expected data format.

### 4. Configure Webhooks

- Review the webhook nodes and their HTTP methods, paths, and payload formats.
- Activate the workflows when ready.
- Use production webhook URLs for deployed integrations.
- Update the corresponding tool URLs in the voice agent.

Use test webhook URLs only during development and testing.

### 5. Connect the Voice Agent

Configure the ElevenLabs agent to call the relevant workflows using the integration mechanism supported by your setup. Check that request fields and response formats match what each workflow expects.

---

## 🔐 Configuration

Depending on your setup, the workflows may require:

- Google Sheets credentials.
- Spreadsheet IDs and worksheet names.
- Webhook URLs.
- Menu and delivery-zone data.
- Voice-agent tool configuration.
- Order-processing parameters.

Configure these values within the relevant service or workflow. Avoid hardcoding secrets into files that will be published publicly.

**Never commit API keys, access tokens, private customer information, or production credentials to GitHub.**

---

## 🧪 Testing

Use sample data to verify the workflows before connecting them to any real ordering environment.

| Test Scenario | Expected Result |
|---|---|
| Search for an available menu item | Matching items and prices are returned. |
| Search for a nonexistent item | A suitable no-results response is returned. |
| Check an eligible delivery location | Configured delivery details are returned. |
| Check an ineligible location | Delivery unavailability is handled appropriately. |
| Submit a valid order | Order information is processed and recorded. |
| Submit incomplete or invalid details | The workflow handles the request safely. |
| Verify a saved order | The relevant records can be found in Google Sheets. |

---

## 🔒 Security and Privacy

CraveAI is a portfolio prototype. Before adapting it for a real business:

- Store API keys and service credentials securely.
- Avoid exposing webhook endpoints unnecessarily.
- Validate incoming webhook payloads.
- Protect customer names, phone numbers, and delivery addresses.
- Restrict access to customer and order spreadsheets.
- Remove personal data and sensitive execution information from public exports.
- Add suitable authentication, error handling, and request validation.
- Ensure order totals and order state are validated by backend logic.

Review all workflow JSON files before publishing them to ensure they do not contain credentials, sensitive URLs, or personal information.

---

## ⚠️ Limitations

- This is a proof of concept, not a production-ready restaurant ordering platform.
- Restaurant, menu, delivery, and customer data are intended for demonstration.
- Live restaurant availability and actual delivery fulfillment are not guaranteed.
- Behavior depends on the configured n8n workflows and connected services.
- Real payment processing, restaurant POS integration, and production-grade order lifecycle management are not part of the stated prototype scope.

---

## 🔮 Future Improvements

- Integrate real restaurant menus and inventory systems.
- Add order-status tracking and customer notifications.
- Improve input validation and structured error handling.
- Add authentication and access controls for webhook endpoints.
- Expand multilingual Urdu-English interactions.
- Integrate restaurant POS and delivery-management platforms.
- Add monitoring, logging, and automated workflow tests.

---

## 👨‍💻 Author

**Huzaifa Sheikh**  
AI Agent Developer · Workflow Automation · Backend Development

- **Portfolio:** [Huzaifa AI Solutions](https://huzaifa-ai-solutions.vercel.app/)
- **GitHub:** [@Huzafi](https://github.com/Huzafi)
- **LinkedIn:** [Huzaifa Sheikh](https://www.linkedin.com/in/huzaifa-sheikh-b2a012342/)

---

## 📄 License

Add a license file if you want to define how others may use, modify, or redistribute this project. Without an applicable license, default copyright protections generally apply.

---

**CraveAI — Turning conversational AI into an automated food-ordering experience.** 🍔🤖

