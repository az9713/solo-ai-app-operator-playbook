# Solo AI App Operator Playbook

This is the **compressed operating system** implied by the host’s examples—Medv, Cal AI, Wave AI, Fly Peter, Trenfeed, Aura, Sleek, and Siteshore/CiteSure—plus a layer of operator-grade structure on top. The recurring patterns in the video are: **pick a painful problem, define the customer sharply, compose existing services, build in small chunks, use AI-friendly stacks, and win distribution without paid spend**.

I will separate this into:

1. **Core doctrine**
2. **12-step execution loop**
3. **Default stack**
4. **Prompting workflow**
5. **Distribution system**
6. **Reliability and scaling gates**
7. **Failure modes**
8. **A 30-day launch plan**
9. **A ruthless scoring rubric for app ideas**

---

## 1. Core doctrine

### A. Your job is not coding
Your job is:

- choosing the right pain point,
- defining the right customer,
- decomposing the product correctly,
- orchestrating tools and services,
- and driving distribution.

The examples repeatedly show founders using AI plus third-party services while focusing their own energy on **judgment** and **positioning**, not artisanal engineering.

### B. Do not build a company from raw atoms
Most solo founders fail because they overbuild. The winning pattern is:

- use APIs,
- use managed infra,
- use existing datasets,
- use model providers,
- use outsourced ops where possible.

Medv and Wave AI are framed exactly this way: treat dependencies as services, not as departments.

### C. Crowded markets are acceptable
Cal AI and Wave AI matter because they were not novel categories. The point is that **you can still win in a crowded market** if:

- the pain is real,
- the workflow is better,
- the UX is smoother,
- or AI materially improves the core job-to-be-done.

### D. Build in chunks, never in one giant prompt
This is one of the most repeated workflow lessons. The founder of Wave AI is described as building piece-by-piece; Aura stresses short prompts and minimal context; Trenfeed is described as modularizing components AI can build and merge.

This is non-negotiable.

### E. Distribution is not downstream of product
Sleek, Trenfeed, and Cal AI all emphasize distribution leverage—X, TikTok, Instagram, YouTube, influencers—rather than paid performance marketing.

In the AI era, shipping is cheaper. Therefore **distribution becomes more scarce**.

---

## 2. The 12-step execution loop

### Step 1: Choose a painkiller, not a vitamin
Ask:

- What task is repeated frequently?
- What task is annoying, error-prone, or slow?
- What task causes money leakage, trust breakdown, or embarrassment?
- What task has become more important because people now use AI?

Siteshore/CiteSure is the archetype: very narrow problem, very real pain, high trust value.

#### Good wedges
- verification,
- summarization-to-action,
- workflow compression,
- expert translation of messy inputs,
- personal or team operating dashboards,
- agent guardrails,
- AI output QA,
- vertical copilots with narrow scope.

#### Bad wedges
- generic chatbot clones,
- broad “AI platform” products,
- apps with unclear buyer,
- ideas whose value depends on users changing habits too much.

---

### Step 2: Write the ICP before writing code
Sleek’s segment makes this explicit: **define the ideal customer profile first**.

Use this template:

**ICP Card**
- Role:
- Industry:
- Team size:
- Current workaround:
- Pain frequency:
- Cost of current pain:
- Existing tools:
- Why current solutions fail:
- Trigger event that makes them buy now:
- Will they pay personally or through company budget?

If this card is fuzzy, the product is fuzzy.

---

### Step 3: Specify the “job to be done” in one sentence
Template:

> “This app helps [ICP] do [job] in [time] instead of [current painful method], with [specific measurable improvement].”

Example:

> “This app helps newsletter operators turn raw news links into ranked, theme-clustered briefs in 10 minutes instead of 90 minutes of manual triage.”

If you cannot write this sentence cleanly, you are not ready to build.

---

### Step 4: Copy the workflow, not the surface product
Trenfeed’s founder reportedly did deep competitor analysis and UI review before building.

Correct method:

- study 5–10 competing products,
- list their onboarding, core actions, pricing, positioning, and obvious user complaints,
- map the workflow skeleton,
- then improve the most painful step.

Do **not** ask “What app should I build?”
Ask:
- “Where is the workflow still manual?”
- “Where is trust low?”
- “Where is accuracy just good enough to displace work?”
- “Where is latency still irritating?”

