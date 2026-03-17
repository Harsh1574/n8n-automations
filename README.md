# 🤖 n8n Automations

> A collection of production-ready AI automation workflows built with n8n, OpenAI, and Gmail API.  
> Built as part of a structured learning path toward AI automation engineering.

---

## 👋 About This Repo

I'm Harsvardhan — a Data Science student learning to build real-world AI automation systems from scratch.

This repository documents my journey of building increasingly complex n8n workflows — starting from basic scheduled automations, progressing toward multi-tool AI agents, RAG pipelines, and agentic systems.

Every workflow here is:
- **Built from scratch** — no copy-paste from tutorials
- **Stress-tested** — edge cases identified and fixed
- **Documented** — with architecture, learnings, and enhancements
- **Versioned** — improvements tracked over time

---

## 📁 Workflows

### 1. 📧 [Gmail Daily Email Digest](./Gmail_Daily_Email_Digest/)
> Triggers every morning to deliver a priority-sorted HTML table summarizing all emails received in the last 24 hours — with sender, subject, summary and required actions clearly laid out.

**Highlights:**
- Batched API architecture — groups emails into sets of 10, reducing API calls by 10x
- Two-stage Map-Reduce LLM pipeline — summarize individually, merge into one priority table
- Custom Python HTML table builder — bypasses n8n's markdown rendering limitations
- Structured JSON input to AI — reduces token usage and improves accuracy

**Tech:** n8n · Python · OpenAI GPT-3.5 · Gmail API

---

### 2. 🏷️ [Gmail AI Label Organizer](./Gmail_AI_Label_Organizer/)
> Reads every incoming email in real-time, processes it using an AI Agent to understand its context and intent, then applies the most appropriate label — creating new ones autonomously if needed.

**Highlights:**
- First AI Agent build — uses ReAct pattern with 3 Gmail tools
- Autonomous label creation — agent builds the entire label taxonomy from scratch
- Conflict resolution via prompt engineering — correctly handles emails with multiple category keywords
- Tested on edge cases — vague subjects, mixed languages, contradicting subject/body

**Tech:** n8n · OpenAI GPT-3.5 · Gmail API · AI Agents

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| **n8n Cloud** | Workflow automation platform |
| **OpenAI GPT-3.5** | Language model for summarization and classification |
| **Gmail API** | Email fetching, label management, sending |
| **Python** | Custom data transformation logic in Code nodes |
| **Prompt Engineering** | Structured prompts for consistent AI output |

---

## 📈 Learning Progression

```
Week 1 — n8n Basics
    ✅ Schedule Trigger, Gmail nodes, Markdown nodes
    ✅ Basic LLM Chain (Summarization Chain)
    ✅ Debugging API credentials and rate limits

Week 2 — Optimization + AI Agents
    ✅ Batched API architecture (Python Code nodes)
    ✅ Loop Over Items + Map-Reduce pattern
    ✅ First AI Agent with tools
    ✅ Prompt engineering for conflict resolution

Upcoming →
    ⬜ RAG pipelines with vector databases
    ⬜ Multi-agent systems
    ⬜ Webhook-based event-driven automations
    ⬜ Slack and Telegram bots
```

---

## 🧠 Key Concepts Learned

- **Chains vs Agents** — chains follow fixed steps, agents decide their own tool-calling order
- **Map-Reduce pattern** — processing large datasets in batches then combining results
- **Token optimization** — structuring input data to minimize API costs
- **ReAct pattern** — how agents reason and act iteratively using tool results
- **Prompt engineering** — writing instructions that produce consistent, parseable output
- **Event-driven vs scheduled triggers** — choosing the right trigger for the right use case

---

## 📬 Connect

- **GitHub:** [github.com/Harsh1574](https://github.com/Harsh1574)
- **n8n Cloud:** [harsh1574.app.n8n.cloud](https://harsh1574.app.n8n.cloud)

---

*This repo is actively maintained and updated as I build more workflows. Star ⭐ to follow the journey!*
