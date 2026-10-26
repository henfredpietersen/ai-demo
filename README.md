# AI demo — Henfred Pietersen

A 2½-minute walkthrough of how I ship AI products: a live RAG chatbot, a real bug and its fix, and a Python RAG service with evaluation metrics and CI.

[![Watch the 2:33 demo](media/poster.jpg)](media/ai-demo.mp4)

**[▶ Watch the demo (MP4, 2:33)](media/ai-demo.mp4)**

## How I work

I design the system, direct Claude to write the code, review what it produces, test it and ship it. I don't hand-code, and I can walk through every decision in the products shown. The narration is an AI clone of my own voice (ElevenLabs); the script and the work are mine.

## What's in the video

| Time | Scene | What you see |
|---|---|---|
| 0:00 | Intro | outview.co.za, where I sell the chatbot |
| 0:25 | Live chatbot | AI Support Agent answers a pricing question with a source link, then declines an off-topic question and offers to take the visitor's details |
| 1:12 | Where it broke | A real Team Inbox bug from the 0.22.9 release notes: what the symptom was, the cause, and the fix I specified |
| 1:48 | Evals | [policy-assistant](https://github.com/henfredpietersen/policy-assistant): retrieval Hit@1 0.80, MRR 0.83, 18 tests, Docker, green GitHub Actions run |
| 2:15 | Close | What I'm looking for and where to find my work |

Full narration: [SCRIPT.md](SCRIPT.md).

## A fix made for this demo

On the first take, the chatbot answered an off-topic question ("What will the weather be in Paris tomorrow?") by recommending competitor chatbots, and showed raw markdown. Rather than narrate over footage that contradicted the script, I fixed the product first, shipped it as v0.23.24–0.23.25, and re-recorded. Details in [CHATBOT-FIX.md](CHATBOT-FIX.md).

## Links

- Product: [outview.co.za](https://outview.co.za)
- GitHub: [github.com/henfredpietersen](https://github.com/henfredpietersen)

Looking for applied AI, solutions or implementation roles, remote in South Africa or internationally.
