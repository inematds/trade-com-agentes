# Trade com Agentes — the 7-day challenge method

**🇧🇷 [Português](README.md) · 🇺🇸 [English](README.en.md) · 🇪🇸 [Español](README.es.md)**

[![Trade com Agentes](guia/assets/banner.jpg)](https://inematds.github.io/trade-com-agentes/guia/en/)

> ## ⚠️ Read first: this is a study text, not a recommendation
>
> **I don't trust this to trade.** Trading is high risk, has too many variables, and **there is
> always someone on the other side with information we don't have**. This repository is not
> financial advice, not a validated strategy, and not an invitation to put money into a robot.
>
> The goal is different: **to learn from what he did** — how he built the agents, how he passed
> context from one to the next, where he got stuck, and what changed along the way. The result of
> the challenge itself makes the point: in 7 days, the system **lost to the S&P 500**.

## 📖 User guide

Full guide (landing page + step by step): **https://inematds.github.io/trade-com-agentes/guia/en/**

## Where it comes from

YouTube video: **"I Gave GPT 6 Astra $10,000 to Trade Stocks...And This Happened"** —
<https://www.youtube.com/watch?v=eg_1NXDcoPk>

The author gave $10,000 of real money to an agent on **Codex with GPT-6 Astra (high effort)** to
trade stocks over **7 trading sessions**, with the goal of **beating the S&P 500**. Unlike an
earlier test of his (with OpenClaw, 30 days, hands off), here he could make **up to two changes
per day** — but could not shut the system down, even while losing.

Everything here is a **paraphrase of the video**. Numbers are **"as reported in the video"**;
nothing was audited. The transcript is automatic, so some names may have been misheard (see
[metodo/06-diario-7-dias.md](metodo/06-diario-7-dias.md) (in Portuguese)).

## The method on one screen

```
07:45  pre-market    → reads news, checks the account, picks what to watch
09:30  1h into open  → looks for the first entry that passes the filters
11:00  midday        → reviews positions, last chance for a new entry
13:00  afternoon     → manages what is open
14:15  close         → closes the remaining positions
14:45  confirmation  → checks everything is flat and logs the day's result
15:15  final notice  → notification
(US Central time — session from 8:30 to 15:00 CT)

Each routine wakes up → READS the handoff note from the previous one → acts → WRITES the next note.
They all run in the SAME thread: it looks like a single agent working all day.
```

From day 2 on, a second piece came in: the model **refused to execute orders on its own**.
His solution: Astra becomes only the **strategist** and ends each routine by sending an **email**
with the recommendations to an **executor bot** (which has its own email + webhook). The bot wakes
up on the email and sends the order to the broker **Alpaca**.

## Contents

| File | What it has |
|---|---|
| [metodo/01-visao-geral.md](metodo/01-visao-geral.md) (in Portuguese) | Challenge rules, parts and architecture |
| [metodo/02-rotinas.md](metodo/02-rotinas.md) (in Portuguese) | The 7 routines of the day, one by one |
| [metodo/03-handoff.md](metodo/03-handoff.md) (in Portuguese) | Continuity: the handoff note between agents |
| [metodo/04-estrategista-executor.md](metodo/04-estrategista-executor.md) (in Portuguese) | Why he separated who thinks from who executes |
| [metodo/05-portoes-de-risco.md](metodo/05-portoes-de-risco.md) (in Portuguese) | Filters, risk/reward ratio and how they were loosened |
| [metodo/06-diario-7-dias.md](metodo/06-diario-7-dias.md) (in Portuguese) | What happened each day (reported numbers) |
| [metodo/07-licoes.md](metodo/07-licoes.md) (in Portuguese) | What can be learned — and why I wouldn't copy it |
| [templates/rotinas.yaml](templates/rotinas.yaml) (in Portuguese) | Routine schedule in configuration format |
| [templates/handoff.md](templates/handoff.md) (in Portuguese) | Handoff note template |
| [templates/prompt-rotina.md](templates/prompt-rotina.md) (in Portuguese) | Prompt template for each routine |
| [templates/recomendacao.json](templates/recomendacao.json) (in Portuguese) | Format of the strategist → executor email |

**There is no trading code in this repository.** The templates are for understanding the
architecture (or for testing on a **simulated account / paper trading**). If you experiment,
start there.

## Result, as reported

| | Final value |
|---|---|
| Agent system | ~$9,900 (≈ −1.0%) |
| Same $10,000 in the S&P 500 | ~$9,980 (≈ −0.2%) |
| Difference | the S&P won by ≈ 0.8 points |

The author's own conclusion: 7 sessions is too few to say whether the strategy works.

---

Study project from [INEMA.CLUB](https://inema.club) · open and free content.
