# Quickstart

A 3-minute walkthrough for chaplains opening the planner for the first time.

## 1. Open the notebook in Colab

Click the **Open in Colab** badge in the [main README](../README.md). The notebook opens read-only in your browser.

## 2. Save a copy to your Drive

In Colab: **File → Save a copy in Drive**. A new tab opens with your editable copy. Close the original read-only tab. Work in your copy from now on.

## 3. Add your OpenAI API key

You need your own key — the notebook author's key is not shared.

1. Get a key at <https://platform.openai.com/api-keys> (about \$0.005 per full notebook run on `gpt-4o-mini`).
2. In Colab, click the **key icon** in the left sidebar.
3. Click **+ Add new secret**.
4. Name: `OPENAI_API_KEY`. Value: paste your key.
5. Toggle **Notebook access ON**.

Detailed walkthrough with screenshots: [API_KEY_SETUP.md](API_KEY_SETUP.md).

## 4. Run all cells

**Runtime → Run all**.

- The first time, click **Grant access** when Colab asks if the notebook may read your secret.
- Step 0.5 should print `API_KEY loaded: length=…`.
- Step 0.6 should print `✅ Key works.`

If either fails, see [API_KEY_SETUP.md](API_KEY_SETUP.md) troubleshooting section.

## 5. Walk through Steps 1–6

| Step | What you do |
|---|---|
| 1 | Type or paste a free-form scenario description. Click **Autofill scenario**. |
| 2 | Review the form. Edit anything wrong. |
| 3 | Click **Generate Plan**. Read the rules-based profile and organizer. |
| 4 | (Optional) Export the plan to Markdown. |
| 5 | (Optional but recommended) Type your concept, scripture, illustrations, or draft. |
| 6 | Click **Generate AI Draft**. Review and edit the draft before delivery. |

## 6. Save your output

Step 4 and the export cell at the end of Step 6 save Markdown files into Colab's temporary file system. To keep them:

- **Files panel** (folder icon, left sidebar) → right-click the `.md` → **Download**.
- Or mount your Drive separately and copy them over.

## OPSEC checklist before you type

- No names of people or units.
- No location specifics that identify an installation, route, or operation.
- No classification markings, ever.
- Use generic descriptors: "squad-sized element after a training accident," not specifics.

See [OPSEC.md](OPSEC.md).

## What to do with the AI draft

Treat it as a **starting draft only**.

- Verify any scripture quotations the model produced.
- Check that the structure honors the time cap (read aloud with a stopwatch).
- Cut anything that doesn't serve your one core message.
- Keep the chaplain's voice; the model's job was to tighten and shape, not to author.
