<div align="center">

<!-- HERO BANNER — reliable GitHub raw asset -->
<img src="https://i.imgur.com/waxVImv.png" alt="separator" width="100%"/>

<!-- BOT GIF — hosted on Giphy (publicly accessible, no login required) -->
<img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExbzRsNXV3NXd4Z3FtNm85NmZiZzlhcGlvazVmN2VxMGh4ajY1dWVrZSZlcD12MV9pbnRlcm5hbGdfZ2lmX2J5X2lkJmN0PWc/3oKIPnAiaMCws8nOsE/giphy.gif" alt="Bot in action" width="220"/>

<h1>🤖 Discord Moderation Bot</h1>

<p><em>A production-grade, slash-command-driven Discord bot for automated server moderation, anti-spam enforcement, and audit logging — deployed on Railway with continuous uptime.</em></p>

<!-- BADGES — all from shields.io, 100% reliable -->
<p>
  <img src="https://img.shields.io/badge/version-1.0.0-5a6340?style=flat-square" alt="version"/>
  <img src="https://img.shields.io/badge/node-%3E%3D18.x-339933?style=flat-square&logo=node.js&logoColor=white" alt="node"/>
  <img src="https://img.shields.io/badge/discord.js-v14-5865F2?style=flat-square&logo=discord&logoColor=white" alt="discord.js"/>
  <img src="https://img.shields.io/badge/MongoDB-connected-47A248?style=flat-square&logo=mongodb&logoColor=white" alt="mongodb"/>
  <img src="https://img.shields.io/badge/deploy-Railway-0B0D0E?style=flat-square&logo=railway&logoColor=white" alt="railway"/>
  <img src="https://img.shields.io/badge/license-MIT-c4a97d?style=flat-square" alt="license"/>
  <img src="https://img.shields.io/badge/status-production-22c55e?style=flat-square" alt="status"/>
</p>

<img src="https://i.imgur.com/waxVImv.png" alt="separator" width="100%"/>

</div>

<br/>

