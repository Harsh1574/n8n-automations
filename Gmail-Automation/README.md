# 📧 Daily Email Digest — AI-Powered Inbox Summarizer

> **Built with:** n8n · Python · OpenAI GPT-3.5 · Gmail API  
> **Type:** Scheduled Automation · AI Pipeline · Custom HTML Rendering

---

## 🧠 What This Does

This workflow runs every morning at 7 AM and delivers a **priority-sorted HTML email digest** of all emails received in the past 24 hours — summarized and ranked by urgency using AI.

Instead of manually scanning dozens of emails, you wake up to a single clean table showing exactly what needs your attention and in what order.

---

## 🏗️ Architecture

```
Schedule Trigger (7 AM)
    → Gmail API (fetch last 24hrs)
    → Python Code Node (clean + batch emails into groups of 10)
    → Loop Over Items
         → OpenAI GPT-3.5 (summarize each batch)         ← loop
    → Python Code Node (combine all batch summaries)      ← done
    → OpenAI GPT-3.5 (merge into single priority table)
    → Python Code Node (convert markdown → HTML table)
    → Gmail API (send digest email)
```

---

## ⚙️ Key Technical Decisions

### 1. Batched API Architecture (My Own Optimization)
Rather than sending each email individually to the AI (50 emails = 50 API calls), I designed a **batching system** that groups emails into sets of 10 before sending them to the model.

This reduces API calls by **10x** while staying safely within token limits — a critical consideration for production-grade automation.

```python
# Group emails into batches of 10
batch_size = 10
batches = [emails[i:i+batch_size] for i in range(0, len(emails), batch_size)]
```

### 2. Two-Stage AI Pipeline
The workflow uses a **Map-Reduce pattern**:
- **Stage 1 (Map):** Each batch of 10 emails is summarized individually
- **Stage 2 (Reduce):** All batch summaries are merged into one final priority-sorted table

This mirrors how production LLM pipelines handle large document sets.

### 3. Structured Data Input
Instead of sending raw email HTML to the AI, each email is first cleaned and structured into a compact JSON format:

```python
emails.append({
    "id": item["json"].get("id", ""),
    "from": item["json"].get("From", ""),
    "subject": item["json"].get("Subject", ""),
    "body": item["json"].get("snippet", "")
})
```

This reduces token usage, improves AI accuracy, and prevents email formatting artifacts from polluting the prompt.

### 4. Custom HTML Table Builder
n8n's built-in Markdown node does not support table rendering in Gmail. Rather than using a third-party library, I wrote a custom Python parser that:
- Parses the AI's markdown table output line by line
- Skips duplicate headers and separator rows
- Renders a styled HTML table with a green header row

```python
# Dynamically detect newline format and parse into HTML
if "\\n" in text:
    lines = text.split("\\n")
else:
    lines = text.split("\n")
```

---

## 📊 Output

The digest email renders as a clean HTML table with:

| Column | Description |
|--------|-------------|
| **Sender** | Who sent the email |
| **Subject** | Email subject line |
| **Summary** | AI-generated concise summary |
| **List of Actions** | Specific actions required (or "None") |

Rows are **sorted by priority** — high urgency emails appear at the top.

---

## 🔧 Setup

### Prerequisites
- n8n Cloud account
- Gmail OAuth2 credentials
- OpenAI API key (GPT-3.5-Turbo)

### Configuration
1. Import the workflow JSON into n8n
2. Connect Gmail OAuth2 credential
3. Add OpenAI API key
4. Set your email address in the Gmail Send node
5. Activate the workflow

---

## 💡 What I Learned

- **Loop architecture in n8n** — using Loop Over Items with loop/done branching paths
- **Two-stage LLM pipelines** — Map-Reduce pattern for processing large datasets
- **Token optimization** — structuring input data to minimize API costs
- **Python in n8n** — writing custom data transformation logic
- **HTML email rendering** — building custom parsers when built-in tools fall short
- **Prompt engineering** — designing strict prompts that return consistent, parseable output

---

## 🚀 Future Improvements

- [ ] VIP sender filter — only process emails from important contacts
- [ ] Weekday-only execution using IF node
- [ ] Exclude self-sent emails from the digest
- [ ] Google Sheets integration to log daily digests
- [ ] Slack notification as alternative to email delivery

---

*Part of my n8n automation portfolio — [github.com/Harsh1574/n8n-automations](https://github.com/Harsh1574/n8n-automations)*

---
## 👤 Author

**Harsvardhan Rajgarhia**

**CSBS'27, Academy Of Technology**

[![Gmail](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:harsvardhanrajgarhia@gmail.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/harshvardhan-rajgarhia-ba62982a4)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Harsh1574)

---
