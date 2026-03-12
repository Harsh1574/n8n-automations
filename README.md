# 📧 Daily Email Digest — n8n Automation Workflow
 
## Overview
An automated n8n workflow that runs every morning and delivers a prioritized summary of all emails received in the last 24 hours directly to your inbox — so you never miss anything important.
 
---
 
## 🧩 How It Works
 
```
Schedule Trigger → Gmail (Fetch) → Markdown (Clean) → Summarization Chain → Markdown (Convert) → Gmail (Send)
                                                              ↑
                                                    Google Gemini AI
```
 
1. **Schedule Trigger** — Fires daily at 7 AM
2. **Gmail (Get Messages)** — Fetches all emails received in the last 24 hours
3. **Markdown Node** — Cleans raw HTML email content into plain text
4. **Summarization Chain** — Sends cleaned emails to an AI model which summarizes each one individually, then combines them into a single prioritized digest
5. **Markdown to HTML** — Converts the AI's markdown table output into HTML for proper email rendering
6. **Gmail (Send)** — Delivers the final digest to your inbox
 
---
 
## 📊 Output Format
 
The workflow delivers a neatly formatted HTML table with 4 columns:
 
| Sender | Subject | Summary | Actions |
|--------|---------|---------|---------|
| John Doe | Project Update | Brief summary of the email | Action items listed here |
 
Emails are **sorted by priority** — those requiring the most urgent actions appear at the top.
 
---
 
## 🛠️ Tech Stack
 
- **Automation Platform:** n8n
- **AI Model:** Google Gemini (via Google AI Studio)
- **Email Integration:** Gmail OAuth2
- **Summarization Method:** Map Reduce Chain (LangChain)
 
---
 
## ⚙️ Setup Instructions
 
### Prerequisites
- n8n cloud account (or self-hosted n8n)
- Gmail account
- Google AI Studio API key (free tier available at aistudio.google.com)
 
### Steps
1. Import `daily-email-digest.json` into your n8n instance
2. Connect your **Gmail credential** via OAuth2
3. Add your **Google Gemini API key** in the Gemini Chat Model node
4. Set your preferred trigger time in the Schedule Trigger node
5. Activate the workflow
 
---
 
## 💡 Potential Enhancements
 
- Add an **IF node** to skip weekends (Monday–Friday only)
- Filter emails by **VIP senders** using the Gmail Sender filter
- Store last execution timestamp in **Google Sheets** for fault-tolerant recovery
- Add a **Slack notification** alongside the email digest
- Expand to include **calendar events** alongside email summaries
 
---
 
## 🎯 Use Cases
 
- **Managers** dealing with high email volumes
- **HR professionals** tracking applicant communications
- **Executives** who need a quick morning briefing
- Anyone who wants to **reclaim time** spent in their inbox
 
---
## 👤 Author

**Harsvardhan Rajgarhia**

**CSBS'27, Academy Of Technology**

[![Gmail](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:harsvardhanrajgarhia@gmail.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/harshvardhan-rajgarhia-ba62982a4)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Harsh1574)

---