---

### Step 5: Architect for composition
Before generating code, decide what you will **not** build.

Split system into:

#### Proprietary core
What must be uniquely yours:
- ranking logic,
- vertical prompt assets,
- workflow orchestration,
- proprietary dataset enrichment,
- onboarding logic,
- community/distribution engine.

#### Commodity layer
What should be rented:
- auth,
- database,
- payments,
- hosting,
- search,
- transcription,
- image gen,
- notifications,
- analytics,
- email.

This is where most solo founders blow themselves up: they build commodity plumbing.

---

### Step 6: Use an AI-friendly stack
Repeated default stack:

- **Frontend**: Next.js + React + Tailwind + shadcn/ui
- **Backend**: Next.js server actions / route handlers or simple Python microservices where needed
- **DB/Auth**: Supabase or Postgres + Clerk/Supabase Auth
- **Hosting**: Vercel for web, Cloud Run/Render/Fly where background jobs matter
- **Payments**: Stripe
- **Storage**: Supabase Storage / S3
- **Queue/Jobs**: Trigger.dev / Inngest / serverless cron
- **Analytics**: PostHog
- **Email**: Resend
- **LLM routing**: Anthropic + OpenAI + Gemini fallback
- **Search/RAG**: minimal first, not as a religion

Why this matters:
- models know this stack,
- generated code is more likely to work,
- community examples are abundant,
- debugging surface area is lower.

---

### Step 7: Generate via task decomposition
Never say:

> “Build my whole app.”

Instead produce this document first:

#### Product decomposition sheet
- Core entities
- User roles
- Main workflows
- Required screens
- State transitions
- External integrations
- Background jobs
- Edge cases
- Billing model
- Analytics events
- Security/privacy notes

Then break into tickets:

1. landing page
2. auth
3. onboarding
4. core data schema
5. first key workflow
6. result display
7. billing
8. admin/debug page
9. analytics
10. error handling

This matches the chunked approach emphasized across the examples.

---

### Step 8: Prompt like an engineering manager
Keep prompts short, focused, and with minimal correct context.

#### Good prompt pattern

Use:

**Context**
- current file(s)
- current goal
- constraints
- acceptance criteria

**Task**
- one bounded task only

**Output**
- code changes only
- list assumptions
- note any migration steps
- note tests to run

#### Example

```text
Context:
This is a Next.js app with Supabase auth and Postgres.
We already have onboarding and user profiles.

Task:
Create a "projects" table and the server actions needed to create, rename, archive, and list projects for the signed-in user.

Constraints:
Use existing auth helpers.
Do not change unrelated files.
Add Zod validation.
Return explicit errors.

Acceptance criteria:
Users can create, rename, archive, and view only their own projects.
```

#### Rules
- one task per prompt,
- one abstraction level per prompt,
- never mix UI redesign + DB schema + bug fix in one ask,
- avoid giant context dumps,
- ask for diffs, not essays.

---

### Step 9: Get to a painful but useful MVP
Your MVP should **not** be feature-complete. It should be:

- ugly but legible,
- narrow but useful,
- manually patchable behind the scenes,
- sellable to one ICP.

Use the **one-core-loop rule**:
- a user signs up,
- completes one action,
- receives one valuable outcome,
- sees one reason to return.

That is MVP.

---

### Step 10: Instrument user behavior immediately
Before public launch, track:

- signup conversion,
- activation rate,
- time to first value,
- retention D1 / D7 / D30,
- paid conversion,
- churn reason,
- top error paths,
- most used workflow,
- dropped flows.

If you do not observe the system, you are blind.

---

### Step 11: Launch with native distribution
Start with the channel that already maps to your ICP:

- **X** for founders, builders, tech/design
- **TikTok/Instagram** for creator tools, consumer utility, visual before/after
- **YouTube** for workflow products needing explanation
- **Influencers** for lifestyle/fitness/creator/consumer niches
- **Communities** for prosumer and technical verticals
- **Cold outbound** for B2B niche tools

#### Launch content system
Produce:

1. problem demo,
2. before/after,
3. 30-second workflow clip,
4. result screenshot,
5. founder build story,
6. user testimonial,
7. competitive comparison,
8. “how it works” thread/video.

