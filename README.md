# Sacred Speech Scenario Planner

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/KirtisChristensen/sacred-speech-planner/blob/main/Sacred_Speech_Planner_v3.ipynb)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A planning tool for U.S. Army chaplains and supervisory UMTs that helps rapidly produce **context-appropriate sacred speech** — devotionals, homilies, memorial remarks, trauma responses — for any operational or garrison scenario.

The tool combines a **transparent rules-based profiler** (no AI, fully auditable) with an optional **LLM-assisted draft step** that treats the chaplain's own scripture, illustrations, and concept as the authoritative source material.

## What it does

1. The chaplain types a free-form description of the event.
2. The LLM extracts structured form fields (event type, audience, trauma level, time, etc.).
3. The chaplain reviews and edits those fields.
4. A rules-based profiler outputs a recommended **form**, **structure with timing**, **tone**, **trauma-responsive posture**, **pluralism posture**, and a fillable organizer.
5. The chaplain optionally provides their own concept, scripture references, illustrations, or draft text.
6. The LLM produces a draft sacred speech that **preserves** the chaplain's content and shapes it to the recommended structure within hard guardrails (pluralism-safe, trauma-responsive, time-capped, no platitudes, no PII echo).

## Quickstart

1. Click the **Open in Colab** badge above.
2. In Colab: **File → Save a copy in Drive** (so you don't edit the canonical version).
3. Get an OpenAI API key at <https://platform.openai.com/api-keys>. Typical full run costs about **\$0.005** on `gpt-4o-mini`.
4. In Colab's left sidebar, click the **key icon** → **+ Add new secret** → name it `OPENAI_API_KEY`, paste the key, toggle **Notebook access ON**.
5. **Runtime → Run all**, click **Grant access** on the consent popup the first time.
6. Walk through Steps 1–6.

Detailed walkthrough: [docs/QUICKSTART.md](docs/QUICKSTART.md). Key setup screenshots: [docs/API_KEY_SETUP.md](docs/API_KEY_SETUP.md).

## OPSEC

**Use generic descriptors only.** No PII, names, unit identifiers, classified material, or sensitive operational detail. Inputs in Steps 1 and 5 are sent to the OpenAI API. See [docs/OPSEC.md](docs/OPSEC.md).

## Pluralism

Recommendations are **descriptive and culturally adaptive**, not prescriptive. The chaplain supplies all sacred text and doctrinal content. The LLM is instructed to preserve tradition-specific wording the chaplain provides while keeping framing inclusive for mixed-faith formations. See [docs/PLURALISM.md](docs/PLURALISM.md).

## Privacy / your key

- Each user supplies **their own** OpenAI API key. The notebook author's key is never shared via the link.
- Keys live in Colab Secrets (per-user, per-account). They are not committed to the repo and are not visible to other viewers of the notebook.
- The notebook does no logging, telemetry, or background calls.

## Examples

Sample scenario descriptions you can paste into Step 1 to try the tool:

- [examples/hurricane_recovery.md](examples/hurricane_recovery.md)
- [examples/combat_loss_memorial.md](examples/combat_loss_memorial.md)
- [examples/deployment_sendoff.md](examples/deployment_sendoff.md)

## Running locally (instead of Colab)

```bash
git clone https://github.com/KirtisChristensen/sacred-speech-planner.git
cd sacred-speech-planner
pip install -r requirements.txt
export OPENAI_API_KEY=sk-...   # or set as Windows env var
jupyter notebook Sacred_Speech_Planner_v3.ipynb
```

## License

[MIT](LICENSE). The notebook itself is freely usable; the chaplain remains the author of any sacred speech produced.

## Feedback

File issues with: which step, what you typed (generic — no PII), what was produced, what you expected. PRs welcome for examples, prompt tuning, and documentation.
