# Implementation Workshop Exercise

**How to use this exercise**
In an AI-first implementation, your M365 Copilot becomes an active participant in every workshop. This exercise walks you through prompts you can use after each session to turn raw workshop content into structured, actionable artefacts.

In a Line of Business system implementation, workshops are the primary mechanism for uncovering requirements, discussing options, and making decisions. Capturing this information consistently creates a **digital twin of your implementation** — a structured knowledge base that AI can draw on to perform downstream delivery functions: drafting Statements of Work, generating design documents, building test plans, and more.

**Meeting transcripts** are the source material for this digital twin. Copilot and Teams are the tools to capture this information. Make sure (after approval) that meetings are recorded and transcribed in Teams. Also use Teams for in-person meetings. Make a habit of storing meeting transcript files for easy access for when this information will be used further downstream.

The information can also be used to keep your project on track, by using prompts to distil crucial information on your project from these transcripts.

**Prerequisite:** An active M365 Copilot licence. All prompts below are designed to be used in Microsoft Copilot with your workshop transcript attached or referenced.

**Tip:** Enable the [Facilitator agent](https://learn.microsoft.com/en-us/microsoftteams/facilitator-in-meetings) in your Teams meetings to keep workshops on track in real time.

---

## 1. One-shot meeting distillation prompts

High value, low effort. Run these immediately after any workshop to capture the essentials before context fades.

### 1.1 Executive recap

```
Summarise this workshop in 6–10 bullets covering:
- Key accomplishments
- Decisions made (with owner and rationale)
- Risks identified (impact, mitigation, owner)
- The next 5 actions (owner and due date)
- Open questions that still need resolution
```

### 1.2 Decisions log

```
Extract every decision made in this workshop.
For each decision: decision statement, owner, approver, date, rationale, workstream, dependencies, and required follow-up action.
If a decision is unclear or tentative, mark it as "Proposed" rather than confirmed.
```

### 1.3 Action register

```
List all action items discussed or agreed in this workshop.
For each: description, owner, due date, dependency on other actions, and a supporting quote from the transcript.
If an owner is not named, suggest the most likely role and mark it "needs confirmation".
```

### 1.4 Open questions & parking lot

```
Create an 'Open Questions / Parking Lot' list from this workshop.
Group by topic (process, data, integration, security, testing, change management, timeline).
For each question: why it matters, who should answer, and suggested next step to resolve.
```

### 1.5 Scope & boundary extraction

```
From this workshop, extract:
- What is explicitly in scope
- What is explicitly out of scope
- Items that are uncertain / pending decision
Then produce a short 'scope statement' suitable for a Statement of Work appendix.
```

### 1.6 Status update (for the project team channel)

```
Draft a project-team status update based on this workshop:
- Progress since last workshop
- Decisions made
- Risks/issues (new/changed)
- Actions due next week
- Topics for next workshop
Tone: professional, short, and suitable to post in Teams.
```

---

## 2. Workshop-structured prompts

Every workshop should have one or more predefined objectives, and each workshop includes an agenda and default key questions to drive discussion and decisions.

### 2.1 Agenda-item summariser

```
Summarise this workshop by agenda section.
For each section:
- What we learned
- Decisions
- Gaps/issues
- Actions
- Any unresolved questions
If the agenda isn't explicit, infer sections from the flow of the discussion and label them clearly as 'inferred'.
```

### 2.2 Workshop objectives check

```
Based on this workshop transcript, evaluate whether we achieved these objectives:
1. Clarified/refined requirements
2. Shared understanding across stakeholders
3. Identified gaps/issues
4. Configurable solution approach identified
5. Prepared for next step (CRP/demo/next workshop)
For each objective: evidence from the transcript + what's missing + recommended follow-up.
```

### 2.3 Assumptions list

```
Extract all assumptions stated or implied in this workshop.
For each: assumption statement, risk if wrong, how to validate, and owner to validate.
```

### 2.4 Requirements to backlog candidates

```
Identify all requirements discussed. Convert them into backlog-ready items with:
- Title
- User story format
- Acceptance criteria (3–5 bullets)
- Priority suggestion
- Dependency notes
Mark which ones are 'fit' vs 'gap' if indicated.
```

---

## 3. Fit-to-standard / Fit-gap specific prompts

Fit/gap analysis is a core phase in every standard Line of Business implementation. For Dynamics 365, Microsoft recommends using the [business process catalog](https://learn.microsoft.com/en-us/dynamics365/guidance/business-process-catalog/overview) to guide and organise evaluations in workshops.

### 3.1 Fit/gap summary

```
Create a Fit-to-Standard summary from this workshop:
- Which business processes were reviewed
- For each process: Fit / Configure / Gap
- Evidence from the transcript for each classification
- Next step per gap (config, extension, ISV, process change)
Output as a table.
```

### 3.2 Gap register (ready for design review)

```
Produce a Gap Register from this workshop.
For each gap: description, impacted process, business impact, severity, proposed solution approach, unknowns, and required proof-of-concept (yes/no).
Flag any gaps that sound like 'nice-to-have' rather than business-critical.
```

### 3.3 Prevent unnecessary customisations

```
Identify any moments where the team proposed recreating legacy behaviour.
List each instance and suggest a fit-to-standard alternative (process change, configuration, or standard capability), and note the trade-off.
```

---

## 4. Implementation-workstream prompts

Use these for specific workshop types — data migration, integration design, security, and testing.

### 4.1 Data migration workshop

**Data migration decisions & plan**
```
Extract data migration strategy decisions from this workshop: scope (entities), volume assumptions, tooling, environments, cutover approach, and ownership.
Output: decisions + actions + risks.
```

**Data readiness blockers**
```
List all data-quality or data-availability blockers mentioned.
For each, define remediation steps, owner, and how it impacts timeline.
```

### 4.2 Integration design workshop

**Integration inventory**
```
Create an integration inventory: each integration, source/target, triggering event, frequency, volume, latency/near-real-time needs, error handling, security/auth, and owner.
```

**Integration risks & test needs**
```
Extract integration-related risks and translate them into test scenarios (happy path + failure modes), with suggested owners.
```

### 4.3 Security workshop

**Security decisions**
```
Summarise security model decisions: roles, segregation of duties concerns, admin model, compliance requirements, and any open security questions.
```

**Security risk register**
```
Create a security-focused risk register with severity, impacted data/process, mitigation, and owner.
```

### 4.4 Testing workshop

**UAT plan extraction**
```
From this workshop, draft a UAT plan outline: test scope, test data needs, entry/exit criteria, roles, and timeline.
```

**Traceability check**
```
List which requirements discussed have no clear test coverage mentioned.
Propose test cases to close the gap.
```

---

## 5. Cutover / go-live readiness prompts

### 5.1 Cutover runbook skeleton

```
Draft a cutover runbook skeleton based on this workshop: phases, checkpoints, owners, timing assumptions, rollback criteria, communications plan.
```

### 5.2 Go-live readiness scoreboard

```
Create a go-live readiness scoreboard with categories: Data, Integrations, Security, Testing, Training, Support model, Performance, Operations.
For each: status (Green/Amber/Red) based on transcript evidence + key actions to move to Green.
```