Do not just announce the product. Show the workflow compression.

---

### Step 12: Add reliability only when signal is real
Solo works until reliability failures destroy money or trust.

#### Reliability gates
Once any of the following is true, you need better engineering process:
- revenue > meaningful side-income,
- business-critical workflows depend on uptime,
- users entrust sensitive data,
- users are blocked when the app fails,
- support burden exceeds founder capacity.

At that point add:
- logging,
- alerting,
- staging,
- backups,
- rollback path,
- incident runbook,
- at least one technical backup person or contractor.

---

## 3. Default stack by product type

### A. Content / creator / marketing tools
- Next.js
- Tailwind + shadcn/ui
- Supabase
- Stripe
- PostHog
- Anthropic/OpenAI
- Vercel

### B. AI verification / research / workflow tools
- Next.js frontend
- Python microservice for extraction/analysis if needed
- Postgres
- queue/job system
- file storage
- citations / provenance logging
- eval set for trust

### C. Consumer mobile utility
- React Native or Expo
- managed backend
- model API routing
- notifications
- analytics
- referral loop

### D. Real-time collaborative or multiplayer app
The prototype is easy; real-time scale is not.

You need:
- websockets or managed realtime infra,
- careful session/state architecture,
- abuse protection,
- load testing early.

---

## 4. Prompting workflow for app building

### The four prompt classes

#### 1. Planning prompts
Use before coding.  
Goal:
- clarify architecture,
- enumerate entities,
- define modules,
- identify edge cases.

#### 2. Generation prompts
Use for bounded implementation tasks.  
Goal:
- create specific tables, routes, screens, components.

#### 3. Debug prompts
Use only with logs/errors and reproduction steps.  
Goal:
- isolate cause,
- propose minimal fix,
- avoid rewrite mania.

#### 4. Refactor prompts
Use after functionality exists.  
Goal:
- reduce complexity,
- modularize components,
- improve naming/testability.

---

### Prompt hygiene rules
- Keep prompts short.
- Supply only relevant files.
- Ask for one change at a time.
- State constraints explicitly.
- Demand acceptance criteria.
- Make model list assumptions.
- Switch models when stuck.

#### Routing suggestion
- **Claude**: code generation, refactors, architectural reasoning
- **GPT**: alternative implementation, debugging angles, copy and content
- **Gemini**: extra fallback, long-context parsing, second opinion
- specialized tools: design/image/audio when needed

---

## 5. Distribution system

### Distribution doctrine
A product without distribution is a private toy.

#### The 5 distribution questions
1. Where does the ICP already spend attention?
2. What format makes the benefit obvious fastest?
3. Can the product create shareable outputs?
4. Is there a referral loop or public artifact?
5. Can one user’s use attract another?

---

### Channel-product fit map

#### X
Best for:
- founder tools,
- design tools,
- AI workflow tools,
- devtools,
- indie hacker products.

Works if:
- strong visual demos,
- clever launch timing,
- public build-in-public narrative.

#### TikTok / Instagram
Best for:
- creator tools,
- consumer utilities,
- transformation products,
- visual workflows.

Works if:
- immediate visual payoff,
- short clips,
- emotionally obvious pain relief.

#### YouTube
Best for:
- products needing education,
- deeper workflows,
- B2B prosumer tools.

Works if:
- you can teach the workflow and let users imagine themselves using it.

#### Influencers
Use when:
- there is trusted niche authority,
- the user base already follows a few key voices.

---

### Launch sequence

#### Pre-launch
- collect waitlist,
- post problem clips,
- show prototype snippets,
- talk to 10–20 ICPs,
- refine messaging.

#### Launch week
- public demo,
- limited early access,
- founder thread/video,
- testimonials from first users,
- daily iteration posts.

#### Post-launch
- ship visibly,
- surface user stories,
- post benchmark/comparison content,
- show metrics carefully,
- keep community loop tight.

---

## 6. Reliability and scaling gates

### Stage 0: Prototype
Acceptable:
- manual ops,
- ugly UI,
- fragile backend,
- no full test coverage.

Not acceptable:
- unclear core value,
- unclear ICP,
- inability to onboard a user without founder explanation.

