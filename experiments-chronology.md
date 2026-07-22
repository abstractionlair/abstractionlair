# Experiments Chronology

I see most of the projects captured in the repos in this account as
experiments.  But experiments in the research _and_ development sense.
Some are purely to learn something, just the "research" side.  In
those cases, getting any result, positive or negative is a success.
Negative results are results.  Some, but not many, are close to pure
development, though none are really, purely that.  For those, there
was something I believed would be useful and I believed I could
implement.  When that doesn't happen, those projects can be properly
called failures.  Most projects are a mix of both.  "I wonder if <x\>
would be useful and if I could make it happen by doing <y\>."  Those
need to be judged as a category. Success doesn't require every project
to be useful, it just requires useful things to be spun out at a
sufficient frequency.  And the bonus of learning while making good
stuff. Note that many projects end when it becomes clear (or at least
pretty likely) that they aren't going to pay off.

Success criteria defined, I wanted to know if the whole sequence, my
experimental program (if that's not too grandiose), was a success.
For different purposes I had recently collected exports of my
conversations with AI assistants and logs from agentic coding sessions
to be analyzed with heavy use of AI.  It seemed natural to also
analyze this question that way, adding my repos and their history to
the corpus. Unfortunately nothing in that can distinguish, without
some guesswork at least, which projects were pure exploration, which
ones were meant to provide a real answer to a real question, and which
were meant to produce useful software. The results of that analysis,
written by Claude, are below.

One thing about the timing is partly evident here, and even more
evident in the Git logs.  Agentic coding tools allowed me (and plenty
of other people) to spin up lots of projects quickly, and to move them
forward quickly.  But I don't think the two effects are symmetrical,
which opens the door to letting the number of started but not finished
projects spiral.  And I felt that happening to me.  (In Nov 2025 I
increased the number on purpose to see what the limit was. It is, of
course, dependent on tooling and models, not just me and my
workflow. But aside from then, it happened unintentionally.) So in
June of this year (2026 as I write) I decided to clamp down on my work
in progress. Several started projects that I _don't_ consider done are
on hold. I am experiencing a sequence of gratifying feelings, like
crossing things off lists.


*Cutoff: entries cover 2024-08 through 2026-07-15, when this chronology was compiled.
The repos have kept moving since; where an entry says "never" or "ever," it speaks
through the cutoff.*

**Legend**
- Not every project named below has a public repo — some are private or not yet
  published. Entries report the experiment either way.
- `RESULT:` reflects whether the specific thing tried worked, not whether anything useful
  was learned — negative results taught plenty; that symmetry is the point of the framing.
  POSITIVE / NEGATIVE / MIXED / ONGOING.
- `[FIRST-HAND]` = Scott's own words or actions show him doing the technical/intellectual
  act directly. `[SUPERVISED]` = a model executed under his direction — claimed as
  direction/oversight, never as personal execution. `[INDETERMINATE]` = the record doesn't
  resolve who did what.
- Dates are month-precision except where a specific day matters. No date below is marked
  "~" — where a source hedged a date, that hedge is written into the entry text instead.
- In the private working record, every entry carries evidence pointers (file + section)
  into the underlying research notes. Those notes are private, so the pointers are removed
  from this published version; the private record retains them. Quotes are verbatim from
  that record, typos preserved.
- Never-built designs are not claimed as builds; where a run happened but its *result*
  isn't citable (e.g. training outcomes), the entry claims the run, not a working model.

**Attribution and verification**
- The dated entries below were drafted by AI agents (2026-07-14) from a reviewed corpus
  record, under Scott's direction; the framing prose — the preamble above — is Scott's
  own.
- Creator≠reviewer discipline applies throughout: no model reviews or audits its own
  output.
- One example: a stance-strength audit of this document by a different model lineage
  (OpenAI's Codex agent running gpt-5.6-sol, 2026-07-15) compared every narrator
  sentence attributing a position to Scott against its source wording. Scott requested
  that audit himself — his concern was that compression tends to restate his hedged
  positions as confident ones. Its four confirmed findings of overstated calibration
  were corrected in this version (2026-07-19); they're noted here, rather than silently
  applied, because they originated from his feedback.
- Publication staging (fix application, privacy scrub, this note) by Claude (Fable 5),
  2026-07-19.

---

## 2024

- **2024-08 — airproject: founding + day-two cross-model review** — Built a CLI coding-agent
  MVP (`click` CLI, a marker file, CRUD file tools, a manual tool loop against
  `claude-3-opus`) and, one day after founding, brought the actual code and a sample
  transcript to a different vendor's model for review rather than asking Claude to review
  its own output ("Since you are different from Claude, I wonder if you can analyze the
  code... without being influenced in that way") — RESULT: MIXED — the cross-model review
  caught a real design gap (no termination guard on the recursive tool loop) before the
  code shipped, but static analysis of the first commit shows the core Anthropic tool-use
  plumbing was never functional in this or any later version — [FIRST-HAND design/review
  choice, SUPERVISED build]

- **2024-09 — airproject: SDK-mismatch bug, correct fix drafted, never committed** — Hit and
  diagnosed a real crash against the live Anthropic API (`AttributeError: 'ToolUseBlock'
  object has no attribute 'text'`); with a real object repr in hand, the correct one-line
  fix (`content_block.name` / `content_block.input`) was worked out and verified in
  conversation — RESULT: NEGATIVE — the correct fix was never committed; five days later a
  different, wrong attribute-access guess landed instead and the file was byte-identical
  from that commit onward through this chronology's cutoff (in July 2026, after the
  cutoff, the 2024 draft fix was finally landed and the round trip completed) — [FIRST-HAND diagnosis,
  SUPERVISED (the fix that shipped)]

- **2024-09 — airproject: the OpenAI-side bootstrap actually ran** — Started a second,
  deliberately minimal, self-editing tool from scratch on the OpenAI side after the
  Claude-side path stalled, debugging it hands-on ("This is how we should convert to json:
  json.dump(message.model_dump(), file)" — his own fix, not the model's) — RESULT: MIXED —
  this is the only path in the whole project demonstrated, by real non-git output files, to
  genuinely read and write files through the live loop — a read of its own source (the
  design was explicitly self-targeting) and a write to test_file.txt with the file's mtime
  matching the logged event to the second; the one self-revision it produced stayed in the
  assistant's message and was never written; never merged with the (broken) Claude-side
  tool, and no message anywhere in the record claims it "fully works" — [FIRST-HAND
  debugging, SUPERVISED build] — (this entry reflects a dated correction, 2026-07-14, to an
  earlier internal analysis of the same events)

- **2024-10 — airproject: wind-down** — In the same weeks the project's multi-model ambition
  remained unmet, evaluated purpose-built coding tools (Cursor, GPT Canvas) and stated "I
  plan to use Cursor" as work on the hand-built tool tapered off — RESULT: NEGATIVE — no
  committed state of the tool, at any point through this chronology's cutoff, had correct
  tool-use plumbing (the repair finally landed in July 2026); no explicit "I'm stopping" statement exists in the record, it just goes quiet —
  [FIRST-HAND] — (a later reassessment named the missing piece as ambient/ongoing context
  management — which is what the window-file system, below, solved roughly 18 months later)

---

## 2025

- **2025-08 — claude-camp: two-agent orchestrator/worker contract** — Built a chat-Claude
  (plans) / Claude-Code (executes) handoff protocol with grading-style feedback —
  RESULT: MIXED — one real, specific graded session exists on record (a two-pointers
  problem, concrete non-generic feedback), but the project was used once and captured
  rather than iterated into a running practice — [SUPERVISED]

- **2025-09 — claude-college: Socratic/mastery-gated tutoring system** — Defined an AI
  tutoring agent entirely through project instructions (calibration questions, mastery
  gates, spaced repetition) — RESULT: MIXED — one real 1,598-line transcript
  shows the Socratic teaching genuinely working (a live derivation of the attention
  mechanism), but the first mastery gate false-passed: immediately after it certified the
  full-architecture material, the student's next message revealed a misconception about
  the MLP wiring — content inside the gate's own certified scope — which the session then
  caught and resolved; the project went essentially dormant —
  [FIRST-HAND prompt/system-instruction design, SUPERVISED sessions]

- **2025-09 — vector-space-generation: continuous-space generation replication** — Tried to
  reproduce concept-token / continuous-concept-space generation ideas (COCONUT, "Soft
  Thinking") — RESULT: NEGATIVE, cleanly bounded — two real, code-verified bugs (a
  double-position-embedding error; a `generate()` output-slice that discarded the real
  generated tokens) invalidated the generation-based results; the writeup explicitly scopes
  which conclusions survive the bugs and which don't — [SUPERVISED build, FIRST-HAND
  scoping of what still stands]

- **2025-09/10 — automated-post-training v1: DPO stage blocked** — Attempted a DPO training
  stage as part of a "use a model to train that same model" experiment inspired by
  Constitutional AI — RESULT: NEGATIVE — blocked outright by TRL/library API-compatibility
  errors ("Status: Unresolved — blocking DPO training"), never completed in this or any
  later iteration; superseded by a "V2 Clean Restart" — [SUPERVISED]

- **2025-10 — automated-post-training v2: Stage-1 SFT run + self-invalidation** — Ran a real
  LoRA SFT training run (1,368 steps, loss 1.67→0.59) — RESULT: MIXED — the run itself
  completed and is real, but a broken length heuristic in the evaluation manufactured a
  fake 81%→99.3% "improvement"; hand-rescoring found the true effect was −0.7%
  (McNemar p=2e-12). The honest claim is a completed run that caught and reported its own
  null, not a working model — [SUPERVISED build, FIRST-HAND in reframing the project around
  the self-invalidation as the actual finding]

- **2025-10 — MultiModelChat, stage 1: the CORS failure** — Tried to build a multi-model
  chat utility as a Claude Artifact using personal API keys — RESULT: NEGATIVE — every
  non-Anthropic call failed ("Anthropic worked. Rest got 'Error: Failed to fetch'" — a CORS
  failure from the artifact-hosting domain) — led him to say, "I think I'd like to continue
  working this with you, but in the Claude Code environment where we could deal with the
  CORS issue"; the idea subsequently moved into a real, separately-hosted app — [FIRST-HAND]

- **2025-11 — MultiModelChat: built and used** — Built a real Node/Express multi-provider
  chat app (SQLite+FTS5 search, OpenAI/Anthropic/Google/xAI adapters) — RESULT: POSITIVE —
  genuinely used daily ("The current version is quite functional... We've had multiple,
  fruitful conversations in it"); later hardened with a public-mode guard and a fixed
  hallucination bug where weak models fabricated other agents' bracketed replies —
  [SUPERVISED build, FIRST-HAND direction]

- **2025-11 — MultiModelChat spec dispatched to five independent agent lineages in
  parallel** — Sent the same written spec to five different coding-agent lineages (Claude
  Code/Sonnet 4.5, Codex, Factory Droid, Gemini, Antigravity) to see how differently each
  would build the identical thing — RESULT: ONGOING (at the time) — the resulting five
  codebases and a comparison writeup sat unexamined in an archive for roughly eight months
  before anyone analyzed them (see 2026-07 below) — [SUPERVISED]

- **2025-11 — MultiModelCLIEmail: real multi-vendor coordination over a shared mailbox** —
  Gave four different models/harnesses (Claude, GPT-5, Gemini, Grok) a shared Maildir to
  coordinate on a task. No mail is ever sent: Maildir here is a message *format* on local
  disk — the agents write and read files in a project directory, with no mail server and no
  network — RESULT: POSITIVE, with honest warts — roughly 37 hours of real
  traffic, 1,499 committed messages; the warts (models dropping out of the loop, needing to
  be re-prompted to rejoin) were kept as dated evidence rather than edited out —
  [SUPERVISED]

- **2025-11 — quant-ingestion-and-simulation, mcp-tool-gateway, multi-agent-harness,
  uniform-k-compression all founded within days of each other** — RESULT: MIXED —
  quant-ingestion-and-simulation became a numerical-methods project with real tests on its
  core contracts (model spec, driver layout, exposure mapping);
  multi-agent-harness shipped real CI machinery (lint/mypy/pytest matrix, Codecov) that then
  failed every single run for the next eight months (2025-11-14 through 2026-07-13, 6/6 red)
  — [SUPERVISED]

- **2025-11 — the founding burst itself, as a meta-experiment** — Four repos in days
  doubled as a test of how many AI-assisted projects could run simultaneously, at the
  time — RESULT: MIXED (Scott-confirmed 2026-07-19) — founding in parallel worked;
  sustained parallel *maintenance* didn't (one strong project, one 8-months-red CI, two
  drifted) — [SCOTT-FRAMING, 2026-07-14: "should we partly judge that as testing the
  possibility of running that many things simultaneously? (At the time.) Not instead of
  the individual grades; they are what they are. But in addition."] [SCOTT, 2026-07-19,
  confirming: "I think in the sense that with the right intertive tooling and workflow
  improvements that level of parallelism would work."] — (entry added at
  Scott's direction; graded from the four sibling entries above)

- **2025-12 — claude-hub: genesis** — Named two explicit inputs (the CORS failure above, and
  ChatGPT's Pulse scheduling feature) and proposed a persistent server-side Claude Code
  instance that chat-Claude instances could message directly — RESULT: POSITIVE — a VPS was
  shopped and stood up within days of the founding turn; the first live connector test
  landed 2025-12-29, roughly 100 minutes after the proposal turn that led to the first
  commit — [FIRST-HAND design, SUPERVISED build]

---

## 2026 — January to June

- **2026-01 — Real-money prediction-market trading begun** — Scott said on 2026-01-13, "I'd
  really like to investigate widely and then let you trade," with seed money "insubstantial
  to me for safety"; by 2026-03, his self-diagnosed rationale included that "real money
  creates accountability" — RESULT: POSITIVE, later complicated — live settlements confirmed
  within about ten weeks; see the temporal-leakage catch in April, below, for the
  complication — [FIRST-HAND decision, SUPERVISED execution]

- **2026-01 — "Validation before building" adopted as standing practice** — Rule: spawn a
  separate agent to verify a research claim against real code before committing further
  infrastructure investment — RESULT: POSITIVE — became a durable practice, later echoed
  directly as the multi-model review discipline used throughout the rest of the record —
  [FIRST-HAND]

- **2026-01 — Multi-agent long-document drafting pipeline** — Ran a large personal
  claim-graph (154 nodes) through a batched, multi-agent drafting process to produce a full
  first draft of a long document — RESULT: MIXED — a first one-shot attempt was explicitly
  rejected as not working well ("that didn't work terribly well"); a node-by-node
  incremental redo did produce a complete draft, but the stated verdict on the draft itself
  was that it was not the valuable part of the exercise — [SUPERVISED]

- **2026-02 — quant-ingestion-and-simulation: numerical-methods infrastructure** — Built
  real applied-math infrastructure (PSD projection, Cholesky/eigendecomposition fallback,
  block-diagonal correlation structure), `mypy --strict` throughout — RESULT: POSITIVE —
  became the oldest continuously-developed research repo in the account and was later named
  the single highest-non-Claude-model-contribution repo in the whole account — [SUPERVISED
  build; the designation itself is WINDOW-NARRATED: it appears in the Claude-written
  session summary of the 2026-07-10 repo editorial pass ("Scott's 'highest-GPT-contribution
  repo'"), and whether the phrase originated with Scott or with Claude is INDETERMINATE.
  It is a contribution-composition observation, not a model-issued quality grade — no
  critical-reading or anti-sycophancy protocol applies because nothing was being judged —
  but its measurement basis is unrecorded; verifiable from the repo's commit/provenance
  data if it's ever load-bearing]

- **2026-02 — External validation check against a funded startup** — Reviewed a
  well-funded startup's newly-launched product (agent-context versioning in git) against an
  already-built personal continuity system — RESULT: POSITIVE (validating) — found
  substantial overlap with a system already built and in use months earlier; the one idea
  actually adopted from the comparison was session-ID-in-commit-message linkage —
  [INDETERMINATE attribution]

- **2026-03 — Window-file continuity: replaced an over-engineered spec** — Rejected an
  earlier continuity design (a new Postgres table, four new tools, HTTP-based hooks,
  summarization-as-a-tool) as over-engineered and replaced it with file-based window
  continuity, forked-agent summarization, and free-form prompting instead of a fixed schema
  — RESULT: POSITIVE — this is the direct, literal predecessor of the window-file system
  still governing session continuity throughout the record, including the notes this
  chronology itself was built from — [FIRST-HAND design call]

- **2026-03 — dev-workflow: third-generation coordination tool** — Replaced an
  intermediate, file-based coordination scheme with a git-native, typed workflow (vision →
  requirements → spec → skeleton → TDD → build → review gates), the project directory
  itself acting as the coordination mechanism — RESULT: POSITIVE — this is the production
  tool in continuing use since; its predecessor arc runs shared-mailbox coordination (Nov
  2025, above) → file-based coordination → this — [FIRST-HAND design principle ("the human
  is the router and the decider"), SUPERVISED build]

- **2026-03 — Sycophancy-calibration A/B on reviewer prompting** — Controlled comparison of
  two review-request framings: "encourage genuine criticism" (made a reviewer model rate a
  claim "massive leap forward" — sycophantic) vs. "permission to be critical / the social
  cost of being critical is zero" (made the same model "the sharpest critic of any reviewer
  in any round") — RESULT: POSITIVE — became a standing practice, reused verbatim across at
  least three later projects — [FIRST-HAND]

- **2026-03 — Silent model-substitution caught mid-review-program** — Noticed, via
  usage-log inspection, that dispatches nominally sent to a frontier model had actually
  been silently routed to a much weaker model by a harness routing bug —
  RESULT: NEGATIVE (the bug), caught cleanly — response was to bypass the broken path
  entirely for one vendor and explicitly flag the other as still possibly affected rather
  than assume the fix was complete — [FIRST-HAND catch]

- **2026-03 — ai-research-ontology: 65-paper taxonomy bootstrap** — Deliberately restarted a
  paper-classification taxonomy chronologically instead of thesis-first, after an earlier
  batch surfaced a "convergence illusion" driven by selection bias — RESULT: POSITIVE —
  7 waves, 682 classes, built from an empty vocabulary in about 2.5 hours — [SUPERVISED
  execution, FIRST-HAND methodology call]

- **2026-03 — ai-research-ontology: "be more inclusive" prompt change reverted** — Built a
  Jaccard/precision/recall harness for LLM entity extraction; a prompt change intended to
  raise recall measurably worsened scores for both a strong and a mid-tier model —
  RESULT: NEGATIVE, targeted revert — reverted just the harmful prompt steps while keeping
  unrelated fixes, and correctly root-caused the real quality ceiling as a name-mapping
  problem, not an instruction-following one — [SUPERVISED]

- **2026-03 — ai-research-ontology: self-optimizing prompts hurt strong models
  (reproduced)** — Ran two independent rounds letting models rewrite their own extraction
  prompts — RESULT: NEGATIVE, reproduced twice — both rounds found self-optimization
  regressed the strong models (Opus/GPT-tier) and helped only the weakest model tested; a
  real, falsifiable, twice-reproduced finding about a specific technique, not a one-off —
  [SUPERVISED]

- **2026-03 — Gold-set eval suite built for an LLM classifier** — Built a 43-case, tiered
  (easy/boundary/ambiguous) gold-standard test set for a market classifier, added synthetic
  cases to cover untested categories, ran two rounds of multi-model review to convergence
  with disagreements adjudicated and the rationale recorded rather than forced to consensus
  — RESULT: POSITIVE — [SUPERVISED]

- **2026-03 — Window-file continuity: three-bug silent-failure discovery** — A controlled
  experiment proved the continuity system's context-injection hook had been display-only
  (visible to the human, invisible to the model) since it was first built —
  RESULT: NEGATIVE, severe, self-caught, then fixed — three separate bugs found and fixed in
  the same session and verified live — [SUPERVISED diagnosis, INDETERMINATE on exactly who
  typed the fix]

- **2026-03 — Prediction-markets: synthetic-spread backtest catch** — Found the per-trade
  backtest was treating hourly-candle high/low prices as simultaneous, manufacturing a
  spread tighter than any real moment and inflating the strategy's apparent win rate to
  95.2% — RESULT: NEGATIVE, self-caught — on real close prices the strategy was
  marginal-to-negative; the honest number was kept over the flattering one — [FIRST-HAND
  catch, SUPERVISED rebuild]

- **2026-03 — Prediction-markets: chain-detection bug** — A ticker-regex-based classifier
  misclassified 33% of events (2,086) as safe monotone option chains — RESULT: NEGATIVE,
  fixed — after a two-layer fix, real-chain win rate rose from a blended ~78%/93% mix to
  93.3% — [INDETERMINATE]

- **2026-03 — claude-hub: production memory leak** — A running instance grew from 130MB to
  4.3GB RSS over 5.7 days — RESULT: MIXED — root cause was a SIGTERM-handler bug forcing
  SIGKILL on every restart; six fixes shipped, then an independent follow-up review caught
  four *more* bugs inside the fixes themselves (a TOCTOU race, an eviction bug, a lock held
  during a blocking wait, a wrongly-reapable participant) — [SUPERVISED]

- **2026-03 — Native computer-use environment stood up, days after the upstream reference
  release** — Built a non-Docker computer-use GUI stack (Xvfb/metacity/tint2/x11vnc) instead
  of the vendor's own Docker reference image, because that image puts the agent inside the
  container alongside the display, which doesn't compose with an externally-driven session
  sharing the same display — RESULT: POSITIVE — included a real compatibility finding
  (mutter refuses to run outside a full GNOME session; metacity substituted) —
  [SUPERVISED]

- **2026-04 — Prediction-markets: temporal-leakage catch, trading goal demoted** —
  Discovered train/test temporal leakage behind a suspiciously good backtest result and used
  it to trigger a systemic infrastructure rebuild rather than a patch, explicitly demoting
  the live trading-strategy goal beneath infrastructure correctness in the project's own
  governing notes — RESULT: MIXED — real trades had already settled successfully in the
  prior two months before the leakage was found; effort then shifted from active strategy
  work to fixing the measurement pipeline itself — [FIRST-HAND]

- **2026-04 — nexus-prime: kernel bootstrap in one ~19-hour session** — Built, live, in a
  single sitting: a window-file continuity system, a separate knowledge store,
  token-triggered agent forking, and a supervisor-command protocol —
  RESULT: POSITIVE — debugged and fixed real infra problems live (an autocompact override
  not working in stream-json mode, forks silently failing past ~200k–550k tokens, a NixOS
  sudo-PATH bug); the append-only, no-fixed-sections window-file design from this session is
  still in effect everywhere it was later checked — [SUPERVISED]

- **2026-04 — model-collaboration-study: design rulings ahead of pre-registration** — Formal
  decisions made before any data collection: compute matched in dollars, not tokens; a
  frontier judge treated as an instrument, not a subject under study; Phase 1 narrowed to
  executable-scoring only, LLM judging dropped, reasoning explicitly that "people... would
  at least wonder why we didn't walk before we ran" — RESULT: ONGOING — design rulings and
  infrastructure in place, a pre-kickoff power analysis run (the final statistical-scoring
  choice explicitly deferred to kickoff), zero experimental results as of this writing; a tie-break-policy design flaw survived four rounds of cross-lineage review
  before being caught by direct inspection — [FIRST-HAND design, SUPERVISED build]

- **2026-05 — claude-hub at real usage scale** — An audit found 383 active artifacts (227
  reviews, 87 review-syntheses, 61 windows) accumulated through ordinary use, running
  "bursty around spec gates" — RESULT: POSITIVE — confirms the review-and-window system was
  genuinely load-bearing daily infrastructure by this point, not a demo — [FIRST-HAND usage,
  SUPERVISED infra]

- **2026-06 — Auto-mode permission friction root-caused to a personal habit** — After three
  actions were denied in one session, concluded roughly 80% of the friction was the
  permission system correctly enforcing what a prior habit of bypassing it had silently
  allowed, and that hot-patching a deploy environment directly (instead of through git) is
  why an untracked file had drifted undetected for months — RESULT: MIXED — four concrete
  process changes followed the self-diagnosis — [FIRST-HAND]

- **2026-06 — Bug-factory micro-pilot: NO-GO** — Designed and ran a from-scratch synthetic-
  bug generator (one model writes a coding task, another implements it in a scripted
  code–test–debug loop, buggy intermediate states harvested as review-corpus material)
  against a pre-stated go/no-go decision band, after a methodology review forced real
  revisions first (blinded screening, bias metrics, a smoke-review recall check) —
  RESULT: NEGATIVE, clean — harvested 1 usable bug from 24 trajectories (~4%) against a
  30%-on-at-least-one-tier decision band; generated tasks were too easy for even the weakest
  tested implementer to fail on. Explicitly logged as not a general verdict on
  model-authored bug factories, only on this exact recipe — two concrete follow-up pilots
  proposed — resolved by the July pilots, below — [FIRST-HAND idea origination and pilot
  design, SUPERVISED execution]

- **2026-06 — Review-diversity: first public post published** — Published a first post on
  multi-model code review, explicit that the historical ad-hoc review data was "casual
  noticing of a pattern," not evidence on its own, paired with a proposed follow-up design
  (the worked preregistration promised as a later post) and a formal power estimate — RESULT: POSITIVE — a real, published, methodologically
  honest artifact with a legible falsifiable follow-up plan; about a month later, still
  awaiting the next post in the planned series — [FIRST-HAND writing, SUPERVISED drafting
  and review]

---

## 2026 — July

- **2026-07 — Public-repo review: scout-before-ruling** — Instead of accepting an initial,
  name-pattern-matched triage of the whole repo set at face value, ran a fleet of read-only
  scout agents to check actual content before ruling anything permanently hidden —
  RESULT: MIXED, positive for the method — five of eight initial "never show this" calls
  were overturned by direct inspection; logged explicitly as a process lesson
  ("repo-classification from names runs ~40% error") — [FIRST-HAND methodology call,
  SUPERVISED execution]

- **2026-07 — one-spec-five-agents: an eight-month-old experiment rediscovered and
  published** — The five-lineage parallel build from November 2025 (above) was found
  sitting in an old archive, and its cross-build comparison was finally written up —
  RESULT: POSITIVE — a second-pass verification overturned the writeup's own first-draft
  causal explanation for one build's failure after someone actually ran the code, and that
  correction was kept in the published version rather than smoothed over — [SUPERVISED]

- **2026-07 — 18-repo adversarial review pass** — Ran a deliberately "extra-thorough"
  multi-model review across the account, explicitly scoped to catch bias, anchoring, and
  sycophancy-shaped reluctance to criticize before treating anything as presentable —
  RESULT: MIXED, positive for the method — zero repos were auto-disqualified, but real
  defects were found and fixed: an unauthenticated endpoint bound to `0.0.0.0`, undisclosed
  AI-authorship in one repo, a command-injection bug in a superseded repo, and a leak of my
  own machine identifiers (local paths, shell prompts, hostnames — no third-party data, no
  credentials) scrubbed across five repos — [FIRST-HAND methodology, SUPERVISED execution]

- **2026-07 — uniform-k-compression: a self-flagged unverified table finally resolved** — A
  previously self-added "⚠️ Unverified figures" warning on a cost/performance table (an
  independent recompute had found materially different numbers) was acted on rather than
  left standing — RESULT: NEGATIVE (the original table was wrong and had sat that way for
  months) — the 18-line table was deleted outright rather than patched with unverifiable
  numbers — [SUPERVISED]

- **2026-07 — portfolio-tool: install fix, and the fix's own false claim caught twice** —
  Fixed a broken-from-a-fresh-clone install (bad import paths, a missing dependency) on the
  repo already publicly framed as a deliberate vibe-coding-limits case study —
  RESULT: MIXED — the first fix-agent's own report contained a confident false claim ("one
  numpy bug" behind five test failures; actually four distinct, pre-existing causes),
  caught by an independent cross-lineage review; the remediation pass that followed then
  introduced a new regression of its own, which the same reviewing lineage caught again on
  re-check — creator≠reviewer discipline demonstrating itself twice in one day —
  [SUPERVISED]

- **2026-07 — multi-agent-harness: first green CI in its eight-month history** — Fixed a
  one-line missing-import bug that had kept every CI run red since the repo's creation
  (2025-11-14 through 2026-07-13, 6 runs, 6 failures) — RESULT: POSITIVE — CI went green for
  the first time ever; an independent cross-lineage review then found the repo's own status
  banner overclaimed which classes actually existed in the code, and a second remediation
  pass fixed the banner plus a latent typing bug in the same review pass —
  [SUPERVISED, creator≠reviewer discipline applied]

- **2026-07 — MultiModelCLIEmail: hostname scrub** — Removed my own machine hostnames from
  seven filenames and fourteen files' content across the committed message archive (kept to
  the repo's own existing host/host2 naming convention) —
  RESULT: POSITIVE at the current tip, mechanical and verified — an independent baseline
  sweep confirmed nothing was missed there. The pre-scrub commits still carry the old
  values: a head scrub, not a history rewrite, and a deliberate call rather than an
  oversight — the two names are my own home machines' Apple defaults, not credentials and
  not anyone else's data, and rewriting a public repo's history to erase them would cost
  more than it buys — [SUPERVISED]

- **2026-07 — Review-diversity: Bayesian counting-rule power simulation** — Ran a same-day
  simulation to settle a statistical-design question (direction-only vs. both-criteria
  significance) for the planned follow-up study — RESULT: ONGOING — direction-
  criterion power estimated at 0.864 at N=50; a marginal-vs-per-cell odds-ratio wrinkle
  (2.0 vs. ≈2.46) surfaced and was deliberately left open for a considered decision rather
  than silently resolved — [SUPERVISED]

- **2026-07 — Bug-factory follow-up pilots: two falsified preregistrations, one
  cost-declined viability** — Ran the three follow-up pilots the June micro-pilot had left
  proposed, each against a pre-stated design. Pilot A (reference-reject recipe): proved
  conditionally viable — five usable bugs harvested; reject rate 8.7% [5.4–13.9];
  downstream pipeline cost $0.28 per usable bug (gate + repair + screen — "marginal" only
  under the report's stated generation-treated-as-sunk scenario); fully loaded ~$2.37/bug,
  ~$710 per 300 (range $480–$1,100 from the reject-rate CI alone, stated in the report as
  a lower bound on the true uncertainty) — with an oracle-coherence blocker identified;
  the scale-up was declined against an informal ≤$1/bug band on the fully-loaded number,
  explicitly not on mechanism. Pilot B: the prediction that frontier
  models would be weak enough implementers to yield organic bugs was FALSIFIED — 71 of 72
  one-shot passes. Pilot C (algorithmic-depth seeds, a deliberately harder self-challenge):
  falsified and scored — 18 of 18 one-shot even under enforced complexity bounds, with the
  mechanism identified (classic algorithms are retrieval; stating the complexity bound
  names the algorithm). Total pilot spend ~$18 — RESULT: MIXED — the tested single-file
  recipes are exhausted and the two scored, falsified predictions stay on the record; the
  wider design space is explicitly left open — [FIRST-HAND design and rulings, SUPERVISED
  execution]

---

- **2026-07 — memory-tool-backend: unpreserved work recovered on the gated project; the
  gate experiment's design lesson named** — A census sweep found the project's working
  material unpreserved — whole untracked directories, with the spec file itself carrying a
  working embedded reference implementation — on the one project whose git hooks gate on
  model review (the 2025-10-16 hard-gate experiment). Scott's causal hedge preserved:
  uncommitted "likely because" of the gate. Recovery: implementation rebuilt from the spec's
  own reference (31/31 contract tests), cross-lineage pre-push review found 7 real bugs the
  tests don't cover (2 critical), pushed to a wip branch rather than gated main; the hook
  itself had a real bug (gated every branch, not just main) fixed in the same pass — RESULT:
  MIXED — the recovery is positive; the nine-months-later negative result is a hedged causal
  inference: the material was uncommitted "likely because" a gate sat where git also serves
  durability and cross-box sync. Scott's lesson, FIRST-HAND (2026-07-15): "If we're going to
  have real gates then we need to start developing in branches to allow those things. If we
  want those things. I think this is why the more recent dev workflow doesn't have such
  hooks." — [SUPERVISED recovery/fixes, FIRST-HAND lesson]

---

*End of chronology. 51 entries, 2024-08 through 2026-07-15. Compiled by agents from a
reviewed private record of the underlying conversations, repositories, and session logs;
claims were taken from that reviewed record rather than re-derived from raw transcripts,
and the private record retains per-entry evidence pointers.*
