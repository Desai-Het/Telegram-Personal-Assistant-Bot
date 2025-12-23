# Telegram Personal Assistant Bot 🤖📅

An **n8n-powered Telegram bot** that lets you manage **Google Tasks** and **Google Calendar** using **natural language chat**.  
You can talk to the bot like a human, and it will fetch tasks, create calendar events, or read schedules for you.

This project consists of **two n8n workflows that work together**.

---

## 📂 Workflow Files

| File | Purpose |
|----|----|
| `n8nTelegramAgent.json` | Main Telegram bot workflow (handles chat, voice, tasks) |
| `n8nTelegramAgentCalendarAccess.json` | Sub-workflow for Google Calendar access |

---

## 🧠 How the System Works (High Level)
Telegram User
↓
Telegram Bot
↓
Main Workflow (n8nTelegramAgent.json)
├─ Handles text & voice
├─ Uses AI Agent
├─ Accesses Google Tasks
└─ Calls Calendar Workflow when needed
↓
Calendar Workflow (n8nTelegramAgentCalendarAccess.json)
└─ Reads / Creates Google Calendar events


---

## ✨ Features

- Chat with a Telegram bot using **natural language**
- Create and read **Google Calendar events**
- View **pending and completed Google Tasks**
- Supports **text and voice messages**
- Maintains short-term conversation memory
- Fully built using **n8n + OpenAI + Google APIs**

---

## 👤 How Public Users Can Use the Bot

Once **you deploy and activate** the workflows:

1. Share your **Telegram bot username**  
https://t.me/YourBotUsername

2. User opens the chat and sends:
/Start

3. Users can now send messages like:
- *“What tasks do I have today?”*
- *“Create a calendar event tomorrow at 5 PM”*
- *“What meetings do I have this week?”*

⚠️ Users **do not need n8n access** — only Telegram.

---

## 🛠️ Setup Instructions (For Repository Users)

### 1️⃣ Import Workflows into n8n

- Open n8n
- Import:
- `n8nTelegramAgent.json`
- `n8nTelegramAgentCalendarAccess.json`

---

### 2️⃣ Create Required Credentials in n8n

You **must configure these credentials yourself**:

| Service | Credential Type |
|----|----|
Telegram | Telegram Bot API |
OpenAI | OpenAI API |
Google Tasks | Google OAuth2 |
Google Calendar | Google OAuth2 |

---

### 3️⃣ What You MUST Change in the JSON Files

After importing, update the following **inside n8n UI** (not manually in code):

#### 🔐 Credentials
Replace all placeholder credentials with your own:
- Telegram account
- OpenAI API
- Google Tasks OAuth
- Google Calendar OAuth

#### 📧 Calendar Email
In `n8nTelegramAgentCalendarAccess.json`:

```text
"calendar": "your-email@example.com"
4️⃣ Connect the Workflows
In n8nTelegramAgent.json:
Ensure the AI Agent calls the Calendar workflow
The Calendar workflow must be saved and enabled

5️⃣ Activate Workflows (IMPORTANT)
Activate both workflows
The Telegram Trigger only works when active

🎙️ Voice Message Support
Voice messages are downloaded from Telegram
Converted to text using Google Speech-to-Text
Transcript is passed to the AI Agent automatically

🔐 Security Notes
❌ Do NOT commit real API keys
❌ Do NOT commit OAuth tokens
Credentials are stored safely inside n8n
JSON files are safe to share once sanitized

🧪 Recommended Testing
Test with text messages first
Then test voice messages
Try:
Reading tasks
Creating calendar events
Asking follow-up questions

📌 Limitations
Uses short-term memory (last few messages)
Designed for personal use
No multi-user calendar isolation by default

🚀 Tech Stack
n8n
Telegram Bot API
OpenAI (Chat Models)
Google Tasks API
Google Calendar API
