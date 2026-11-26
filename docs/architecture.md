# VaaniX architecture (proposed, not yet built)

Facts checked on 25 November 2026. Re-check before integration.

## Flow

    React (MediaRecorder, max 25 s)
      -> FastAPI
      -> Sarvam saaras:v4      (transcript, language)
      -> LLM provider          (simple answer or clarification question)
      -> Sarvam bulbul:v4-flash (audio)
      -> React                 (shows text, plays audio)

No database and no login in the MVP. Conversation context lives only for the session.

## Provider switches

- `ALLOW_REAL_API_CALLS=false` (default): every provider returns mock data.
- `LLM_PROVIDER`: `mock`, `sarvam` or `gemini`. No automatic fallback between providers.
- The backend will enforce these switches. They are not implemented yet.

## APIs

| Use | Endpoint | Model |
|---|---|---|
| Speech-to-text | `POST https://api.sarvam.ai/speech-to-text` (under 30 s) | `saaras:v4` |
| Text-to-speech | `POST https://api.sarvam.ai/text-to-speech` (max 2,500 chars) | `bulbul:v4-flash` |
| LLM, proposed | `POST https://api.sarvam.ai/v1/chat/completions` | `sarvam-105b-conversations` |
| LLM, on hold | Gemini API | `gemini-3.5-flash-lite` (stable) |

Frontend setting (public, not a secret): `VITE_API_BASE_URL`.

## LLM decision: pending

**Gemini.** Its terms require API users to be 18+ and bar apps directed towards, or likely to be
accessed by, under-18s. VaaniX targets students and the general public, so compliance is
uncertain. An age checkbox or an "adult learners" label does not settle it.
On the free tier, Google may use prompts and responses to improve its services, and human
reviewers may read them.

**Proposed: Sarvam `sarvam-105b-conversations`.** Same key as speech, paid from free credits.
Telugu answer quality is untested.

**Sarvam is not a blanket solution for minors.** Its terms allow under-18 use only with
verifiable parental or guardian consent, and its privacy policy says its services are not
directed at children. This applies to speech features too. Separate platform/API terms
exist and have not been reviewed.

**MVP scope:** operated and demonstrated by adult team members. No public launch, and no
use by minors, until the age and consent question is resolved.

**Data use:** Sarvam may use inputs and outputs, including audio, to improve models unless
you opt out. Opt out in account settings before the first real call.

## Cost (before GST)

| Item | List price |
|---|---|
| Speech-to-text | ₹0.49 per minute |
| Bulbul v4 Flash | ₹2.00 per 1,000 characters |
| sarvam-105b-conversations | ₹10 input / ₹25 output per 1M tokens (introductory, to end of 2026) |
| Free credits | ₹100 per verified user |

Estimate per turn (10 s speech, 200 spoken characters, about 600 input and 200 output tokens):
0.082 + 0.400 + 0.011 = about ₹0.49, or roughly 200 turns. Estimates, not measurements.
When credits end, requests fail (HTTP 402). The app must stop and say so. Never top up.

## Safety rules for answers

Simple language, ask when information is missing, never invent scheme details,
never diagnose or prescribe.

## Sources

- https://docs.sarvam.ai/api/getting-started/pricing
- https://www.sarvam.ai/api-pricing
- https://www.sarvam.ai/terms-of-service
- https://www.sarvam.ai/privacy-policy
- https://docs.sarvam.ai/api-reference/chat/chat-completions
- https://ai.google.dev/gemini-api/terms
- https://ai.google.dev/gemini-api/docs/models/gemini-3.5-flash-lite
