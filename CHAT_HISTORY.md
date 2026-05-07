# Sacred Speech Scenario Planner — Chat History

**Project:** Sacred Speech Scenario Planner for U.S. Army Chaplains
**Repo:** <https://github.com/KirtisChristensen/sacred-speech-planner>
**Captured:** May 6, 2026
**Tooling:** GitHub Copilot (VS Code) — Claude Opus 4.7

---

## Phase 1 — Concept and v1 (rules-based + first LLM call)

### Initial ask

> "I'm making a tool for the army that supports planning for the context of any given event scenario applying the best practices and principles for training in handling of Sacred Speech. Could this be implemented using Jupyter notebook with a steps for inputting the event description and characterizing context inputs and then with a connection to OpenAI to generate the outputs? Run on Google Colab?"

### Outcome

- Confirmed Jupyter on Colab + OpenAI is a good fit.
- Built `Sacred_Speech_Planner.ipynb` (v1):
  - `ipywidgets` form for scenario inputs (event, audience, time, context, goals).
  - Rules-based profiler (`@dataclass ScenarioInputs` → `ScenarioProfile`).
  - Markdown organizer template output.
  - Phase 2 layered an LLM-generated draft on top using OpenAI Python SDK.
- Default model: `gpt-4o-mini`. Cost: ~\$0.005/run.
- API key load via Colab Secrets bridged into `os.environ`.

### Guardrails baked into the system prompt

- Pluralism-safe (no prescribed doctrine).
- Trauma-responsive (no platitudes; presence over explanation; no graphic re-narration).
- Time-capped (~130 wpm × 0.8).
- No PII echo.
- No fabricated scripture quotations.
- Draft only — chaplain remains author.

---

## Phase 2 — v2 enhancements

### Asks

> "When the chaplain writes up the event description and situation context in natural language, the LLM is employed to setup the configuration settings in the scenario inputs of step 1. Allow the chaplain to review the outline through step 3 and save that if they wish, or allow them to input their concept for what they wish to convey and even their detailed content to somehow include with scripture references or illustrations. Have the LLM process through the Step 4 to use for the Generate Draft AI content source."

> "The Scenario description input should come first and be used to configure the initial settings for step 1 for Event, Audience, Time & Goals, and Chaplain notes."

### Outcome (`Sacred_Speech_Planner_v2.ipynb`)

Six-step workflow:

| Step | Action |
|---|---|
| 1 | Natural-language scenario description → click **Autofill scenario** (LLM JSON-mode → form widgets). |
| 2 | Review/edit form fields. |
| 3 | Click **Generate Plan** — rules-based profile + organizer. |
| 4 | Export plan to Markdown (optional). |
| 5 | Chaplain content: concept, scripture, illustrations, draft, constraints (optional). |
| 6 | Click **Generate AI Draft** — uses chaplain content as authoritative source. |

