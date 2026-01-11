## 🚀 Overview

The workflow acts as an autonomous "Executive Editor," performing real-time research and high-vocabulary reporting in the style of the Times of India.

### Data Sources

* **Google Custom Search**: General web news and high-quality metadata/images.
* **Hacker News (Algolia)**: Real-time developer and tech community trends.
* **Reddit**: Social sentiment and public opinion.
* **NewsAPI**: Global business and finance reporting.
* **arXiv**: Scientific and academic research papers.

## 🛠️ Features

* **Multi-Agent Research**: Aggregates data from five different APIs simultaneously.
* **LLM Synthesis**: Uses GPT-4.1-mini to convert raw JSON data into a structured newspaper layout (Headline, Subheading, Byline, and Lead Story).
* **Intelligent Image Sourcing**: Prioritizes images found in research data or falls back to topic-relevant placeholders.
* **Dual Distribution**:
* **Gmail**: Sends a fully responsive, table-based HTML email (optimized for mobile and desktop).
* **Slack**: Delivers a structured, formatted message with "Read More" links.


* **Error Resilience**: Includes "Continue on Fail" logic for scientific research nodes and custom regex parsers for XML (arXiv).

## 📋 Prerequisites

To use this workflow, you will need credentials for the following services:

1. **n8n Instance**: (v1.x+ recommended).
2. **OpenAI**: API Key for GPT models.
3. **Slack**: Bot Token with `app_mention` and `chat:write` scopes.
4. **Google Cloud**:
* Custom Search API Key and CX ID.
* Gmail OAuth2 credentials.


5. **NewsAPI**: Free API Key for business news.

## ⚙️ Configuration

1. **Import the JSON**: Copy the content of `Yesh_Slack_Gmail_Newsletter.json` and paste it into a new n8n workflow.
2. **Assign Credentials**: Update the following nodes with your specific accounts:
* `Slack Trigger` & `Send a message`
* `OpenAI Chat Model`
* `Google Custom search`
* `Gmail Mail Send`


3. **Topic Customization**: The workflow is currently set to the "Digital Intelligence Edition" based in Chennai. You can modify the `HTML` and `JSON Slack` nodes to change the branding.

## 🧬 Workflow Architecture

1. **Trigger**: User mentions the bot in Slack with a topic (e.g., *"The growth of AI and its impact on IT Jobs"*).
2. **Research**: Five parallel HTTP requests fetch raw data.
3. **Processing**: Custom JavaScript nodes normalize the different JSON/XML formats.
4. **AI Chain**: A LangChain-powered LLM summarizes the data into a specific JSON schema.
5. **Formatting**: An HTML node builds the responsive email, while a JS node builds the Slack markup.
6. **Delivery**: Final nodes trigger the email and Slack post.

---

## 📄 Node Descriptions (Internal Documentation)

| Node Name | Function |
| --- | --- |
| **Edit Fields** | Cleans the Slack trigger text to extract the core topic. |
| **Merge** | Collects results from all 5 research streams. |
| **Basic LLM Chain** | The "Editor-in-Chief" that enforces the British English tone and newspaper structure. |
| **HTML** | Contains the responsive CSS and table structure for Gmail. |
| **JSON Slack** | Recreates the newspaper masthead using ASCII and Slack Markdown. |
| **science code** | A specialized regex-based parser for arXiv's XML feed. |

---

*Built with n8n and YESH Intelligence.*
