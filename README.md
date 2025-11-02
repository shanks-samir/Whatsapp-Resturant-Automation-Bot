# Whatsapp-Resturant-Automation-Bot
This project delivers a robust, low-code solution for automating customer order management, inventory checks, and frequently asked questions (FAQs) for a restaurant directly through WhatsApp. It leverages powerful workflow automation (n8n), Google's Gemini AI for conversational intelligence, and Google Sheets as a flexible, no-fuss database.

This bot transforms customer service by providing 24/7, intelligent, and personalized responses, dramatically reducing the manual effort required for order fulfillment.

**Media & Screenshots**


**Key Features**

**Intelligent Order Processing**: Automatically initiates, collects, and validates customer orders based on a multi-step conversation.
**Real-time Inventory Validation**: The bot uses the database to check item availability before accepting an order (e.g., if "Extra Rice" is out of stock, the bot informs the user and denies the specific request).
**Conversational AI (Gemini)**: Utilizes an LLM agent to handle complex, open-ended questions and maintain a natural conversation flow.

This project delivers a robust, low-code solution for automating customer order management, inventory checks, and frequently asked questions (FAQs) for a restaurant directly through WhatsApp. It leverages powerful workflow automation (n8n), Google's Gemini AI for conversational intelligence, and Google Sheets as a flexible, no-fuss database.
This bot transforms customer service by providing 24/7, intelligent, and personalized responses, dramatically reducing the manual effort required for order fulfillment.

**Technology Stack**

| Component          | Role                                                                 | Technology                        |
|-------------------|----------------------------------------------------------------------|-----------------------------------|
| **Workflow Engine**   | Orchestrates all automated tasks and connections (trigger, logic, tools) | n8n (Open Source Automation Tool) |
| **Conversational AI** | Provides the intelligence for understanding, responding, and decision-making | Google Gemini (LLM Agent)         |
| **Messaging Gateway** | The official platform for connecting the automation to WhatsApp   | WhatsApp Business API (Meta)      |
| **Database/CRM**      | Stores inventory lists, FAQs, and new customer order records      | Google Sheets                     |


**Prerequisites**

To deploy this project, you will need the following accounts and credentials:
n8n Account: (For hosting and running the automation workflow).
Google Account: (For creating and connecting the Google Sheets database).
Google AI Studio/MakerSuite Account: (To generate a Gemini API Key).
Meta for Developers Account: (To set up the WhatsApp Business API, which requires an App ID and an Access Token).

**Setup & Deployment**

The deployment process is broken down into four core steps within the n8n environment:

1. Database Setup (Google Sheets)
Create a single Google Sheet with three separate sheets (tabs) to serve as the core data source:
Inventory: Lists all available menu items and their stock status.
Order: The sheet where new customer orders will be appended.
FAQ: Contains common questions and pre-set answers for the bot to reference.

2. Core Workflow & Trigger
Create a new workflow in n8n.
Configure the WhatsApp Business On Message node as the starting Trigger.
Connect the Trigger to your Meta App ID and Client Secret (obtained from Meta for Developers).

3. AI Agent Configuration
Add an AI Agent node and connect it after the WhatsApp trigger.
Chat Model: Select Gemini and provide your API Key as the credential.
Memory: Implement Simple Memory to maintain short-term context across a set number of messages (e.g., last 10 messages).
System Message (Instructions): Write detailed instructions for the Gemini agent, including:
The restaurant's name (e.g., "MDA Restaurant").
The primary language/tone for conversation.
The CRITICAL rule: Only fulfill orders that are currently available in the Inventory tool.

**4. Tool Integration (Google Sheets)**
Create three Google Sheets nodes and connect them as Tools within the AI Agent configuration:

Tool: Get_Inventory
Operation: Read rows from the Inventory sheet.
Purpose: Allows the AI to check item availability.
Tool: Get_FAQ
Operation: Read rows from the FAQ sheet.
Purpose: Allows the AI to answer general restaurant questions.
Tool: Place_Order
Operation: Append Row to the Order sheet.
Purpose: When the AI decides an order is ready, it uses this tool, which will prompt the user for necessary details (e.g., Name, Address, Quantity) and save the data.

**5. Final Connection (The Reply)**
Add a WhatsApp Business Send Message node at the end of the workflow.
Connect the output of the AI Agent node to the Text Body of the Send Message node.
Activate the n8n workflow to make the bot live.

**Future Enhancements**

Payment Gateway Integration: Integrate with a service like Stripe or a regional payment system to collect payments immediately upon order confirmation.
Delivery/Logistics Integration: Connect to a delivery management system (e.g., tracking software) to automatically schedule pickups.
Multi-language Support: Use n8n's logic nodes to detect the input language and switch the system message/tool responses accordingly.
Admin Notifications: Send an automated internal notification (e.g., to Slack or Telegram) to the restaurant staff whenever a new order is successfully placed.: Employs simple memory to recall key details (like the customer's name) throughout the conversation for a personalized experience.
Automated Database Entry: Successfully placed orders are instantly appended to a Google Sheet (acting as a live Order CRM).
FAQ Handling: Answers common questions about the restaurant (e.g., "What time do you open?", "Do you support online payments?").


Admin Notifications: Send an automated internal notification (e.g., to Slack or Telegram) to the restaurant staff whenever a new order is successfully placed.
