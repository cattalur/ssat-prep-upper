# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

SSAT Prep is a **single-file, no-build web application** for daily SSAT (Secondary School Admission Test) Middle Level verbal practice. It covers synonyms and analogies questions with progress tracking.

## Running the App

No build process or dependencies. Open `index.html` directly in a browser.

## Architecture

Everything lives in `index.html`: HTML structure, embedded CSS, and vanilla JavaScript. No frameworks, no bundler, no package.json.

### Screens (SPA-style via CSS `display` toggling)
- **Home** — dashboard (streak, sessions, avg score, questions seen)
- **Setup** — quiz configuration (type, count, difficulty focus)
- **Quiz** — question presentation with progress bar
- **Results** — score arc, per-question review
- **History** — past session log
- **Vocab** — vocabulary reference bank

### State
- `state` — persistent user data (sessions, weak words, streaks); serialized to `localStorage`
- `quiz` — ephemeral current-session data (questions, index, answers, timer)

### Question Bank
`QUESTIONS` array (~105+ items). Each entry: `{ id, type, stem, choices, answer, difficulty }`. Types are `"synonym"` or `"analogy"`. Difficulty is numeric; weak-area weighting prioritizes words the user has gotten wrong.

### Key Functions
- `startQuiz()` — builds filtered/weighted question list, initializes `quiz` state
- `renderQuestion()` — renders current question and choices
- `selectAnswer()` — validates answer, updates weak-word tracking
- `finishQuiz()` — computes results, appends session to `state.sessions`
- `renderResults()` — draws score arc, renders review list
- `saveState()` / `loadState()` — localStorage persistence
