# Scott McGuire

Quantitative researcher, software engineer, and hands-on engineering
manager — ~20 years in financial markets, currently at Clearwater
Analytics working on Beacon Platform, where I'm part house quant, part
quant translator, part quant dev. Nobody appointed me to lead AI adoption
but it happened anyway: Claude Code sessions for three teams so far, and a
setup guide that gets passed around on its own. Physics PhD before that.

Lately I've been experimenting with ways to get the most out of
AI. In particular with trying to figure out how to delegate as much as possible
to models while maintaining confidence in the quality and correctness of the results.
One common theme is using multiple, _different_ models to check each other and
cover blind spots. And I try my best to record both what worked and what didn't.
(Negative results are results.)

Much of what's here was written using these techniques. Code, natural language documents, everything.
Aside from one experiment really leaning into vibe coding, which wasn't satisfactory (but wait until
next year), these are high-engagement on my part. But with my contributions being more like what I've done
as a manager or a coach, or what I've seen good PhD advisors do. Vision, spec, and other documents are written
by the models but after long conversations including my close reading of drafts and providing detailed feedback,
etc. Most artifacts, docs and code included, get reviewed by a different model than authored them and those 
reviews also tend to spark more rounds of conversation.

In July 2026, while I had access to Claude Fable 5 through my Anthropic subscription, I applied these techniques
(among others) to all my existing repos. I am very happy with how this went and it is the reason for the flurry
of changes all at once.

## Writing

