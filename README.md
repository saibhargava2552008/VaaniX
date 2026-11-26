# VaaniX: Your Language. Your Voice. Your Access.

A voice-first Telugu and Indian English assistant, planned for HackWithAditya 2026 (theme: AI for Bharat).

## Status

Planning only. There is no application code yet, and no API call has been made or tested.

## Planned journey

Choose a language, speak, read the transcript and answer, and hear the answer aloud.
If key information is missing (for example, the scheme name), VaaniX asks instead of guessing.

## Planned stack

| Layer | Choice |
|---|---|
| Frontend | React, Vite, TypeScript, Tailwind CSS |
| Backend | Python, FastAPI, Uvicorn |
| Speech-to-text | Sarvam `saaras:v4` |
| Text-to-speech | Sarvam `bulbul:v4-flash` |
| LLM | **Not decided.** See [docs/architecture.md](docs/architecture.md) |

## Rules

- **₹0 out of pocket.** No billing, no bought credits, no silent switch to a paid service.
- **Mock responses by default.** Real API calls only after explicit team approval.
- **No secrets in Git.** Keys go only in `backend/.env`.
- **Adults only for now.** The MVP is a team-run demo, not a public service (see the architecture document).

## Privacy

Audio and text will be processed by third-party providers. Do not speak or type personal,
medical or financial details. VaaniX will not store recordings by default; providers have
their own retention rules.

## Setup

Run commands will be added when there is code to run.
