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
- The setup cell loads the API key and prompts; the launcher cell renders the wizard.
- On the **Welcome** screen you should see `✅ API key works.`

If the key check fails, see [API_KEY_SETUP.md](API_KEY_SETUP.md) troubleshooting section.

## 5. Walk through the 5 wizard screens

Use **Next ▶** / **◀ Back** to move between screens.

| # | Screen | What you do |
|---|---|---|
| 1 | Welcome | Confirm the API key works (automatic). |
| 2 | Describe | Paste a free-form scenario description. Click **Autofill from description**. |
| 3 | Review | Review the form. Edit anything the AI got wrong (especially Time, Trauma, Fatigue, Cultural mix). |
| 4 | Plan | Read the rules-based profile and organizer. (Optional) add your concept, scripture, illustrations. |
| 5 | Draft | Click **Generate AI Draft**. Review and edit before delivery. Export the plan + draft to Markdown. |

## 6. Save your output

The export button on screen 5 saves a Markdown file into Colab's temporary file system. To keep it:

- **Files panel** (folder icon, left sidebar) → right-click the `.md` → **Download**.
- Or mount your Drive separately and copy it over.

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
