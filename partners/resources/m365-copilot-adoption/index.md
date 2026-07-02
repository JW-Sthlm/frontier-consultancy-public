# AI-First Beyond Delivery — M365 Copilot for Secondary Processes

The Frontier Consultancy tracks focus on the primary process: the AI-first delivery of services to customers. But an AI-first partner is AI-first everywhere. **Finance**, **HR**, **purchasing**, **facilities**, and **sales** all contain repetitive, language-heavy work that Copilot handles well. Adopting here requires less technical setup than delivery-side AI, and the habit-building is the same.

---

## Why this matters

Partners who adopt M365 Copilot internally get three things:

1. **Direct productivity gains** — hours recovered per person per week across all departments.
2. **Internal credibility** — you cannot convincingly deliver AI transformation for your customers if your own finance team still writes emails from scratch.
3. **A replication pattern** — the adoption motion you run internally is the same motion you will help your customers run. You learn it by doing it first.

---

## Adoption approach

Use a phased rollout. Each department has different literacy levels, different risk appetite, and different low-hanging fruit. Start with quick wins that deliver value in the first week, not a big-bang rollout that depends on training everyone at once.

| Phase | Scope | What changes |
|---|---|---|
| **0 — Activate** | All departments | Ensure every user has a Microsoft 365 Copilot licence. Verify it is active. |
| **1 — Quick wins** | Per department | 2–3 scenarios each person does daily or weekly. No process redesign. |
| **2 — Workflow integration** | Per department | Copilot becomes the default starting point for standard work items. |
| **3 — Agents** | Selective | Build or deploy agents for repeating structured tasks (HR policy Q&A, sales follow-up, etc.). |

---

## Finance

**Standard M365 Copilot experiences:**

| Scenario | App | What to prompt |
|---|---|---|
| Summarise invoice or contract | Outlook, Word | "Summarise this document and list all amounts, deadlines, and parties" |
| Write financial narrative for a board deck | Word | "Write a 3-paragraph summary of Q2 results based on this data" |
| Analyse cost data | Excel | "What are the top 5 cost lines this quarter? Show as a table and flag any variances above 10%" |
| Prepare for a finance meeting | Teams | "Summarise the last three finance meetings and list open actions" |
| Draft a vendor response | Outlook | "Draft a response to this vendor email asking for a payment extension of 30 days" |

