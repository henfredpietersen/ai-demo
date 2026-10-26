# The fix behind scene 2

AI Support Agent is a self-hosted WordPress chatbot (PHP) that answers from the site's own content (RAG) across seven LLM providers with fallback. The plugin source is commercial and isn't in this repo; this note describes the change.

## What went wrong (recorded live, v0.23.23)

| Question | Expected | What happened |
|---|---|---|
| "How much does the Starter licence cost?" | Price plus a link to the pricing page | Correct price (R999, once-off), but **no source link** |
| "What will the weather be in Paris tomorrow?" | Decline and offer to take details | Answered with a **comparison of competitor chatbots** (Tidio, ChatBot.com, Intercom), **raw `**markdown**`** visible, and blog posts listed as sources |

## Why

1. **Retrieval always returns something.** Semantic search returns its top-k chunks even when none are relevant. For "weather in Paris", the nearest chunks were chatbot-comparison blog posts, so the model got those as CONTEXT.
2. **"Only answer from CONTEXT" in the system prompt wasn't enough.** The model treated the decoy content as relevant and answered from it.
3. **Pricing skips retrieval.** A pricing question is routed straight to a pricing tool, so there were no RAG sources to show. The tool returned no source of its own.
4. **The widget rendered replies as plain text,** so markdown from the model appeared with its asterisks.

## What I directed Claude to change

- **Grounding rules appended last on every RAG turn**, so they override a looser custom prompt: answer only from CONTEXT; if CONTEXT doesn't answer the question, reply with the exact sentinel `[[NO_ANSWER]]`.
- **A server-side branch on the sentinel.** The server swaps it for a fixed decline ("I don't have information about that — I can only help with questions about Outview…"), clears sources, and flags `offer_lead` to the widget. Declining becomes deterministic instead of relying on the model to phrase a refusal.
- **A "Leave my details" button** under a declined reply. The first version auto-opened the lead form, which covered the decline message, so I changed it in 0.23.25.
- **Tools can return a `source`.** The pricing tool now returns its pricing page (South Africa or international, matching the visitor's currency), shown as the reply's source link.
- **Safe markdown rendering in the widget.** Bold, bullets and links are built as DOM nodes, never `innerHTML`, so reply text can't inject markup. I tested this with an `<img onerror>` payload, which rendered as text.
- **Found while checking: a pricing data bug.** The pricing tool quoted the Agency tier at $499 / R7,999 while every page said $269 / R4,500. Corrected.

## How it was verified

- PHP lint on every changed file. Unit-style checks of the grounding prompt, the decline text and the pricing tool's source for both currencies.
- Markdown renderer tested in a headless browser against bold, bullets, links, bare URLs, headings and an injection attempt.
- Installed on outview.co.za, cache cleared, and confirmed the live page served the new widget version.
- Re-asked both questions on the live site. The recording in the video is that run.

## Known limits

- The decline depends on the model emitting the sentinel. A model that ignores instructions could still answer off-topic; a relevance-score threshold on retrieval would be a stronger second guard.
- Pricing tiers are hard-coded in the tool, which is how the Agency price drifted from the site. Reading them from one settings source would prevent that.
