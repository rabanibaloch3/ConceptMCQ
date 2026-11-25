# ConceptMCQ

A **concept-first exam preparation system**. Instead of memorising questions, you organise what you study — subjects, topics, and your own notes — and ConceptMCQ turns that into practice: manual and AI-generated MCQs, instant feedback with explanations, a "Practice Again" set built from your mistakes, full tests, and analytics that show your weak topics.

Built for my own competitive-exam and Computer Science preparation, and designed to work for any subject.

## Features

- **Subjects & hierarchical topics** — create subjects (e.g. Computer Networks, Operating Systems) with parent–child topic trees, and paste or write study content per topic
- **Manual MCQs** — add your own questions per topic with options, correct answer, explanation and difficulty
- **AI-generated MCQs** — generate questions from a topic's content or for a whole subject, choosing the provider, count (5–20) and difficulty. Questions are written to test *why* and *how*, not definitions
- **Multi-provider AI** — Google Gemini and Groq (free) and OpenAI (paid), with the generating provider tracked and badged on every question
- **Practice Again** — every wrong answer is automatically collected into a mistakes set, organised by subject and topic, so revision targets exactly what you got wrong
- **Tests** — generate a test from all topics of a subject with configurable question count and difficulty
- **Analytics** — overall accuracy, per-subject stats, and a weak-topics view (Recharts)
- **Accounts** — JWT authentication with hashed passwords; every user's subjects, attempts and progress are their own

## Tech stack

**Frontend:** React 18, TypeScript, Vite, Tailwind CSS, shadcn/ui, React Router, Zustand, Axios, Recharts
**Backend:** Node.js, Express, TypeScript, PostgreSQL, Prisma ORM, JWT + bcrypt

## Data model (Prisma)

- `User` — account, owns subjects and attempts
- `Subject` — a study subject belonging to a user
- `Topic` — hierarchical (parent/child), holds study content and completion status
- `MCQ` — question with 4 options, correct answer, explanation, difficulty, and AI-generation fields (`isAIGenerated`, `aiProvider`)
- `UserAttempt` — each answer a user submits, used for accuracy, Practice Again and weak-topic analytics

## API overview

- `/api/auth` — register, login (JWT), current user
- `/api/subjects` and `/api/subjects/:id/topics` — subject and topic CRUD (hierarchical)
- `/api/topics/:topicId/mcqs` — MCQ CRUD, plus AI generation per topic or per subject
- `/api/mcqs/:mcqId/attempt` — submit an answer, get instant correctness + explanation
- `/api/practice-again` — wrong-answer sets, overall or per subject
- `/api/subjects/:subjectId/test` — generate a test
- `/api/analytics` — overview, per-subject stats, weak topics

## Project status

Designed and built in February 2026 (spec-driven development: the full design — data model, API and screens — was written first, then implemented). The working app currently lives in my Replit workspace; this repository hosts the project showcase and design documentation, and the source code is being migrated here.

## Author

**Ghulam Rabbani** — BS Computer Science, University of Balochistan
[LinkedIn](https://www.linkedin.com/in/ghulam-rabbani-85938bb1) · TechForSeed.com