**Role-specific:** [Microsoft 365 Finance Agent](https://learn.microsoft.com/en-us/copilot/finance/) — invoice reconciliation, financial analysis, and variance analysis in Excel. Available as an add-on for users who already have a Microsoft 365 Copilot licence.

**Quick win to start:** Copilot in Excel for monthly cost analysis. Ask it to flag variances above a threshold. Takes 10 minutes of setup and zero process change.

---

## HR

**Standard M365 Copilot experiences:**

| Scenario | App | What to prompt |
|---|---|---|
| Write or rewrite a job description | Word | "Write a job description for a senior Dynamics 365 consultant at [company name]" |
| Summarise interview or performance review notes | Teams, Word | "Summarise this meeting transcript and extract the key feedback points" |
| Draft onboarding documentation | Word | "Create a 1-week onboarding plan for a new ERP consultant joining our team" |
| Answer HR policy questions | Business Chat | "What is our parental leave policy?" (requires SharePoint knowledge source) |
| Draft an offer letter | Word | "Draft an offer letter for [role] at [salary] starting [date]" |

**Agents:** The [Benefits agent template](https://learn.microsoft.com/en-us/microsoft-copilot-studio/template-m365-ext-benefits) (Copilot Studio) answers employee questions about company-provided benefits. Requires SAP SuccessFactors as a data source. For a broader HR Q&A agent without that dependency, build a custom agent in Copilot Studio against a SharePoint knowledge base containing your HR policies.

**Quick win to start:** Copilot in Teams for meeting summaries after interviews and performance conversations. Zero setup if Copilot is licensed and transcription is enabled.

---

## Purchasing and Facilities

There is no dedicated role-specific Copilot for procurement yet. Standard M365 Copilot covers the main workflow:

| Scenario | App | What to prompt |
|---|---|---|
| Summarise and compare vendor quotes | Word, Excel | "Compare these three quotes and recommend the best value option based on total cost and delivery lead time" |
| Draft a purchase request or approval email | Outlook | "Write a purchase request for [item] including the business justification and estimated cost" |
| Review a supplier contract | Word | "Summarise this contract. Flag any auto-renewal clauses, termination conditions, and payment terms" |
| Track facility issues and actions | Teams, OneNote | "Summarise the open facility issues from the last three meeting notes" |
| Write an RFP or supplier brief | Word | "Write a request-for-proposal for office cleaning services at our [city] location" |

**Custom agent option:** A Copilot Studio agent connected to your procurement mailbox can triage incoming supplier emails and route them by category. Medium effort — worth it if you process more than 50 supplier emails per week.

**Quick win to start:** Copilot in Word for contract review. Paste in a supplier contract, ask it to flag risks and key terms. No process change required.

---

## Sales

Sales is the department with the most mature role-specific Copilot tooling.

**[Microsoft 365 Sales Agent](https://learn.microsoft.com/en-us/microsoft-sales-copilot/)** (add-on to Copilot licence, connects to Dynamics 365 Sales or Salesforce):

| Scenario | What it does |
|---|---|
| Meeting prep | Pulls opportunity data from CRM, surfaces last interactions, suggests talking points |
| Meeting follow-up | Auto-drafts follow-up email with action items from the Teams meeting transcript |
| CRM updates | Extracts commitments and updates Dynamics 365 Sales fields from meeting notes |
| Opportunity summary | One-click summary of any open opportunity: stage, contacts, recent activity |
| Pipeline review | "Show me all open deals at proposal stage" answered from Business Chat |

**Standard M365 Copilot (no Sales Agent add-on):**

| Scenario | App | What to prompt |
|---|---|---|
| Draft a proposal or statement of work | Word | "Draft a proposal for [service] addressing [client problem]" |
| Prepare for a customer meeting | Teams, Outlook | "Summarise the last 5 emails with [client] and list any open questions" |
| Write a follow-up email | Outlook | "Write a follow-up to today's discovery call summarising what we discussed and the agreed next steps" |
| Research a prospect | Business Chat | "Summarise [company name]'s industry, recent news, and likely Dynamics 365 needs" |

**Custom agents:** Build a follow-up agent in Copilot Studio that sends personalised follow-up messages after a defined period of no activity on an opportunity. See [Copilot Studio agent templates](https://learn.microsoft.com/en-us/microsoft-copilot-studio/template-fundamentals) for a starting point.

**Quick win to start:** Copilot in Outlook for meeting follow-up emails. After every sales call, paste the notes and prompt: "Write a follow-up email summarising what we discussed and the agreed next steps."

---

## Rollout checklist

- [ ] Verify all staff have an active Microsoft 365 Copilot licence
- [ ] Enable meeting transcription in Teams (required for meeting summaries)
- [ ] Run one "hour of Copilot" per department — live demo of 2–3 quick wins
- [ ] Identify one champion per department to sustain usage and share what works
- [ ] Audit SharePoint: is HR policy content there? If not, move it — it unlocks Business Chat answers
- [ ] Evaluate Finance Agent and Sales Agent licences for relevant teams
- [ ] Schedule a 30-day check-in: what are people using, what is not sticking, what to add next

---

## Resources

| Link | What it is |
|---|---|
| [Microsoft 365 Copilot adoption hub](https://adoption.microsoft.com/en-us/copilot/) | Adoption guides and getting started resources |
| [Copilot Skilling Center](https://adoption.microsoft.com/en-us/copilot/skilling-center/) | Role-based training, videos, and events by department |
| [Sales Agent overview](https://learn.microsoft.com/en-us/microsoft-sales-copilot/) | Documentation and getting started guide |
| [Finance Agent overview](https://learn.microsoft.com/en-us/copilot/finance/) | Documentation and getting started guide |
| [Copilot Studio agent templates](https://learn.microsoft.com/en-us/microsoft-copilot-studio/template-fundamentals) | Available agent templates including Benefits, IT Helpdesk, and more |
