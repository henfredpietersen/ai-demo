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

---

<a id="brief-writer-demo"></a>
# Narration: WordPress Content Brief Writer (1:29)

Same voice clone, same rule: the script and the work are mine.

**Add a topic** · Screen: Google Sheet
This is my WordPress Content Brief Writer, the project closest to the work on your roadmap. A content team adds topics to a Google Sheet. Here I'm adding one: storing coffee beans.

**Run the agent** · Screen: Brief agent menu, script running
One menu click sends every new row to my live agent. It's a LangGraph workflow: it searches the WordPress site through its REST API, decides which posts to read, and then writes the brief.

**Result** · Screen: the filled-in row
About a minute later, the row is filled in: done, a link to the Google Doc, grounded yes, how many posts it read, and which model ran.

**The brief** · Screen: the Google Doc
Here's the brief. A working title and an angle. An outline. The existing posts to link, the facts the site already states, and the gaps the new article should fill. The agent may only cite pages it actually read. A check at the end enforces that, and the Doc lists exactly what it read.

**Live API** · Screen: wp-brief-agent.onrender.com/docs
Behind the Sheet is a FastAPI service on Render, with token-protected live routes, streaming, and an hourly cap. It runs on Groq with tool calling, and the same graph supports the Anthropic API.

**Code** · Screen: the GitHub repository
I designed it, directed Claude to write the code, reviewed it, and shipped it, with tests running on every push. The code and the live evaluation results are on GitHub. Thanks for watching.
