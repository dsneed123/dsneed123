<div align="center">

# Davis Sneed

### AI &amp; Full-Stack Engineer · Agentic Systems

**Seattle, WA**

<a href="https://www.dsneedy.com">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=21&pause=1200&color=7C3AED&center=true&vCenter=true&width=850&height=45&lines=Agents+that+plan%2C+act%2C+and+improve+themselves.;AWO+%C2%B7+self-improving+workflows+on+cyclic+graphs;Polling+agents+%C2%B7+autopilot+%C2%B7+local-first+LLMs;React+%2B+FastAPI+%2B+Postgres%2C+end+to+end.;Open+to+AI+%26+Full-Stack+roles+%E2%80%94+Seattle+or+remote." alt="Agents that plan, act, and improve themselves" />
</a>

<br/>

<a href="https://www.dsneedy.com"><img src="https://img.shields.io/badge/Portfolio-dsneedy.com-7C3AED?style=for-the-badge&logo=google-chrome&logoColor=white" alt="Portfolio"></a>
<a href="https://www.linkedin.com/in/dsneedy"><img src="https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
<a href="mailto:dlsneed1298@gmail.com"><img src="https://img.shields.io/badge/Email-Reach%20out-D14836?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"></a>
<img src="https://img.shields.io/badge/Seattle,%20WA-Open%20to%20work-16A34A?style=for-the-badge&logo=googlemaps&logoColor=white" alt="Seattle, open to work">

<img src="https://komarev.com/ghpvc/?username=dsneed123&style=flat-square&color=7C3AED&label=profile+views" alt="Profile views" />

</div>

---

## 👋 About

**AI and software engineer with 2+ years of professional experience** building agentic systems, full-stack applications, and AI infrastructure.

I work across the whole stack — React/Next.js front ends, Python services behind them, and the LLM orchestration, data pipelines, and evaluation in between. I currently work in **data operations for Amazon Personal Robotics**, running QA and validation on the operational data that feeds machine learning pipelines. Outside of that I co-founded **AWO** (*Agentic Workflow Orchestrator*) — a visual agent workflow builder with self-improving cyclic execution graphs and always-on polling agents.

<table>
<tr>
<td width="50%" valign="top">

**🤖 Agentic AI**
Cyclic workflow graphs · self-improvement loops · autopilot agents · tool use · model routing · token optimization

**🧱 Full-Stack**
React · Next.js · FastAPI · Django · Flask · PostgreSQL · Redis

</td>
<td width="50%" valign="top">

**🦾 Robotics & ML Data**
Robotics QA · AR/VR data collection · validation and labeling at scale

**🔐 Security-Minded**
Cyber Security concentration · cryptography · network analysis · secure by default

</td>
</tr>
</table>

---

## 🚀 AWO — Agentic Workflow Orchestrator · *Co-founder*
<sub>🔒 Private repository — walkthrough and demo available on request</sub>

> **AWO** is a visual builder and runtime for **self-improving agent workflows**. You compose agents on a graph canvas and AWO executes the graph — **cyclic graphs**, not just DAGs, so a workflow can loop back on itself, evaluate its own output, and re-run until the result clears the bar. Branching, parallel fan-out, long-lived **polling agents** that watch the outside world, and an **autopilot mode** where agents plan, execute, critique, and commit multi-step software tasks with no human in the loop.

```mermaid
flowchart LR
    T["⚡ Triggers<br/>push · poll-diff · schedule · webhook · manual"] --> B["🎛️ Workflow Builder<br/>visual graph canvas"]
    B --> E["🔁 Cyclic Execution Engine<br/>loops · branching · parallel"]

    E --> P["Plan"]
    P --> X["Execute"]
    X --> V["Evaluate"]
    V -->|"clears the bar"| S["✅ Commit / PR"]
    V -.->|"self-improvement loop"| P

    E --> C["🔌 Connector Layer"]
    C --> L["Local models<br/>Grace Blackwell"]
    C --> R["Cloud endpoints<br/>OpenAI · Anthropic compatible"]

    style B fill:#0EA5E9,stroke:#0369A1,color:#fff
    style E fill:#7C3AED,stroke:#5B21B6,color:#fff
    style V fill:#F59E0B,stroke:#B45309,color:#fff
    style S fill:#16A34A,stroke:#15803D,color:#fff
```

### What it actually does

<details open>
<summary><b>📡 Polling agents</b> — agents that watch instead of wait</summary>

<br/>