[writingcommitmentdevice.substack.com](https://writingcommitmentdevice.substack.com)
- I have amassed a lot of stuff that I've been telling myself I _should_ write up. This is my attempt to make myself do it.
- First post: multi-model code review: If a model writes code or creates another kind of artifact, will review by other models with different lineages find more bugs than reviews by the same model or models in the same lineage? And, for smaller/weaker models, do they do better if asked to just point to potential bugs/errors without trying to explain or suggest fixes?

## Repos

### An arc through some of these repos

Last October I was running multi-model
conversations by hand — copying and pasting between chat interfaces. At some point
I heard that Claude, in the web interface, had gotten good at writing web apps
as artifacts so I asked it in a new conversation to automate this by writing a simple
web app accessing models via API. For a moment it appeared to have worked but
I soon found that it could only call the Anthropic API; others hit CORS issues.
However, it did demonstrate that current models knew how to write the correct code and that
inspired [MultiModelChat](https://github.com/abstractionlair/MultiModelChat) — a
working multi-model web chat that I could run from my machine. It was actually useful;
I used it to have some substantial conversations with a Claude, a GPT, a Gemini, and a Grok,
IIRC. (Somewhat expensive though.)
When Gemini 3 and Antigravity launched in November, I turned the same idea into an
experiment.  With AI help, I wrote a detailed spec and other docs descrining the app I wanted
five coding model and harness combinations to reimplement it in one go, and compared the builds:
[one-spec-five-agents](https://github.com/abstractionlair/one-spec-five-agents).
That repo containts the spec, all five builds, the (much more recent) comparison study, and the
story of how I forgot I'd run the experiment how it got recovered and evaluated.
In December, I realized I could both give a permanent home to apps like this and work around
the CORS issue and similar issues (which I may have just been assuming existed based on extrapolation)
by geting a VPS and giving Claudes in the web app access to it via MCP. That led to
[claude-hub](https://github.com/abstractionlair/claude-hub). This became my general dev box, and the home
of multiple AI-backed or AI-helping services. Much of what's below, the work
graph, the multi-model review engine, the dev workflow, grew out of managing
this kind work. It was also a playground for testing ideas I would later use in my day job.
It's not a Claw but there are some simmilarities.

### Selected repos

Some completed projects, some ongoing.

- [claude-hub](https://github.com/abstractionlair/claude-hub): the hub of my
  personal AI infrastructure: one authenticated door from any chat client to a
  persistent, tool-equipped Claude Code backend (OAuth 2.1 + PKCE + TOTP at the
  boundary; 679 tests). The pieces I use hardest: the work graph — which tracks
  what *I* need to do across many concurrent AI-assisted threads, with models
  helping maintain it and often executing from it — a persistent-session bridge,
  a multi-model review engine that grades its own reviewers against a
  failure-mode taxonomy, and an artifact store with semantic search. (The work
  graph is pretty new but I'm very happy with how it's going.)
  
- [one-spec-five-agents](https://github.com/abstractionlair/one-spec-five-agents):
  a controlled comparison of five AI coding systems handed one identical,
  fully specified project. Findings: agents complete the documented plan, not
  the spec inventory; same model under different harnesses diverges materially;
  self-reported completion runs backwards to competence. Includes the builds,
  the study, and an account of how the forgotten experiment was recovered and evaluated.
  The fact that I had forgotten about this and Claude ended up explaining to me what
  I'd done (based on the code, mining logs, ...) gave me the idea of having this one
  written up in a novel way: First person from Claude's perspective.
  
- [model-collaboration-study](https://github.com/abstractionlair/model-collaboration-study):
  a pre-registered experiment: do collaboration structures (debate, peer
  review, fusion) beat a single model at fixed budget? Typed IR for protocol
  composition; power analysis before kickoff.
  
- [dev-workflow](https://github.com/abstractionlair/dev-workflow): a
  distilled, importable process for spec-driven development with multi-model
  review gates: Vision → Scope → Roadmap → Spec → Skeleton → Tests →
  Implementation, each stage gated by independent model reviewers. The far
  end of another arc of experiments: first giving models email to message
  each other ([MultiModelCLIEmail](https://github.com/abstractionlair/MultiModelCLIEmail)),
  then a CLI harness. The lesson — conversation-driven agent work degrades
  as a project grows — is reasoned through in
  [dev_workflow_meta](https://github.com/abstractionlair/dev_workflow_meta)
  and distilled here into a process that deliberately drops message-passing
  for shared files and roles.
  
- [prediction-markets](https://github.com/abstractionlair/prediction-markets):
  a research and trading infrastructure for prediction markets: an estimator
  framework built for temporal integrity (no look-ahead at the estimator
  interface, by construction), calibration studies against market outcomes,
  backtests, and a live trading loop.
  
- [airproject](https://github.com/abstractionlair/airproject):
  my first step going beyond chat (2024): an attempt at a multi-model, tool-using CLI coding assistant,
  inspired by Claude Projects and groping towards what Claude Code eventually delivered.
  It fell short, but writing it and learning why it fell short was very educational.
  This is the one repo on this short list that I wrote and debugged significantly by hand.
  I'd ask a model, usually Claude, in the chat interface to write parts or tell
  me how an API worked, ... then copy it into the code, try it, fix things. But I
  had the sense, and this was the project's motivation, that the models _could_
  just write this stuff if given the right infrastructure, tools, etc. 
  
- [quant-ingestion-and-simulation](https://github.com/abstractionlair/quant-ingestion-and-simulation):
  state-space framework where ingestion is inverse simulation: one
  ModelSpec drives Kalman filtering, multi-asset Monte Carlo, and
  historical-VaR correlation shocks.
  
- [automated-post-training](https://github.com/abstractionlair/automated-post-training):
  an automated post-training experiment inspired by Constitutional AI: generating
  training data by smart-prompting base models, with contamination guards and
  hard validity gates. Its headline early result was invalidated by its own
  in-repo review — and both the result and the invalidation are preserved,
  which is the part I'd want a reader to see. (I think I, plus newer models,
  could make this work today.)
  
- [vector-space-generation](https://github.com/abstractionlair/vector-space-generation):
  exploring language-model generation in continuous vector space. A negative
  result published with its raw outputs — and with the review-found bugs that
  bound what the negative result can claim.

- [claude-college](https://github.com/abstractionlair/claude-college):
  conversation-native Socratic tutoring system (mastery gates, spaced
  repetition), with a real sample session included.
  
- [claude-camp](https://github.com/abstractionlair/claude-camp): interview
  prep pairing chat-Claude orchestration with Claude Code problem
  generation and critique.

- [MultiModelChat](https://github.com/abstractionlair/MultiModelChat):
  multi-model web chat: one conversation, several frontier models, with
  projects, file context, and full-text search. **Try it live:**
  [chat.abstractionlair.xyz](https://chat.abstractionlair.xyz) (a public
  sandbox restricted to cheap models, with cost controls). Code-execution phase
  specced, not started. (TUI harnesses like Claude Code and Codex plus the multi-model
  interaction tools on claude-hub now fill the role this would have filled.)

- [portfolio-tool](https://github.com/abstractionlair/portfolio-tool): an
  experiment in pure "vibe coding": how far could I get letting the models
  write essentially all of it, hands off the wheel? Far enough to be
  interesting, not far enough to be releasable. Independent model reviews
  found the financial math held up but the engineering around it didn't —
  and the multi-model review infrastructure I built since kept catching real
  bugs that vibe-coding alone had left in. The README explains.

A unifying question: how much of software development — and knowledge
work generally — can you responsibly delegate to models, and when you do,
how do know the results are good?
