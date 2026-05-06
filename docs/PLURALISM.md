# Pluralism

This tool is built to operate inside the U.S. Army's pluralistic chaplaincy model. It is **descriptive and culturally adaptive**, not prescriptive.

## What "pluralism-safe" means here

- The tool does **not** generate doctrine.
- The tool does **not** advocate one tradition over another.
- The chaplain supplies all sacred text, theological framing, and tradition-specific content.
- The tool's job is to help shape, structure, and time-fit that content for the audience and context.

## How the rules-based profiler handles pluralism

The profiler reads the **Cultural / faith mix** field (Homogeneous / Moderately mixed / Highly pluralistic) and adjusts the recommended posture:

- **Highly pluralistic** audiences trigger guidance such as "speak from your tradition without requiring shared belief," "use universal human anchors (breath, light, presence, courage) alongside sacred text," "avoid in-group shorthand," "offer blessing in inclusive form."
- **Homogeneous** audiences allow more tradition-specific language, with the standing reminder that outliers may still be present.

These outputs are guidance for the chaplain. They are not theological claims.

## How the LLM draft step handles pluralism

The system prompt for Step 6 explicitly orders the model to:

1. **Treat chaplain-supplied scripture and wording as authoritative.** If you paste a passage from your tradition, the model preserves it. It does not water down tradition-specific language; it frames it so listeners from other traditions can still receive the message with respect.
2. **Avoid prescribing doctrine.** The model produces inclusive framing around your content, not new theology.
3. **Avoid insider shorthand** that requires shared belief to land (e.g., undefined jargon).
4. **Offer the closing blessing** in a form a mixed audience can receive from their own tradition.
5. **Flag every section** in a "Notes for the Chaplain" block, so you can see what was preserved from you, what was filled in by the model, and what to verify.

## What the tool will not do

- It will not paraphrase scripture you only referenced (without quoting) into a fabricated quotation. References-only inputs come back marked "verify exact wording."
- It will not invent details about specific traditions it doesn't have explicit input about.
- It will not produce content that disparages any tradition or non-tradition.

## Supervisor / endorser oversight

For training programs and IDP integration, the rules-based profile (Steps 1–4) is the most useful artifact for review: it surfaces structure, tone, posture, and pluralism considerations without committing to any specific theological content. Use it as a planning document a supervising chaplain can review across endorser lines.

## Reporting concerns

If the tool produces output that crosses a pluralism, theological-neutrality, or trauma-responsiveness line in a way the system prompt should have caught, file an issue with:

- The scenario inputs (generic — no PII).
- The chaplain content provided (if any).
- The LLM output that violated the line.
- What the correct posture would have been.

Prompt-tuning fixes for systemic issues will be released as repo updates.