Most agent frameworks only run when you push a button. AWO's polling agents are **long-lived workers on a schedule** — they wake on an interval, look at a source, diff it against the last state they saw, and only spend tokens when something actually changed.

- **Poll-diff triggers** — an agent watches a repo, branch, endpoint, feed, table, or file and fires the workflow only on a real delta, so idle cycles cost nothing
- **Interval + cron scheduling** — per-agent cadence, from seconds-level polling to nightly sweeps, backed by a Redis-driven queue with **backoff on quiet sources** and jitter so pollers don't stampede
- **Cursor / watermark state in Postgres** — each poller remembers where it left off, so restarts resume instead of replaying, and the same change never triggers twice
- **Debounce and coalesce** — a burst of ten commits in a minute becomes one run against the final state, not ten competing runs
- **Fan-out on wake** — one poller can hand its delta to many downstream agents in parallel (review, test, doc, notify) as a single run

</details>

<details>
<summary><b>🔁 Cyclic execution engine</b> — loops are first-class</summary>

<br/>

- **Real cycles, not retries bolted on** — an edge can point backwards; the engine tracks visit counts, iteration budgets, and convergence conditions per loop
- **Plan → Execute → Evaluate → (loop or commit)** — the evaluator node scores its own output against the workflow's bar and decides whether to ship or send it back around with the critique attached
- **Guardrails** — max-iteration caps, wall-clock and token budgets, and stall detection so a workflow that stops improving exits instead of spinning
- **Conditional branching** — route on evaluator scores, tool results, or arbitrary predicates over run state
- **Parallel execution** — independent branches run concurrently and rejoin at a barrier node, with per-branch failure isolation

</details>

<details>
<summary><b>🤖 Autopilot</b> — multi-step software work, no human in the loop</summary>

<br/>

- Takes a task, **plans** the change set, **executes** against a real repo in an isolated workspace, **critiques** the diff, and iterates until it passes
- Runs tests and linters as evaluation signal — the loop is gated on real feedback, not the model's self-report
- Ends at a **commit or PR** with the run's reasoning trail attached

</details>

<details>
<summary><b>🎛️ Visual workflow builder</b> — compose instead of hand-wiring</summary>

<br/>

- **React Flow canvas** — drag agents, tools, evaluators, branches, and loop-backs onto a graph instead of writing orchestration glue
- **Typed ports and state passing** — outputs flow along edges as structured artifacts, so downstream agents get data rather than re-parsed prose
- **Live run view** — watch nodes light up as they execute, with per-node inputs, outputs, token spend, and latency
- **Run history and replay** — every execution is persisted, inspectable, and re-runnable from any node

</details>

<details>
<summary><b>🔌 Connector layer & model routing</b> — model-agnostic by design</summary>

<br/>

- **Local-first inference** on Grace Blackwell hardware, or any **OpenAI/Anthropic-compatible** endpoint — swappable per node
- **Per-node model routing** — cheap fast models for classification and polling triage, frontier models for planning and critique
- **Token optimization** — context trimming, artifact reuse across loop iterations, and caching so a self-improving cycle doesn't re-pay for the same context every pass
- **Tool use** — shell, HTTP, filesystem, and database tools exposed to agents with per-node scoping

</details>

<table>
<tr><td width="33%" valign="top">

**📡 Polling agents**
Long-lived watchers that wake on a schedule, diff against last-seen state, and only fire on real change.

</td><td width="33%" valign="top">

**🔁 Self-improvement loops**
Agents evaluate their own output and iterate — cycles are first-class, not an escape hatch.

</td><td width="33%" valign="top">

**🔌 Model-agnostic**
Local inference on Grace Blackwell or any OpenAI/Anthropic-compatible endpoint, routed per node.

</td></tr>
</table>

<div align="center">

<img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white">
<img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white">
<img src="https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white">
<img src="https://img.shields.io/badge/React%20Flow-FF0072?style=flat-square&logo=react&logoColor=white">
<img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white">

<a href="mailto:dlsneed1298@gmail.com?subject=AWO%20demo"><img src="https://img.shields.io/badge/Request%20an%20AWO%20demo-→-7C3AED?style=for-the-badge&logo=maildotru&logoColor=white" alt="Request an AWO demo"></a>

</div>

---

## 💼 Experience

<details open>
<summary><b>Quality Assurance Technician, Data Operations</b> — Amazon Personal Robotics <i>(via Apex Systems)</i> · <code>06/2026 – Present</code></summary>

<br/>

