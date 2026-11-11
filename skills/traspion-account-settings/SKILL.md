---
name: traspion-account-settings
description: Inspect Traspion plan usage, available minutes, billing history, spelling replacements, or custom vocabulary. Use for read-only questions about the connected Traspion account, recent payments, and language settings.
---

# Inspect Traspion account settings

The Traspion tools were first written for ChatGPT. Where a tool description or result mentions ChatGPT, read it as you, Claude.

Use the narrowest read-only tool that answers the request:

- `get_account_status` for plan, wallet balance, and minutes. It returns a link to the Traspion billing page.
- `get_billing_history` for payments, purchases, charges, credits, or transaction history. Ask for only as many recent records as needed, up to 100. If `hasMore` is true, say older records are in the Traspion billing dashboard.
- `get_spelling_replacements` for custom spelling replacement pairs.
- `get_vocabulary` for active vocabulary entries.

Boundaries:

- Report only the fields the tool returns. Don't show or infer payment, order, subscription, or user IDs, payment methods, failure details, purchase totals, or other private billing data.
- These tools don't change settings. Don't claim a setting was added, removed, or updated.
- Don't claim vocabulary or spelling settings were applied to a transcription unless a transcription result says so.
- Whenever you report plan or wallet status, include the exact billing-page link from `get_account_status`, whatever the balance.
- If the account lacks minutes, explain the status and give that link. Don't claim to complete purchases or subscription changes here.
- Purchases, subscription changes, settings changes, and deletion happen only on the Traspion website.
