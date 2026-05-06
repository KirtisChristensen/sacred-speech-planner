# API Key Setup

Each user of the planner supplies their **own** OpenAI API key. The notebook author's key is **not** shared via the Colab link â€” Colab Secrets are per-user, per-Google-account.

## Step 1 â€” Create an OpenAI API key

1. Go to <https://platform.openai.com/api-keys>.
2. Sign in (or create an OpenAI account).
3. Click **+ Create new secret key**. Give it a memorable name like `sacred-speech-planner`.
4. Copy the key. It starts with `sk-`. **You will not be able to view it again** â€” copy it now or you'll have to create another.
5. Make sure your account has billing set up: <https://platform.openai.com/account/billing>. A \$5 minimum credit is enough for many hundreds of full notebook runs.

### Cost note

The default model is `gpt-4o-mini`. A typical full run (autofill + draft) uses well under \$0.01. Heavy daily use of the tool would still be in the cents-per-day range.

## Step 2 â€” Add the key to Colab Secrets

1. Open the notebook in Colab (click the **Open in Colab** badge in the README).
2. **File â†’ Save a copy in Drive** so you're working in your own copy.
3. In the left sidebar, click the **key icon** (Secrets).
4. Click **+ Add new secret**.
5. **Name:** `OPENAI_API_KEY` (exact spelling, all caps, with the underscore).
6. **Value:** paste the `sk-â€¦` key from Step 1.
7. Toggle **Notebook access** to **ON** for this notebook.

> The key now lives in your Google account's secret store. It is **not** stored in the notebook file. Anyone else opening the notebook with their own Colab account sees the notebook code but not your key value.

## Step 3 â€” Verify

1. Run **Step 0.5** in the notebook.
2. The first time, Colab pops up: *"Grant this notebook access to your secret OPENAI_API_KEY?"* Click **Grant access**.
3. Step 0.5 should print:
   ```
   Provider: openai
   LLM configured: gpt-4o-mini @ https://api.openai.com/v1
   API_KEY loaded: length=51, starts with 'sk-p'
   ```
4. Run **Step 0.6**. It should print:
   ```
   âœ…  Key works. Model gpt-4o-mini replied: 'ready.'
   ```

You're done. Continue with Step 1.

## Optional secrets

Add these the same way as Step 2 if you want to override defaults:

| Secret name | Purpose | Example value |
|---|---|---|
| `LLM_PROVIDER` | Switch to xAI Grok instead of OpenAI | `xai` |
| `LLM_MODEL` | Use a different model | `gpt-4o`, `gpt-4.1-mini` |
| `XAI_API_KEY` | xAI key (if `LLM_PROVIDER=xai`) | `xai-â€¦` |

## Troubleshooting

### Step 0.5 shows `length=0` or `YOUR_KEY_HERE`

- Check the secret name is exactly `OPENAI_API_KEY` (no leading/trailing spaces).
- Confirm **Notebook access** is toggled ON for this notebook.
- Re-run Step 0.5. If still failing, click **Grant access** if the consent popup appears.

### Step 0.6 fails with `401 Incorrect API key`

- The key is invalid, revoked, or copied incomplete. Create a new key and update the secret.

### Step 0.6 fails with `429 You exceeded your current quota`

- No billing on the account. Add a payment method at <https://platform.openai.com/account/billing>.

### Step 0.6 fails with `model_not_found`

- Your account doesn't have access to the configured model. Set `LLM_MODEL` to one you do have, e.g. `gpt-4o-mini`.

### "Notebook access" toggle is greyed out

- The notebook tab might be the read-only canonical version. Make sure you did **File â†’ Save a copy in Drive** and you're editing your copy.

## If you'd rather not use Colab Secrets

In Step 0.5 there is a commented line:

```python
# API_KEY = "sk-PASTE-YOUR-OPENAI-KEY-HERE"
```

Uncomment it and paste your key. **Do not commit a notebook with a pasted key to GitHub** and **do not share** that copy of the notebook. Prefer Secrets for anything you might share.