- Run structured QA testing on robotics systems, documenting performance metrics affecting accuracy, reliability, and usability
- Analyze, validate, and label operational data feeding ML pipelines — surfacing patterns and inconsistencies that improve training data quality
- Partner with engineering and operations teams to execute data collection protocols and support system validation
- Use Python scripting to support hardware-in-the-loop testing and data capture

</details>

<details>
<summary><b>Graduate Engineer / Site Lead</b> — Qualitest · Kirkland, WA · <code>02/2026 – 06/2026</code></summary>

<br/>

- **Site Lead** over a team of 5 data collectors across multiple locations, owning timelines, quality standards, and research protocol adherence
- Supported ML development for **humanoid robotics** programs, capturing and managing training data with AR/VR technology
- Maintained a **95%+ data pass rate** through rigorous QA review and data validation
- Resolved data inconsistencies with cross-functional research, engineering, and operations teams

</details>

<details>
<summary><b>Software Engineer</b> — PIVOT · <code>09/2025 – 01/2026</code></summary>

<br/>

- Created high-fidelity UI designs in Figma and shipped responsive features in JavaScript, HTML, and CSS
- Integrated front-end components with a **Python/Django + PostgreSQL** backend, writing SQL to power dynamic data rendering

</details>

<details>
<summary>🏆 <b>Scrum Master & Full-Stack Developer</b> — R7D LLC <i>(SpaceX vendor)</i> · <code>09/2024 – 05/2025</code></summary>

<br/>

- Led a year-long capstone as **Scrum Master**, coordinating a team of 4 with Git, GitHub Projects, and Agile workflows
- Built a timeline visualization web app in **React, Next.js, Python, and PostgreSQL** — drag-and-drop interactions, dynamic visualizations, and SQL-backed models for real-time event correlation
- 🏆 Awarded **Best Senior Design Computer Science Project**, Gonzaga School of Engineering & Applied Sciences, 2025

</details>

---

## 🛠️ Featured Projects

