# ConceptMCQ — Design Specification

*Written February 2026, before implementation. This is the specification the app was built from.*

## Concept

A study platform where the learner organises knowledge first — subjects, then hierarchical topics, then content — and the system generates practice from that structure. Wrong answers feed a "Practice Again" loop, and analytics expose weak topics.

## Screens

- **Login / Register** — email, password, name; JWT stored client-side
- **Dashboard** — subject cards (topic count, completion %, accuracy), quick stats (attempted MCQs, overall accuracy, Practice Again count), create-subject action
- **Subject page** — expandable topic tree with completion status and MCQ counts, progress bar, add-topic and Create Test actions
- **Topic page** — breadcrumbs; tabs for Content (rich text, mark-complete), MCQs (answer in place, instant feedback with explanation) and Add MCQ (question, 4 options, correct answer, explanation, difficulty)
- **Test page** — a generated test across all topics of a subject
- **Generated MCQs / Review Mistakes** — AI-generated questions and wrong answers, both organised by subject hierarchy
- **Analytics** — overview, per-subject accuracy, weak topics

## AI MCQ generation requirements

1. Generate for a single topic (from its content) or for an entire subject
2. Providers: Google Gemini (free), Groq (free), OpenAI (paid) — user selects provider, count (5–20) and difficulty
3. Questions must test deep understanding: "why/how" and scenario-based, with plausible distractors and a 2–3 sentence explanation each
4. Difficulty mix guideline: ~40% easy, ~40% medium, ~20% hard
5. Every generated MCQ records which provider created it, shown with a badge

## Key behaviours

- Submitting an answer returns correctness and the explanation immediately, and records a UserAttempt
- Incorrectly answered MCQs appear automatically in Practice Again
- Tests sample randomly across a subject's topics, optionally restricted to previously-wrong questions
