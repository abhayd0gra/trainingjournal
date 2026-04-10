# Training Journal — Personal Fitness & Nutrition Accountability Tracker

**Live app:** [abhayd0gra.github.io/trainingjournal](https://abhayd0gra.github.io/trainingjournal)

---

## Why

At 31, with a body scan showing 65.7 lbs of skeletal muscle mass and a target of 78 lbs, the gap between where I am and where I want to be is measurable. The problem was never motivation - it was the absence of a system. Without tracking, training sessions blur together, protein targets get missed by guesswork, and progress is invisible until it's too late to course-correct.

Most fitness apps are either too generic, too cluttered, or built for someone else's goals. I wanted something built around my exact numbers, my exact schedule, and my exact meals. Something that would tell me, at the end of every day, whether I did the work or not - without softening the verdict.

This is that tool.

---

## How

Built entirely as a single HTML file using vanilla JavaScript, no frameworks, no build pipeline. Designed to be fast, portable, and fully owned - no third-party fitness platform controlling your data or monetizing your activity.

**Tech stack:**
- HTML, CSS, vanilla JavaScript
- Google Drive API (appDataFolder) for cross-device data sync
- Google Identity Services for OAuth 2.0 authentication
- Anthropic Claude API for AI coaching
- GitHub Pages for hosting

**Data storage:** All training data is saved to a private JSON file in your Google Drive appDataFolder - invisible to other apps, private to your account, and accessible from any device you authorize. localStorage serves as a fallback and offline cache.

**AI coaching:** The daily and weekly review features call the Anthropic API directly from the browser, passing a complete snapshot of that day's exercise, nutrition, and hydration data. The coach reads everything across all tabs before generating an assessment.

---

## What

A 4-tab web application accessible from any device at a permanent URL.

### Exercise Tab
- 7-day training schedule: Push / Pull + Deadlift / Rest + Mobility / Legs / Upper Body / Run + Mobility / Swim + Mobility
- Pre-loaded exercise lists for each strength day (8 exercises per session, the research-backed ceiling for hypertrophy volume per session)
- Weight, sets, and reps logging per exercise
- Progressive overload indicator: compares each session against the previous session of the same type and flags whether you went up in weight, volume, or held the same
- Add, remove, and rename exercises with confirmation dialogs
- Reset to defaults option if you want to restore the original list
- Run tracking: distance (miles), pace (min/mile), duration, heart rate, elevation gain, RPE, notes - with a session history table showing distance deltas across sessions
- Swim tracking: distance (meters), pace (min/100m), duration, stroke, laps, RPE, notes - with session history
- Mobility drill lists for Rest day, post-Run, and post-Swim sessions

### Nutrition Tab
- Daily protein tracker with a 150g target
- Four pre-loaded meals matching my actual eating habits: breakfast, lunch, post-training snack, dinner - each with protein estimates
- One-tap meal logging
- Edit any meal for days you ate differently, with custom protein entry
- Extra protein items section for anything outside the four main meals (boiled eggs, Greek yogurt, protein shake)
- Live progress bar and running total updating as you log

### Hydration Tab
- Bottle-based logging (710ml per bottle, matching my actual water bottle)
- Training day toggle that adjusts the target from 3,000ml to 3,550ml
- Visual fill indicators and percentage tracker

### AI Coach Tab
- Daily Review: reads all logged data across exercise, nutrition, and hydration and generates a 4-sentence direct assessment covering what went well, the biggest gap, a specific fix for tomorrow, and a longer-term observation
- Weekly Review: synthesizes the full week across all sessions, protein averages, and cardio data into three sections - what went well, what fell short, and specific improvements for next week
- Powered by Anthropic Claude API (requires your own API key, stored locally in your browser)

---

## Personal Goals

| Metric | Current | Target | Timeline |
|---|---|---|---|
| Skeletal Muscle Mass | 65.7 lbs | 78 lbs | 9–12 months |
| Body Fat % | 17.6% | ~14.6% | 9–12 months |
| Daily Protein | ~80g | 150g | Immediate |
| Training Days/Week | 3 | 4 strength + run + swim | Now |

---

## Setup

The app is live and requires no installation. To run your own version:

1. Fork this repository
2. Enable GitHub Pages (Settings → Pages → Deploy from main branch)
3. Create a Google Cloud project, enable the Drive API, and create an OAuth 2.0 Web Client ID with your GitHub Pages URL as an authorized origin
4. Replace the `GOOGLE_CLIENT_ID` constant in `index.html` with your own Client ID
5. Get an Anthropic API key from [console.anthropic.com](https://console.anthropic.com) and enter it in the AI Coach tab on first use

---

## What I Learned Building This

This project was built in a single evening working with Claude as a coding partner. The process involved:

- Iterating from an in-browser artifact to a standalone HTML file to a hosted webapp
- Debugging JavaScript JSON serialization edge cases (numeric object keys becoming strings after JSON round-trips)
- Setting up Google OAuth and Drive API from scratch, including OAuth consent screen configuration and appDataFolder scoping
- Applying performance review feedback and distinguishing between genuinely impactful optimizations and premature ones at this scale
- Deploying to GitHub Pages and managing the full release cycle from local testing to live URL

The most valuable thing was learning to treat AI as a thinking partner on technical decisions, not just a code generator - pushing back on suggestions, asking for honest assessments of tradeoffs, and building something that actually fits my specific needs rather than a generic template.
