# OPSEC

This tool is designed for **planning and self-development**, not for processing sensitive information.

## What leaves your environment

When you use Steps 1, 5, or 6, the contents of those text fields are sent to the OpenAI API over HTTPS. OpenAI's API data usage policy applies. The notebook itself does no logging — but anything you type into the form is part of the API request.

For Steps 0–4 (everything before the LLM autofill and the LLM draft), nothing leaves your browser. The rules-based profiler runs locally in the Colab kernel.

## Do not enter

- Names of soldiers, family members, or any individuals.
- Specific unit identifiers (UIC, regiment, battalion, company designators).
- Specific locations (installation names, AO designators, grid coordinates, route names).
- Operation names or codewords.
- Dates and times tied to actual operations.
- Anything classified at any level. Ever.
- Medical, legal, or pastoral counseling content tied to identifiable individuals.

## Do enter (generic descriptors are fine)

- "Squad-sized element after a training accident."
- "Exhausted work crews on day five of disaster response."
- "Mixed unit formation, predominantly junior enlisted, highly pluralistic."
- "Family of a soldier lost in the line of duty, plus the soldier's company."
- "Deployment send-off for a company headed to a multi-month rotation."

## If you have to refer to a real event

- Strip identifiers. Use roles ("the squad leader," "the soldier's spouse"), not names.
- Generalize the incident type ("training accident," "line-of-duty death") rather than specifics.
- Round time references ("yesterday," "this morning"), don't use exact times.

## What about saved Markdown exports?

Steps 4 and the Step 6 export write files into Colab's temporary file system. If you download them, treat them as **For Official Use Only / sensitive working drafts** by default and store them on appropriate systems. Do not email them or paste them into uncleared chat tools.

## What about the AI draft?

The model's response is also processed via the OpenAI API. The same caveats apply. Review the draft, edit out anything that drifted toward specifics, and store the final under your normal information-handling rules.

## When in doubt

If the planning content involves specifics you wouldn't put on an unclassified GPMS or send over commercial email — don't put it in this notebook. Use the rules-based profile only (skip Steps 1, 5, and 6) and write the message yourself.