User confirmed: *"works well."* Shared via Colab link with view access; key safety verified (Colab Secrets are per-user; the shared link does not leak the author's key).

---

## Phase 3a — GitHub-distributable repo skeleton

### Ask

> "A Version 3 will need to be created that can be deployed from a public GitHub repo and downloaded and run from Colab with their own API key."

License decision: **MIT**.

### Outcome — `repo/` directory created

| File | Purpose |
|---|---|
| `README.md` | Landing page with Colab badge, quickstart, OPSEC/pluralism, examples, local-run instructions. |
| `LICENSE` | MIT, "Copyright (c) 2026 Sacred Speech Planner Contributors". |
| `requirements.txt` | `openai>=1.0.0`, `ipywidgets>=8.0.0`. |
| `.gitignore` | Notebook checkpoints, generated `sacred_speech_plan_*.md`, `.env`, OS noise. |
| `Sacred_Speech_Planner_v3.ipynb` | v2 + v3 edits (see below). |
| `docs/QUICKSTART.md` | 3-min walkthrough. |
| `docs/API_KEY_SETUP.md` | Step-by-step with troubleshooting (length=0, 401, 429, model_not_found). |
| `docs/OPSEC.md` | What NOT to enter; what's safe; what about exports. |
| `docs/PLURALISM.md` | Rules-based + LLM behavior; supervisor oversight; reporting concerns. |
| `examples/hurricane_recovery.md` | Canonical scenario, expected autofill values. |
| `examples/combat_loss_memorial.md` | Memorial homily / lament+hope arc. |
| `examples/deployment_sendoff.md` | Large formation send-off. |

### v3 notebook edits over v2

1. Title cell rebranded to v3 with embedded first-time setup callout, Save-a-Copy reminder, OPSEC + pluralism summaries.
2. Deleted redundant standalone OPSEC cell.
3. Inserted **Step 0.6 Key Health Check** — 1-token round-trip with try/except diagnostics for 401, 429, `model_not_found`.
4. Final markdown shows version stamp, GitHub issues link, validation checklist, roadmap.

---

## Phase 3b — Patch placeholders + push to GitHub

### Ask

User provided real repo URL: `https://github.com/KirtisChristensen/sacred-speech-planner`.

### Outcome

Replaced 5 occurrences of `REPLACE_USER` → `KirtisChristensen`:
- `repo/README.md` lines 3 (Colab badge URL) and 55 (clone URL).
- `repo/Sacred_Speech_Planner_v3.ipynb` lines 16 (badge URL in title cell), 1151 (version footer), 1155 (issues link).

Provided three push paths: web upload, git CLI, `gh repo create`. User pushed via git CLI; commit `2b2aca7` ("Initial v3 release") landed on `main`.

---

## Phase 3b.1 — Mojibake fix

### Issue reported

> "There is a some messed up symbols scattered through the text that loaded into github as follows: â€—"

### Root cause

PowerShell 5.1's `Set-Content -Encoding UTF8` had read UTF-8 files as cp1252 and re-saved them, double-encoding every em-dash, en-dash, and curly quote. GitHub then rendered each as `â€"` etc. Each file also got a stray leading `?` byte from the original UTF-8 BOM (U+FEFF) being unrepresentable in cp1252.

### Fix

For each `.md` and `.ipynb` file under `repo/`:
1. Read current bytes; decode as UTF-8 → re-encode as cp1252 (reverse round-trip) → write back.
2. Strip stray leading `?` byte where present.
3. Verified notebook still valid JSON (21 cells); verified no remaining `C3 A2 E2 82 AC` mojibake byte sequences.

Pushed as commit `ed99984` ("Fix double-encoded UTF-8 (em-dashes, curly quotes)").

---

## Phase 3b.2 — Requirements doc question

### Ask

> "Do we need to update the Requirements and Design document?"

### Recommendation given

Yes — the existing `Requirements and Design.md` is the original v1.0 spec from before any code existed. Identified gaps:

1. Implementation reality (Jupyter+Colab+OpenAI vs. doc's "Streamlit/Gradio MVP").
2. Six-step workflow not described.
3. LLM integration (model, JSON-mode autofill, system prompts) absent.
4. Pluralism + trauma safeguards in code (system prompts, allowed-value lists, no-PII rule).
5. v3 distribution model (public GitHub, MIT, per-user Colab Secrets).
6. OPSEC requirements.
7. Key Health Check (Step 0.6) operational requirement.
8. Updated success metrics (cost/run, draft-only output).
9. Version stamp bump from "1.0 Draft" to "3.0 As-Built".

Two options proposed:
- **Option A (lighter):** Append a "Section 8: As-Built Implementation (v3.0)" while preserving the v1.0 design intact.
- **Option B (fuller rewrite):** Update each section in place with a revision-history block.

User selected Option B — but first wanted UX improvements addressed.

---

## Phase 3b.3 — UX: cleaner interface for non-technical users

### Ask

> "Before we update to option B, how could we make the flow cleaner and easier to use for people who are not familiar with Jupyter notebooks or get nervous and confused when they see Python code? Can we make a cleaner interface that steps people through without all that confusion for them?"

### Four options presented

1. **Hide the code** (smallest change, stays in Colab) — collapse code cells via metadata; ~1 hour effort.
2. **Single "wizard" cell with stepper widget** — `Stack` + `IntProgress` + Back/Next buttons; ~half-day.
3. **Voilà / Solara / Gradio app** — true single-page web app; 1–2 days; takes on hosting story.
4. **Full hosted web app** — Flask/FastAPI + frontend; best UX, worst fit for current constraints.

User chose **Option 1**.

### Implementation pass 1 (insufficient)

Added `jupyter.source_hidden: true` and `cellView: "form"` metadata to all 11 code cells. User reported:

> "I still see code in the notebook by default when I open it. Nothing is hidden."

### Diagnosis

VS Code ignores `source_hidden`; Colab's "form mode" only kicks in when the **first line** of the cell is a `#@title` directive.

### Implementation pass 2 (working)

Prepended each code cell with a Colab form directive auto-generated from the existing first-line comment, e.g.:

```python
#@title Step 1 — Build form widgets (silently) + Scenario Description input (hidden code) { display-mode: "form" }
```

Result: Colab renders each code cell as a single clickable bar showing the title; Python source collapsed by default; widget output renders normally below.

Also rewrote the top markdown cell into a **3-step "what to do" guide** (open in Colab → add key → Run all → scroll), with a clear note that *no code reading is required*.

User confirmed:

> "It's working."

Pushed as commit `9d3b6c5` ("UX: hide code cells via Colab #@title form directives").

---

## Phase 3b.4 — Refresh-without-clutter workflow

### Ask

> "How do I refresh the upload to Colab without having a bunch of versions running?"

### Recommendation given

Two separate copies are in play:
1. **Canonical (GitHub):** opened by the badge, always fresh.
2. **Drive copy:** frozen snapshot from File → Save a copy in Drive.

Clean refresh workflow:
1. After every push, click the Open-in-Colab badge to fetch fresh from GitHub.
2. Don't save another Drive copy unless you actually need to retain scenario inputs.
3. Clean up old Drive copies via <https://drive.google.com> search for `Sacred_Speech_Planner`.
4. Bookmark the direct Colab+GitHub URL to bypass the README.

Direct URL:
```
https://colab.research.google.com/github/KirtisChristensen/sacred-speech-planner/blob/main/Sacred_Speech_Planner_v3.ipynb
```

---

## Current state (end of session)

### Repo on GitHub (`main` branch)

| Commit | Description |
|---|---|
| `2b2aca7` | Initial v3 release |
| `ed99984` | Fix double-encoded UTF-8 (em-dashes, curly quotes) |
| `9d3b6c5` | UX: hide code cells via Colab `#@title` form directives |

### What chaplains experience now

- Click **Open in Colab** badge → fresh notebook.
- See readable headings, short instructions, and form-style title bars (no Python code visible).
- Add `OPENAI_API_KEY` once via Colab Secrets.
- **Runtime → Run all** once.
- Scroll down and use forms in Steps 1–6.
- Total cost ~\$0.005/run. Drafts only — chaplain edits before delivery.

### Pending / deferred

- **Phase 3c** (deferred): issue templates, `CONTRIBUTING.md`, version tags.
- **Option B requirements doc rewrite** (deferred): full update of `Requirements and Design.md` to v3.0 as-built spec with revision history.
- **Optional UX polish:** merge setup steps, friendly try/except wrappers around handlers, renumber steps.
- **Phase 4 ideas** (roadmap): Drive auto-export, post-event SMFF scoring CSV, prebuilt example presets, Streamlit/Gradio port.

---

## Key technical decisions captured

- **Distribution model:** public GitHub repo (MIT) + Colab badge + per-user `OPENAI_API_KEY` via Colab Secrets. No hosted backend; no shared keys.
- **Default model:** `gpt-4o-mini`. Configurable via `LLM_MODEL` secret.
- **Provider:** OpenAI by default; xAI Grok supported via `LLM_PROVIDER=xai` + `XAI_API_KEY`.
- **Autofill:** JSON-mode with strict allowed-value lists per field; ignores out-of-vocabulary values returned by the model.
- **Source priority for AI draft:** chaplain content > scenario profile > model fills (clearly flagged in "Notes for the Chaplain").
- **Hide-code mechanism (Colab):** `#@title <label> { display-mode: "form" }` on the first line of every code cell; supplemented by `jupyter.source_hidden` metadata.
- **Encoding rule:** always write files as UTF-8 with no BOM via `[System.IO.File]::WriteAllText` + `UTF8Encoding($false)` — never `Set-Content -Encoding UTF8` in PS5.1.

---

## File layout (workspace)

```
Sacred Speech Tool/
├── Requirements and Design.md            # v1.0 spec (out of date — pending Option B rewrite)
├── Sacred_Speech_Planner.ipynb           # v1 (reference)
├── Sacred_Speech_Planner_v2.ipynb        # v2 (working personal copy)
├── CHAT_HISTORY.md                       # this file
└── repo/                                 # public GitHub repo content
    ├── README.md
    ├── LICENSE
    ├── requirements.txt
    ├── .gitignore
    ├── Sacred_Speech_Planner_v3.ipynb    # canonical, hidden-code version
    ├── docs/
    │   ├── QUICKSTART.md
    │   ├── API_KEY_SETUP.md
    │   ├── OPSEC.md
    │   └── PLURALISM.md
    └── examples/
        ├── hurricane_recovery.md
        ├── combat_loss_memorial.md
        └── deployment_sendoff.md
```
