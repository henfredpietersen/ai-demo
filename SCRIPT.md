# Narration script

Narrated with an AI clone of my own voice (ElevenLabs). The script and the work shown are mine.

---

## Scene 1 — Intro (0:00–0:25) · Screen: outview.co.za homepage

Hi, I'm Henfred Pietersen, founder of Outview in Cape Town. I build and sell AI products. I design the system, direct Claude to write the code, review what it produces, and ship it. I don't hand-code. In the next few minutes I'll show you how I make AI-built software work in production. And yes, this narration is an AI clone of my own voice, which felt like the honest way to make the point.

## Scene 2 — Live chatbot (0:25–1:12) · Screen: chat widget on outview.co.za

This is AI Support Agent, a self-hosted chatbot for WordPress that I sell in three licence tiers. It indexes the site's own pages, posts and products, and answers only from that content. Watch: I ask what the Starter tier costs, and it answers with a link to the page it used.

Now I ask something the site doesn't cover. Instead of inventing an answer, it says it doesn't know and offers to take my details. That's the whole point of grounding.

Under the hood it supports seven LLM providers. You set a primary and a fallback. If the primary fails, it switches automatically, and if every provider is down it still answers from the indexed content rather than going silent.

## Scene 3 — Where it broke (1:12–1:48) · Screen: changelog / release notes

Here's a real bug. Customers using the Team Inbox reported that an agent's reply would pop up again on later page visits, sometimes days later. The cause: on every page load, the widget re-checked the whole conversation from the start, so old replies looked new.

I described the symptom and the cause to Claude and specified the fix: the browser should remember which agent replies it has already shown, stored alongside the conversation ID. I reviewed the change, tested it across page loads, and shipped it as version 0.22.9.

## Scene 4 — Evals (1:48–2:15) · Screen: github.com/henfredpietersen/policy-assistant README + Actions tab

RAG fails quietly, so I insist on measuring it. This is policy-assistant, a small Python service for insurance FAQs. Retrieval scores 0.80 Hit at 1 and 0.83 MRR on its test set. It runs in Docker, and every push runs lint, eighteen tests and a smoke test in GitHub Actions. I specified the evaluation and the tests; Claude generated the code.

## Scene 5 — Close (2:15–2:33) · Screen: github.com/henfredpietersen profile

I'm looking for applied AI, solutions or implementation roles, remote in South Africa or internationally, where shipping with AI tools is how the work gets done. Links to my products and GitHub are below. Thanks for watching.
