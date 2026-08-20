# 🤖 Meet AI — Intelligent Video Meetings

<p align="center">
  <strong>AI-powered video meetings with real-time agents, automatic summaries, searchable transcripts, and contextual AI assistance.</strong>
</p>

<p align="center">
  <a href="#-features">Features</a> •
  <a href="#-architecture">Architecture</a> •
  <a href="#-tech-stack">Tech Stack</a> •
  <a href="#-getting-started">Getting Started</a> •
  <a href="#-roadmap">Roadmap</a>
</p>

<p align="center">

![Next.js](https://img.shields.io/badge/Next.js-15-black?style=for-the-badge\&logo=next.js)
![React](https://img.shields.io/badge/React-19-61DAFB?style=for-the-badge\&logo=react)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=for-the-badge\&logo=typescript)
![OpenAI](https://img.shields.io/badge/OpenAI-API-black?style=for-the-badge\&logo=openai)
![Stream](https://img.shields.io/badge/Stream-Video%20%26%20Chat-005FFF?style=for-the-badge)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=for-the-badge\&logo=postgresql)

</p>

---

## 🌐 Overview

**Meet AI** is a full-stack AI-powered video conferencing platform that combines real-time communication with intelligent meeting automation.

Users can create meetings, invite custom AI agents into live video calls, communicate through real-time video and chat, and automatically turn completed meetings into searchable knowledge.

After a meeting ends, Meet AI processes the conversation in the background and provides:

* 📝 AI-generated transcripts
* 🧠 Intelligent meeting summaries
* 🔍 Searchable transcript content
* 📺 Meeting recording playback
* 💬 Context-aware AI Q&A
* 📂 Persistent meeting history

The goal is simple:

> **Don't just record meetings. Make them useful after they're over.**

---


## ✨ Features

### 🤖 Real-Time AI Agents

Create custom AI agents that can participate directly in live video meetings.

Agents are connected to the real-time meeting infrastructure and powered by OpenAI to understand and respond to participants.

**Highlights:**

* Custom AI agents
* Agent configuration
* Real-time participation
* OpenAI-powered responses
* Agent-to-meeting association

---

### 📹 Real-Time Video Calls

Meet AI uses **Stream Video** to provide reliable real-time communication.

Users can:

* Join video meetings
* Enable/disable camera
* Enable/disable microphone
* Interact with participants
* Invite AI agents
* Use real-time meeting controls

---

### 💬 Real-Time Chat

Meetings include real-time messaging powered by **Stream Chat**.

Participants can communicate without leaving the meeting experience.

---

### 📝 Automatic Transcripts

After a meeting finishes, the conversation can be processed into a structured transcript.

This makes previously recorded meetings much easier to revisit.

Instead of watching an entire one-hour recording, users can quickly search for the information they need.

---

### 🧠 AI-Generated Summaries

Meet AI automatically generates concise meeting summaries using OpenAI.

The summary can help users quickly understand:

* What was discussed
* Important decisions
* Key topics
* Important context
* Potential follow-ups

---

### 🔍 Smart Transcript Search

Long meetings become searchable knowledge.

Users can search transcripts for:

```text
authentication
subscriptions
database
deployment
API
action items
```

This allows users to jump directly to relevant parts of a conversation.

---

### 📺 Meeting Recording & Playback

Completed meetings can be revisited through the meeting history.

Users can:

* View meeting information
* Watch recordings
* Read transcripts
* Review summaries
* Search transcript content
* Ask AI questions

---

### 💬 Post-Meeting AI Assistant

The most powerful part of the application is the contextual AI experience after the meeting.

Instead of asking a generic chatbot, users can ask questions about the **specific meeting**.

Example:

```text
User:
What were the main decisions made during this meeting?

AI:
The team agreed to migrate the authentication
system to Better Auth and move background
processing to Inngest.
```

Another example:

```text
User:
Who was responsible for the authentication work?

AI:
The authentication implementation was assigned
to the backend team.
```

The assistant uses the meeting context to provide relevant answers.

---

## 🏗️ Architecture

Meet AI is built around a combination of real-time infrastructure, a type-safe backend, persistent storage, AI services, and asynchronous background processing.

```text
                              ┌──────────────────┐
                              │      Client      │
                              │ Next.js / React  │
                              └────────┬─────────┘
                                       │
                    ┌──────────────────┼──────────────────┐
                    │                  │                  │
                    ▼                  ▼                  ▼
              ┌───────────┐     ┌─────────────┐    ┌─────────────┐
              │   tRPC    │     │ Stream      │    │ Better Auth │
              │   API     │     │ Video/Chat  │    │             │
              └─────┬─────┘     └──────┬──────┘    └─────────────┘
                    │                  │
                    ▼                  ▼
              ┌───────────┐      ┌─────────────┐
              │  Drizzle  │      │ AI Agents   │
              │    ORM    │      │  + OpenAI   │
              └─────┬─────┘      └─────────────┘
                    │
                    ▼
              ┌─────────────┐
              │    Neon     │
              │ PostgreSQL  │
              └──────┬──────┘
                     │
                     ▼
              ┌─────────────┐
              │   Inngest   │
              │ Background  │
              │    Jobs     │
              └──────┬──────┘
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
     Transcript   Summary    AI Context
          │          │          │
          └──────────┼──────────┘
                     ▼
              ┌─────────────┐
              │ Post-Call   │
              │ AI Q&A      │
              └─────────────┘
```

---

## 🔄 Meeting Lifecycle

The application follows a multi-stage meeting lifecycle.

```text
Create Meeting
      │
      ▼
Configure AI Agent
      │
      ▼
Start Meeting
      │
      ▼
Stream Video Call
      │
      ├───────────────┐
      │               │
      ▼               ▼
Participants      AI Agent
      │               │
      └───────┬───────┘
              ▼
        Meeting Ends
              │
              ▼
          Inngest Job
              │
      ┌───────┼────────┐
      ▼       ▼        ▼
 Transcript Summary Recording
      │       │        │
      └───────┼────────┘
              ▼
       Meeting History
              │
     ┌────────┼─────────┐
     ▼        ▼         ▼
   Search  Playback   AI Q&A
```

---

## 🧠 AI Pipeline

The AI functionality is divided into multiple stages.

### During the meeting

```text
Participant
     │
     ▼
 Stream Video
     │
     ▼
 AI Agent
     │
     ▼
   OpenAI
     │
     ▼
 Real-time Response
```

### After the meeting

```text
Meeting Completed
        │
        ▼
     Inngest
        │
        ├── Process meeting data
        │
        ├── Generate transcript
        │
        ├── Generate summary
        │
        └── Prepare meeting context
                     │
                     ▼
                AI Assistant
```

This separation allows real-time functionality and expensive post-processing tasks to operate independently.

---

# 🛠️ Tech Stack

## Frontend

| Technology          | Usage                      |
| ------------------- | -------------------------- |
| **Next.js 15**      | Full-stack React framework |
| **React 19**        | UI development             |
| **TypeScript**      | Type safety                |
| **Tailwind CSS v4** | Styling                    |
| **shadcn/ui**       | Reusable UI components     |

## Backend

| Technology      | Usage                     |
| --------------- | ------------------------- |
| **tRPC**        | End-to-end type-safe APIs |
| **Drizzle ORM** | Database access           |
| **Neon**        | Serverless PostgreSQL     |
| **Inngest**     | Background jobs           |

## AI & Communication

| Technology       | Usage                      |
| ---------------- | -------------------------- |
| **OpenAI**       | AI agents, summaries & Q&A |
| **Stream Video** | Real-time video            |
| **Stream Chat**  | Real-time messaging        |

## Authentication & Payments

| Technology      | Usage                   |
| --------------- | ----------------------- |
| **Better Auth** | Authentication          |
| **Polar**       | Subscription management |

---

# 🔐 Authentication

Authentication is handled through **Better Auth**.

The application supports authenticated user sessions and protects resources belonging to individual users.

User-specific resources include:

```text
User
 ├── AI Agents
 ├── Meetings
 ├── Transcripts
 ├── Recordings
 └── Meeting Conversations
```

---

# 💳 Subscription System

Meet AI integrates **Polar** for subscription and payment management.

The subscription architecture is designed around:

```text
User
 │
 ▼
Subscription
 │
 ▼
Polar
 │
 ▼
Webhook
 │
 ▼
Application
 │
 ▼
Update Subscription State
```

This allows subscription events to be synchronized with the application.

---

# ⚙️ Background Jobs

Not every operation should happen during a user's request.

Meet AI uses **Inngest** for asynchronous workflows such as:

* Meeting processing
* Transcript generation
* AI summaries
* Post-call processing
* External service synchronization

Example:

```text
Request
  │
  ▼
Meeting Completed
  │
  ▼
Queue Background Job
  │
  ▼
Return Response
  │
  └──────────────► Inngest
                       │
                       ├── Transcript
                       ├── Summary
                       └── AI Context
```

This keeps the user-facing application responsive while heavier operations run independently.

---

# 🗄️ Data Layer

The application uses:

**Neon PostgreSQL + Drizzle ORM**

Drizzle provides a strongly typed interface between the application and database.

Conceptually, the data model revolves around:

```text
User
 │
 ├── Agents
 │
 └── Meetings
       │
       ├── Participants
       ├── Transcript
       ├── Summary
       ├── Recording
       └── AI Conversations
```

---

# 📂 Project Structure

```text
.
├── public/
│   └── screenshots/
│
├── src/
│   ├── app/
│   │   ├── (auth)/
│   │   ├── (dashboard)/
│   │   └── api/
│   │
│   ├── components/
│   │   ├── ui/
│   │   └── ...
│   │
│   ├── db/
│   │   └── ...
│   │
│   ├── modules/
│   │   ├── agents/
│   │   ├── meetings/
│   │   └── ...
│   │
│   ├── trpc/
│   │   └── ...
│   │
│   └── lib/
│       └── ...
│
├── .env.example
├── drizzle.config.ts
├── next.config.ts
├── package.json
└── README.md
```

---

# 🚀 Getting Started

## Prerequisites

Make sure you have:

* Node.js 18+
* npm
* Git

You will also need accounts/API keys for the external services used by the application.

---

## 1. Clone the Repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>

cd <YOUR_PROJECT_DIRECTORY>
```

---

## 2. Install Dependencies

Because this project uses React 19:

```bash
npm install --legacy-peer-deps
```

---

## 3. Configure Environment Variables

Create your local environment file:

```bash
cp .env.example .env.local
```

Then configure the required environment variables.

The project integrates with:

```text
Neon
Better Auth
OpenAI
Stream
Inngest
Polar
ngrok
```

> ⚠️ Never commit `.env.local` or expose API keys in your repository.

---

## 4. Setup Database

Push the database schema:

```bash
npm run db:push
```

Open Drizzle Studio:

```bash
npm run db:studio
```

---

## 5. Start the Development Server

```bash
npm run dev
```

Open:

```text
http://localhost:3000
```

---

## 6. Start Inngest

Open another terminal:

```bash
npx inngest-cli@latest dev
```

This starts the local Inngest development environment.

---

## 7. Configure Webhooks

Some services require a publicly accessible webhook URL during development.

Configure your ngrok static domain inside `package.json`:

```json
{
  "scripts": {
    "dev:webhook": "ngrok http --url=YOUR_NGROK_STATIC_DOMAIN 3000"
  }
}
```

Then run:

```bash
npm run dev:webhook
```

---

# 📜 Available Scripts

### Development

```bash
npm run dev
```

Start the Next.js development server.

```bash
npm run dev:webhook
```

Start the ngrok webhook tunnel.

```bash
npx inngest-cli@latest dev
```

Start the Inngest development server.

### Database

```bash
npm run db:push
```

Push schema changes to the database.

```bash
npm run db:studio
```

Open Drizzle Studio.

### Production

```bash
npm run build
```

Build the application for production.

```bash
npm run start
```

Start the production server.

---

# 📱 Responsive Experience

Meet AI is designed to work across different screen sizes.

The application includes responsive layouts for:

* Dashboard
* Navigation
* Forms
* Dialogs
* Agent management
* Meeting management
* Meeting pages
* Post-meeting experience

---

# 🧪 Development Workflow

The project was developed around a feature-driven workflow.

Major development milestones included:

```text
Project Setup
      │
      ▼
Database
      │
      ▼
Authentication
      │
      ▼
Dashboard
      │
      ▼
tRPC
      │
      ▼
AI Agents
      │
      ▼
Meetings
      │
      ▼
Stream Video
      │
      ▼
AI Agent Integration
      │
      ▼
Background Jobs
      │
      ▼
Transcripts
      │
      ▼
Summaries
      │
      ▼
Post-Meeting AI
      │
      ▼
Subscriptions
      │
      ▼
Polish & Bug Fixes
```

---

# 🧑‍💻 What This Project Demonstrates

This project goes beyond a simple CRUD application.

It demonstrates experience with:

### Full-Stack Development

* Next.js App Router
* Server/client architecture
* Type-safe APIs
* Database design
* Authentication
* Authorization
* External API integrations

### Real-Time Systems

* Real-time video
* Real-time chat
* AI agents inside live calls
* Webhooks
* Event-driven workflows

### AI Engineering

* OpenAI API integration
* Real-time AI interaction
* Context-aware AI
* Meeting summarization
* Transcript processing
* AI-powered question answering

### Backend Architecture

* PostgreSQL
* Drizzle ORM
* tRPC
* Background jobs
* Webhook processing
* Asynchronous workflows

### SaaS Development

* Authentication
* User-specific data
* Subscriptions
* Payment events
* Responsive dashboard
* Production-oriented architecture

---

# 📚 Key Learnings

Building Meet AI helped me understand how multiple modern systems can work together inside a single production-style application.

Some of the biggest takeaways were:

* Designing scalable full-stack applications with Next.js
* Working with real-time video infrastructure
* Integrating AI into real-time workflows
* Building asynchronous background processing
* Handling webhooks from third-party services
* Designing relational data models
* Building contextual AI experiences
* Managing authentication and subscriptions
* Structuring larger React applications
* Creating responsive SaaS interfaces
* Debugging integrations across multiple external services

---

# 🗺️ Roadmap

Meet AI can be extended with additional collaboration and intelligence features.

### Planned Improvements

* [ ] Calendar integration
* [ ] Meeting scheduling
* [ ] Email notifications
* [ ] AI-generated action items
* [ ] Automatic task extraction
* [ ] Meeting sentiment analysis
* [ ] Speaker analytics
* [ ] Team workspaces
* [ ] Organization accounts
* [ ] Role-based permissions
* [ ] Meeting exports
* [ ] Advanced semantic transcript search
* [ ] Custom AI agent personalities
* [ ] More OAuth providers
* [ ] Improved analytics and observability

---

# 🔒 Security Notes

Never expose the following publicly:

* API keys
* Database credentials
* Authentication secrets
* Stream credentials
* OpenAI credentials
* Polar credentials
* Webhook signing secrets

Use environment variables for all sensitive configuration.

```text
.env.local
```

should remain local and should **never be committed**.

---



# 👨‍💻 Author

## Palak Upadhyay

Full-stack developer interested in building modern web applications, AI-powered products.




  Built with ❤️ using Next.js, React, TypeScript, OpenAI, Stream, Neon, Drizzle, Inngest, Better Auth & Polar.
</p>
