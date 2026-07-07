# Scott McGuire

Quantitative researcher, software engineer, and hands-on engineering
manager — ~20 years in financial markets, currently at Clearwater
Analytics working on Beacon Platform, where I'm part house quant, part
quant translator, part quant dev. Nobody appointed me to lead AI adoption;
it happened anyway — Claude Code sessions for three teams so far, and a
setup guide that gets passed around on its own. Physics PhD before that.

Lately experimenting and writing about getting the most out of
AI: measuring whether multi-model setups beat single models, harnesses
for directing several models at once, and (planned) write-ups of what worked
and what didn't. (Negative results are results.)

**Writing:** [writingcommitmentdevice.substack.com](https://writingcommitmentdevice.substack.com)
- I have amassed a lot of stuff that I've been telling myself I _should_ write up. This is my attempt to make myself do it.
- First post: multi-model code review: If a model writes code or creates another kind of artifact, will review by other models with different lineages find more bugs than reviews by the same model or models in the same lineage? And, for smaller/weaker models, do they do better if asked to just point to potential bugs/errors without trying to explain or suggest fixes?

**One thread through these repos.** Last October I was running multi-model
conversations by hand — copying and pasting between chat interfaces. I tried
automating that as a Claude Artifact and hit the browser sandbox: every
non-Anthropic API call died on CORS. So I went where the sandbox wasn't and
built [MultiModelChat](https://github.com/abstractionlair/MultiModelChat) — a
working multi-model web chat, in daily use within a week. When Gemini 3 and
Antigravity launched in November, I turned the same idea into a controlled
experiment: re-specified the app as a vision doc and nine feature specs, handed
the identical pack to five coding agents independently, and compared the builds:
[one-spec-five-agents](https://github.com/abstractionlair/one-spec-five-agents)
— the spec, all five builds, the comparison study, and the story of how the
experiment was recovered and evaluated. What the builds taught me went into a
re-specified v2 within days. And in December, wanting a permanent home for
work like this — the Artifact CORS failure was, in my own words at the time,
the first input to the thinking — I got a VPS and built
[claude-hub](https://github.com/abstractionlair/claude-hub): instead of making
the chat page do the work, give every chat client a door to a persistent,
tool-equipped backend. The instruments further down this page — the work
graph, the multi-model review engine, the dev workflow — grew out of managing
exactly this kind of work at AI speed.

**Selected repos:**

- [claude-hub](https://github.com/abstractionlair/claude-hub) — the hub of my
  personal AI infrastructure: one authenticated door from any chat client to a
  persistent, tool-equipped Claude Code backend (OAuth 2.1 + PKCE + TOTP at the
  boundary; 679 tests). The pieces I use hardest: the work graph — which tracks
  what *I* need to do across many concurrent AI-assisted threads, with models
  helping maintain it and often executing from it — a persistent-session bridge,
  a multi-model review engine that grades its own reviewers against a
  failure-mode taxonomy, and an artifact store with semantic search.
- [one-spec-five-agents](https://github.com/abstractionlair/one-spec-five-agents)
  — a controlled comparison of five AI coding systems handed one identical,
  fully specified project. Findings: agents complete the documented plan, not
  the spec inventory; same model under different harnesses diverges materially;
  self-reported completion runs backwards to competence. Includes the builds,
  the study, and a first-person account (Claude's) of how the forgotten
  experiment was recovered and evaluated.
- [model-collaboration-study](https://github.com/abstractionlair/model-collaboration-study)
  — pre-registered experiment: do collaboration structures (debate, peer
  review, fusion) beat a single model at fixed budget? Typed IR for protocol
  composition; power analysis before kickoff.
- [dev-workflow](https://github.com/abstractionlair/dev-workflow) — a
  distilled, importable process for spec-driven development with multi-model
  review gates: Vision → Scope → Roadmap → Spec → Skeleton → Tests →
  Implementation, each stage gated by independent model reviewers. The far
  end of an arc of coordination experiments — giving models email to message
  each other (MultiModelCLIEmail), then a CLI harness — reasoned through in
  [dev_workflow_meta](https://github.com/abstractionlair/dev_workflow_meta)
  (why conversation-driven agent work degrades as a project grows) and
  distilled here into a process that deliberately drops message-passing for
  shared files and roles.
- [prediction-markets](https://github.com/abstractionlair/prediction-markets)
  — research and trading infrastructure for prediction markets: an estimator
  framework built for temporal integrity (no look-ahead at the estimator
  interface, by construction), calibration studies against market outcomes,
  backtests, and a live trading loop.
- [airproject](https://github.com/abstractionlair/airproject) — the
  ur-ancestor (2024): a multi-model, tool-using CLI coding assistant built
  *before Claude Code existed*, measured against Claude Projects — where it
  fell short, and where its diagnosis (ambient context was the missing piece)
  held up. The one repo here I wrote and debugged by hand; the baseline the
  rest of this list's delegation is measured against.
- [quant-ingestion-and-simulation](https://github.com/abstractionlair/quant-ingestion-and-simulation)
  — state-space framework where ingestion is inverse simulation: one
  ModelSpec drives Kalman filtering, multi-asset Monte Carlo, and
  historical-VaR correlation shocks.
- [cai-constitution-bootstrap](https://github.com/abstractionlair/cai-constitution-bootstrap)
  — automated Constitutional AI training pipeline experiment.
- [vector-space-generation](https://github.com/abstractionlair/vector-space-generation)
  — exploring language-model generation in continuous vector space. A negative
  result published with its raw outputs — and with the review-found bugs that
  bound what the negative result can claim.

- [claude-college](https://github.com/abstractionlair/claude-college) —
  conversation-native Socratic tutoring system (mastery gates, spaced
  repetition), with a real sample session included.
- [claude-camp](https://github.com/abstractionlair/claude-camp) — interview
  prep pairing chat-Claude orchestration with Claude Code problem
  generation and critique.

- [MultiModelChat](https://github.com/abstractionlair/MultiModelChat) —
  multi-model web chat: one conversation, several frontier models, with
  projects, file context, and full-text search. **Try it live:**
  [chat.abstractionlair.xyz](https://chat.abstractionlair.xyz) (a public
  sandbox running cheap models, with cost controls). Code-execution phase
  specced, not started.

- [portfolio-tool](https://github.com/abstractionlair/portfolio-tool) — an
  experiment in pure "vibe coding": how far could I get letting the models
  write essentially all of it, hands off the wheel? Far enough to be
  interesting, not far enough to be how I work. Independent model reviews
  found the financial math held up but the engineering around it didn't —
  and the multi-model review infrastructure I built since kept catching real
  bugs that vibe-coding alone had left in. The README says so plainly.

The unifying question: how much of software development — and knowledge
work generally — can one person responsibly delegate to models, and how do
you instrument the answer instead of guessing at it?