| Project | What it is | Stack |
|:---|:---|:---|
| 🤖 **[TARS](https://github.com/dsneed123/TARS)** | Autonomous coding agent — *Task Automation & Repository Steward*. Plans, writes, and ships code end to end against real repos. | `Python` `Claude API` |
| 🐘 **[elephant-dashboard](https://github.com/dsneed123/elephant-dashboard)** | Real-time trading dashboard — stocks, crypto, and Kalshi signals with live charts, targets, and stop-losses. | `TypeScript` `Python` |
| 🏃 **[athlete-vision](https://github.com/dsneed123/athlete-vision)** | 40-yard-dash biomechanical analysis: pose estimation, stride metrics, movement-optimization datasets. | `Python` `CV/ML` |
| 🌐 **[packet-mapper](https://github.com/dsneed123/packet-mapper)** | Web-based packet sniffer that maps live network connections onto a world map. | `Python` `networking` |

<details>
<summary><b>📂 More public projects</b> — security tooling, ML, and product builds</summary>

<br/>

| Project | What it is | Stack |
|:---|:---|:---|
| **[InvisiMark](https://github.com/dsneed123/InvisiMark)** | Invisible watermarking service binding ownership metadata to images to trace unauthorized sharing. | `Python` `cryptography` |
| **[shamir_secret_sharing](https://github.com/dsneed123/shamir_secret_sharing)** | Threshold cryptography — split a secret into shares that require a quorum to reconstruct. | `Python` `cryptography` |
| **[intrigue](https://github.com/dsneed123/intrigue-)** | PyTorch model trained on public social data to predict view/like counts and rate content virality. | `PyTorch` |
| **[resume-optimizer](https://github.com/dsneed123/resume-optimizer)** | Single-page resume builder with ATS optimization, import/export, and fine-grained typography control. | `Python` |
| **[elephant](https://github.com/dsneed123/elephant)** | Kalshi prediction-market copy-trading platform — track top bettors, analyze performance, mirror trades. | `Python` |
| **[bucket-budget](https://github.com/dsneed123/bucket-budget)** | Personal finance manager — bucket budgeting, purchase ranking, savings goals, spending insights. | `Python` |

</details>

<details>
<summary><b>🔒 Private work</b> — available to walk through on request</summary>

<br/>

| Project | What it is | Stack |
|:---|:---|:---|
| **AWO** | *Agentic Workflow Orchestrator* — polling agents, self-improving cyclic execution graphs, and autopilot *(see above)*. | `FastAPI` `Postgres` `Redis` `React Flow` |
| **stock-signal-scanner** | Self-hosted scanner: ingests financial news, runs a local LLM analysis engine, surfaces per-ticker signal cards. | `Go` `Python` `Docker` |
| **TARS-Lite** | TARS running fully local on Ollama — no cloud, no API keys. | `Python` `Ollama` |
| **crypto-trading-bot** | Autonomous crypto trading bot with a GUI dashboard and no external API-key dependency. | `Python` `Docker` |

</details>

---

## ⚙️ Tech

<div align="center">

**Languages**

<img src="https://skillicons.dev/icons?i=python,ts,js,go,rust,cpp,postgres&theme=dark" alt="Languages" />

**Frameworks & Data**

<img src="https://skillicons.dev/icons?i=react,nextjs,fastapi,django,flask,nodejs,redis,sqlite,firebase&theme=dark" alt="Frameworks" />

**AI & Infrastructure**

<img src="https://skillicons.dev/icons?i=aws,docker,linux,git,github,figma,pytorch&theme=dark" alt="Infra" />

<br/>

<img src="https://img.shields.io/badge/Claude%20API-D97757?style=flat-square&logo=anthropic&logoColor=white">
<img src="https://img.shields.io/badge/OpenAI%20API-412991?style=flat-square&logo=openai&logoColor=white">
<img src="https://img.shields.io/badge/Ollama-000000?style=flat-square&logo=ollama&logoColor=white">
<img src="https://img.shields.io/badge/LLM%20Orchestration-7C3AED?style=flat-square">
<img src="https://img.shields.io/badge/Workflow%20Automation-16A34A?style=flat-square">
<img src="https://img.shields.io/badge/DigitalOcean-0080FF?style=flat-square&logo=digitalocean&logoColor=white">

</div>

---

## 📊 GitHub

<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github-profile-summary-cards.vercel.app/api/cards/profile-details?username=dsneed123&theme=github_dark">
  <img src="https://github-profile-summary-cards.vercel.app/api/cards/profile-details?username=dsneed123&theme=github" width="90%" alt="Profile summary" />
</picture>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github-profile-summary-cards.vercel.app/api/cards/repos-per-language?username=dsneed123&theme=github_dark">
  <img src="https://github-profile-summary-cards.vercel.app/api/cards/repos-per-language?username=dsneed123&theme=github" height="200" alt="Repos per language" />
</picture>
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github-profile-summary-cards.vercel.app/api/cards/most-commit-language?username=dsneed123&theme=github_dark">
  <img src="https://github-profile-summary-cards.vercel.app/api/cards/most-commit-language?username=dsneed123&theme=github" height="200" alt="Most committed languages" />
</picture>

</div>

### 📈 Contributions per year

<div align="center">

<img src="https://img.shields.io/badge/Total%20contributions-3,943-7C3AED?style=for-the-badge" alt="Total contributions">
<img src="https://img.shields.io/badge/Average%20per%20year-789-0EA5E9?style=for-the-badge" alt="Average per year">
<img src="https://img.shields.io/badge/2026%20pace-~4,800%2Fyr-16A34A?style=for-the-badge" alt="2026 pace">

</div>

<div align="center">
<sub>Averaged across 2022–2026 · 2026 is year to date, running at roughly <b>4,800/yr</b></sub>
</div>

---

## 🎓 Education

**B.A. Computer Science & Computational Thinking** — Gonzaga University, Spokane, WA · *May 2025*
Concentrations in **Cyber Security**, **Software Development**, and **Philosophy**

🏆 Winner — School of Engineering & Applied Sciences **2025 Best Senior Design Computer Science Project** *(timeline visualization capstone with R7D LLC)*

---

## 📬 Currently

- 🔭 Building **AWO** — polling agents and self-improving agent workflows with real autopilot — and **TARS**, an agent that takes a task and ships the PR
- 🌱 Going deeper on agent evaluation, model routing, and local-first inference
- 💬 Ask me about agentic workflows, LLM tool use, ML data pipelines, or application security
- ⚡ Fun fact: most of my side projects were built *by* agents I wrote

<div align="center">

<br/>

### Let's build something.

<a href="mailto:dlsneed1298@gmail.com"><img src="https://img.shields.io/badge/dlsneed1298@gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"></a>
<a href="https://www.linkedin.com/in/dsneedy"><img src="https://img.shields.io/badge/linkedin.com/in/dsneedy-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
<a href="https://www.dsneedy.com"><img src="https://img.shields.io/badge/dsneedy.com-7C3AED?style=for-the-badge&logo=google-chrome&logoColor=white" alt="Portfolio"></a>

<sub>Built by an engineer who ships — and by the agents he builds.</sub>

</div>