## 📑 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Slash Commands](#-slash-commands)
- [Deployment](#-deployment-railway)
- [Database Schema](#-database-schema)
- [Author](#-author)
- [License](#-license)

---

## 🧭 Overview

This bot was built to **completely eliminate manual server moderation** overhead on Discord. It uses Discord.js v14 slash commands, persists every infraction and audit event to **MongoDB**, and is deployed with **continuous uptime on Railway** — no babysitting required.

> Built and maintained by **Mohamed Siddiq N** — Full-Stack Developer  
> 📍 Tiruchirappalli, India &nbsp;|&nbsp; 📧 mohamedsiddiq7504@gmail.com

<div align="center">
  <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExbzc4dGJ2NXM5NmZiZzlhcGlvazVmN2VxMGh4ajY1dWVrZSZlcD12MV9pbnRlcm5hbGdfZ2lmX2J5X2lkJmN0PWc/du3J3cXyzhj75IOgvA/giphy.gif" width="160" alt="robot working"/>
</div>

---

## ✨ Features

- ⚡ **Slash Commands** — All commands use Discord's native `/command` interface, no prefix needed
- 🛡️ **Anti-Spam Detection** — Automatically detects and mutes repeat message spammers
- 🚫 **Bad Word Filter** — Customizable inappropriate language detection with auto-deletion
- 📋 **Infraction Logging** — Every warn, mute, kick, and ban is logged to MongoDB with timestamps
- 📊 **Audit Trail** — Full audit history queryable per user
- 🔔 **DM Notifications** — Users are privately notified when actioned
- 🔄 **Railway Deploy** — Continuous uptime with zero manual restarts
- 🧩 **Modular Command Handler** — Easy to add new commands without touching core logic

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| Runtime | Node.js ≥ 18.x |
| Bot Framework | Discord.js v14 |
| Database | MongoDB (Mongoose ODM) |
| Deployment | Railway |
| Language | JavaScript (ES6+) |
| Dev Tools | Git, VS Code, Nodemon |

---

## 📁 Project Structure

```
discord-mod-bot/
├── src/
│   ├── commands/
│   │   ├── moderation/
│   │   │   ├── ban.js
│   │   │   ├── kick.js
│   │   │   ├── mute.js
│   │   │   ├── warn.js
│   │   │   └── infractions.js
│   │   └── utility/
│   │       ├── ping.js
│   │       └── help.js
│   ├── events/
│   │   ├── ready.js
│   │   ├── messageCreate.js
│   │   └── interactionCreate.js
│   ├── models/
│   │   └── Infraction.js
│   └── utils/
│       ├── commandHandler.js
│       ├── spamDetector.js
│       └── logger.js
├── deploy-commands.js
├── index.js
├── .env.example
├── package.json
└── README.md
```

---

## ✅ Prerequisites

Before you begin, make sure you have the following:

- **Node.js** `>= 18.x` — [Download](https://nodejs.org/)
- **MongoDB** URI (Atlas free tier works) — [Get one](https://cloud.mongodb.com/)
- **Discord Bot Token** — [Discord Developer Portal](https://discord.com/developers/applications)
- **Railway account** (for deployment) — [railway.app](https://railway.app/)

---

## ⚙️ Installation

**1. Clone the repository**

```bash
git clone https://github.com/Siddiq0075/discord-mod-bot.git
cd discord-mod-bot
```

**2. Install dependencies**

```bash
npm install
```

**3. Set up environment variables**

```bash
cp .env.example .env
```

Open `.env` and fill in your values (see [Configuration](#-configuration) below).

**4. Register slash commands with Discord**

```bash
node deploy-commands.js
```

> ⚠️ You only need to run this once, or whenever you add/modify commands.

**5. Start the bot**

```bash
# Development (with auto-restart)
npm run dev

# Production
npm start
```

---

## 🔧 Configuration

Create a `.env` file in the root directory based on `.env.example`:

```env
# ─── Discord ──────────────────────────────────────
DISCORD_TOKEN=your_bot_token_here
CLIENT_ID=your_application_client_id
GUILD_ID=your_test_server_id          # Only for dev guild-scoped commands

# ─── MongoDB ──────────────────────────────────────
MONGO_URI=mongodb+srv://<user>:<password>@cluster.mongodb.net/modbot

# ─── Bot Settings ─────────────────────────────────
LOG_CHANNEL_ID=your_audit_log_channel_id
SPAM_THRESHOLD=5                       # Messages per 5 seconds before mute
MUTE_DURATION_MINUTES=10              # Default auto-mute duration
```

> 🔒 **Never commit your `.env` file.** It is already in `.gitignore`.

---

## 💬 Slash Commands

### Moderation

| Command | Description | Required Permission |
|---|---|---|
| `/warn @user [reason]` | Issues a warning and logs to DB | Moderator |
| `/mute @user [duration] [reason]` | Mutes a user for a set duration | Moderator |
| `/unmute @user` | Removes mute from a user | Moderator |
| `/kick @user [reason]` | Kicks a user from the server | Moderator |
| `/ban @user [reason]` | Bans a user permanently | Administrator |
| `/infractions @user` | Shows full infraction history | Moderator |
| `/clearinfractions @user` | Clears all infractions for a user | Administrator |

### Utility

| Command | Description | Required Permission |
|---|---|---|
| `/ping` | Returns bot latency and API response time | Everyone |
| `/help` | Lists all available commands | Everyone |

### Example Usage

```
/warn @spammer123 Sending repeated promotional messages
/mute @user42 duration:30 reason:Inappropriate language
/infractions @user42
```

---

## 🚀 Deployment — Railway

This bot is production-deployed on [Railway](https://railway.app/) with continuous uptime.

**Step 1 — Push to GitHub**

```bash
git add .
git commit -m "feat: initial bot setup"
git push origin main
```

**Step 2 — Create Railway project**

1. Go to [railway.app](https://railway.app/) → **New Project**
2. Select **Deploy from GitHub repo**
3. Choose your repository

**Step 3 — Add environment variables**

In your Railway project dashboard → **Variables** → add all keys from your `.env` file.

**Step 4 — Set start command**

In Railway → **Settings** → **Deploy** → set:

```
node index.js
```

**Step 5 — Deploy**

Railway auto-deploys on every push to `main`. Your bot will be live within ~60 seconds.

> ✅ Railway provides free restarts on crashes and persistent uptime without a credit card for hobby projects.

---

## 🗄 Database Schema

Infractions are stored in MongoDB using Mongoose:

```js
// src/models/Infraction.js

const mongoose = require('mongoose');

const InfractionSchema = new mongoose.Schema({
  userId:    { type: String, required: true },
  guildId:   { type: String, required: true },
  type:      { type: String, enum: ['warn', 'mute', 'kick', 'ban'], required: true },
  reason:    { type: String, default: 'No reason provided' },
  moderator: { type: String, required: true },
  timestamp: { type: Date,   default: Date.now },
});

module.exports = mongoose.model('Infraction', InfractionSchema);
```

---

## 👤 Author

<div align="center">

**Mohamed Siddiq N**

*Full-Stack Developer — MERN · Python · Bot Automation*

[![Email](https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:mohamedsiddiq7504@gmail.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/siddiq75)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Siddiq0075)
[![Discord](https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.com/users/Siddiq0075)

📍 Tiruchirappalli, Tamil Nadu, India

</div>

---

## 📄 License

```
MIT License

Copyright (c) 2025 Mohamed Siddiq N

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND.
```

---

<div align="center">

<img src="https://i.imgur.com/waxVImv.png" alt="separator" width="100%"/>

*Built with ❤️ by Mohamed Siddiq N &nbsp;·&nbsp; Tiruchirappalli, India*

⭐ **Star this repo if it helped you!**

<img src="https://i.imgur.com/waxVImv.png" alt="separator" width="100%"/>

</div>
