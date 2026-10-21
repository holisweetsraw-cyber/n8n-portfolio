# Ilona Bila: n8n & AI Automation Portfolio

**n8n & AI Automation Specialist · RAG · Multi-Agent Systems · GDPR-Compliant Design**

> I build automations that turn manual, repetitive work into systems that run themselves: n8n, Make and AI agents for CRM, bookings and inbox workflows. They're grounded in a business background, not just a technical one.

📖 [Case studies on Notion](https://ilona-bila-portfolio.notion.site/Portfolio-36e9e4dcbceb81baaf15cd1c34d83d11) · 💼 [Upwork profile](https://www.upwork.com/freelancers/~01185d5a4ab8156523)

This repository holds the **real n8n workflow files** behind the case studies, each with a README explaining the architecture, design decisions, error handling and setup. Every workflow can be imported into n8n.

---

## Projects

| # | Project | What it does | Built with |
|---|---|---|---|
| 01 | [**Multi-Agent Customer Support**](01-multi-agent-customer-support/) | Online-store support from a web form and email. A Router delegates to 4 specialist agents, a Critic reviews every draft, risky replies go to a human, and every answer is scored. | n8n · OpenRouter · Groq · Gmail · Google Sheets |
| 02 | [**Restaurant Booking Assistant**](02-restaurant-booking-assistant/) | Telegram voice/text assistant for a Berlin restaurant: bookings, Stripe deposits, allergen-safe menu answers, cancellations, 2-hour reminders and nightly evaluation. **4 workflows.** | n8n · OpenRouter · Groq · Qdrant · ElevenLabs · Stripe · Telegram |
| 03 | [**Voice Assistant with Guardrails**](03-voice-assistant-guardrails/) | Telegram voice assistant for a German retailer. A regex PII guardrail runs before any LLM, a classifier routes to a warehouse agent or an FAQ agent, and EU AI Act Art. 50 disclosure is built in. | n8n · ElevenLabs · Qdrant · Google Sheets · OpenRouter · Groq |
| 04 | [**Structured AI Output Pipeline**](04-structured-ai-output-pipeline/) | One form for screenshots, PDFs and audio. Vision bug triage with schema-guided reasoning, transcription and Map-Reduce summarization, all into structured Sheets rows. | n8n · OpenRouter · Deepgram · Google Drive · Google Sheets |
| 05 | [**AI Recruitment Assistant**](05-ai-recruitment-assistant/) | Resume intake (PDF/OCR → 9 structured fields → Sheets + Pinecone) and semantic candidate search for recruiters on Telegram. **2 workflows.** | n8n · OpenAI embeddings · Pinecone · OpenRouter · Telegram |
| 06 | [**Email Assistant for Freelancers**](06-email-assistant-freelancer/) | Classifies incoming Gmail and drafts replies, books meetings, answers new leads and alerts on urgent mail. A human always presses Send. | n8n · OpenRouter (Claude Haiku) · Gmail · Google Calendar · Telegram |
| 07 | [**Legal Navigator**](07-legal-navigator-guardrails/) | Internal legal assistant grounded in a company handbook. Routes by confidence, asks approval before acting, escalates to a lawyer with a timeout, and feeds approved answers back into the knowledge base. | n8n · Qdrant · OpenRouter · Gmail · Telegram |

---

## Patterns across these projects

| Pattern | Where |
|---|---|
| **Supervisor / multi-agent routing:** a Router delegates to specialist agents used as tools | 01, 02, 03 |
| **Critic loop:** a second agent reviews drafts with a hard retry limit | 01, 02 |
| **Human-in-the-loop:** risky, money-related or low-confidence cases wait for human approval | 01, 02, 06, 07 |
| **Privacy first:** PII is detected and tokenized (or refused) **before** any LLM call and restored only in the final message | 01, 02, 03 |
| **RAG:** vector search over Qdrant or Pinecone, including a self-updating knowledge base | 02, 03, 05, 07 |
| **Evaluation:** an LLM judge scores answers on fixed criteria and logs them | 01, 02 |
| **Structured outputs:** JSON schemas with auto-fixing parsers, so bad JSON doesn't stop a run | 01, 02, 04, 05, 07 |
| **Reliability:** fallback models across providers, retries, error branches, dead-letter logging | all |
| **Voice:** speech-to-text and text-to-speech in Telegram | 02, 03 |

---

## Using these workflows

1. In n8n, go to **Workflows → Import from file** and choose a `.json` file.
2. Create your own credentials (each project's README lists which ones).
3. Replace placeholders such as `YOUR_GOOGLE_SHEET_ID_1`, `YOUR_TELEGRAM_CHAT_ID` and `you@example.com`.

The files are sanitized exports: no API keys, personal IDs or test data. Most prompts and some node names are in Russian, and each README is in English.