### Stage 1: MVP with revenue
Now add:
- auth hardening,
- billing correctness,
- basic analytics,
- data backups,
- logs,
- privacy review.

### Stage 2: Real traction
Now add:
- alerting,
- support workflow,
- incident process,
- QA passes,
- staging environment,
- partial automation of ops.

### Stage 3: Mission-critical
Now add:
- redundancy,
- on-call backup,
- audit trails,
- security review,
- performance profiling,
- vendor concentration review.

---

## 7. Failure modes

### Failure mode 1: Build-first, ICP-later
Symptom:
- impressive demo,
- no retained users,
- praise from peers, not customers.

### Failure mode 2: Monolithic prompting
Symptom:
- messy code,
- hallucinated architecture,
- fragile app,
- endless regression bugs.

### Failure mode 3: Overbuilding commodity layers
Symptom:
- custom auth,
- custom billing logic,
- custom infra everywhere,
- no user feedback loop.

### Failure mode 4: Mistaking usage for retention
Track return behavior, not vanity metrics.

### Failure mode 5: No distribution engine
Symptom:
- “We launched but nobody came.”

This usually means the founder built product without channel strategy.

### Failure mode 6: No reliability plan after traction
Symptom:
- outages,
- founder exhaustion,
- churn due to trust loss.

### Failure mode 7: Over-trusting one model
Route between models when blocked.

---

## 8. A 30-day launch plan

### Days 1–3: Opportunity and ICP
- generate 20 app wedges,
- score them,
- interview 5 target users,
- pick one ICP,
- define one painful workflow.

### Days 4–5: Spec
Create:
- ICP card,
- JTBD sentence,
- product decomposition sheet,
- page flow,
- schema draft,
- success metrics.

### Days 6–10: Core build
Ship:
- landing page,
- auth,
- onboarding,
- first core workflow,
- result screen.

Ignore:
- polish,
- advanced settings,
- broad integrations.

### Days 11–14: Functional refinement
Add:
- billing,
- analytics,
- error handling,
- admin/debug tools,
- support email flow.

### Days 15–18: Distribution prep
Create:
- launch assets,
- demo video,
- screenshots,
- waitlist copy,
- thread/post set,
- referral or invite mechanism if suitable.

### Days 19–21: Soft launch
- onboard first users manually,
- fix high-friction points,
- patch onboarding,
- gather testimonials,
- measure time-to-value.

### Days 22–30: Public launch and iteration
- publish consistently,
- respond to users fast,
- improve the highest-frequency workflow,
- cut dead features,
- push on the channel with best response.

---

## 9. Ruthless scoring rubric for app ideas

Score each 1–5.

### Market pain
- Is the problem frequent?
- Is it costly?
- Is it emotionally irritating?

### ICP clarity
- Can you name the buyer precisely?
- Can you reach them cheaply?

### Workflow compression
- Does the app collapse 30–120 minutes into 3–10 minutes?

### AI advantage
- Does AI make the job materially easier, faster, or more accurate?

### Build tractability
- Can this be built with known AI-friendly stack/components?

### Distribution fit
- Is there an obvious channel where this ICP already watches content?

### Monetization clarity
- Is there a plausible reason they pay within first session/week/month?

### Retention potential
- Does the use case recur naturally?

### Trust/risk
- Are hallucinations/errors tolerable, or must the system be verifiable?

### Defensibility
- Is there room for proprietary workflow, data, brand, or distribution moat?

#### Interpretation
- **42+**: strong candidate
- **35–41**: maybe, requires sharper wedge
- **<35**: likely a distraction

---

## A sharper synthesis for you

The real meta-lesson is not “non-devs can now build apps.” That is already old news.

The deeper lesson is this:

> The bottleneck has shifted upward from implementation to selection, decomposition, distribution, and trust design.

That is where you should compete.

For someone with your profile, the highest-upside lane is probably **not** generic consumer fluff. It is likely one of these:

- AI trust/verification layers,
- research workflow compression,
- finance/econ/geopolitics analyst tools,
- expert-grade synthesis systems,
- agent QA / observability / control surfaces,
- vertical intelligence products with narrow but painful jobs-to-be-done.

Those categories fit your comparative advantage much better than another “AI website generator.”
