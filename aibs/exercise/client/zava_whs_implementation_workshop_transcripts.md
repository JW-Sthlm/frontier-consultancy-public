# Zava DIY — Warehouse Management Design Workshop: Meeting Transcript

> **Document ID:** ZAVA-WHS-MTG-001  
> **Meeting Series:** WHS-Only Mode Configuration Design Workshops  
> **Sessions Covered:** Session 1 (Feb 12), Session 2 (Feb 18), Session 3 (Feb 25), Session 4 (Mar 3), Session 5 (Mar 5), Session 6 (Mar 10), Session 7 (Mar 12), Session 8 (Mar 15), Session 9 (Mar 18)  
> **Compiled:** March 25, 2026  
> **Status:** Draft for Review

---

## Attendees (recurring)

| Name | Role | Department |
|------|------|------------|
| Maya Hollister | Supply Chain Lead | Operations |
| Derek Fowler | Warehouse Operations Manager | DC Operations |
| Priya Anand | IT Architect | IT |
| Sam Keogh | Inventory Control Manager | Operations |
| Linh Tran | Logistics Lead | Transportation |
| Marcus Webb | DC Operations Manager | DC Operations |
| Elena Strickland | Quality Manager | Quality Assurance |
| Jordan Bates | Data Migration Lead | IT |
| Facilitator: Alex Chen | WMS Configuration Lead (Microsoft Partner) | External |

---

---

## Session 1 — February 12, 2026: Project Kickoff & Deployment Model

**Location:** Zava DIY HQ Conference Room A, Seattle  
**Duration:** 2 hours

---

**Alex Chen:** Good morning everyone. Thanks for joining for our first design workshop. The goal today is to align on the deployment model for the Dynamics 365 warehouse management rollout — specifically, where D365 fits in your technology stack relative to your existing OMS. Maya, do you want to kick us off with some context on the current state?

**Maya Hollister:** Sure. So today we run all our order management — sales to stores, customer orders for the online channel, vendor POs — through our own OMS. It's been running for about six years and honestly, it does exactly what we need on the order side. The gap is execution in the DC. We're using a basic barcode system on the floor with no directed work, no wave management, no real-time inventory visibility. That's what we need D365 to solve.

**Alex Chen:** That context is really helpful. So when we talk about WMS deployment, there are essentially two models in D365 Supply Chain. The first is the embedded WMS — your sales orders, purchase orders, and warehouse execution all live in D365. The second is called WHS-Only Mode, which is designed exactly for your situation — D365 acts as the warehouse execution engine and receives shipment orders from an external system. The orders live in your OMS; D365 handles the put-away, picking, packing, and shipping at the DC.

**Priya Anand:** That sounds like WHS-Only is the obvious fit. But what does the integration look like? Who pushes orders to D365?

**Alex Chen:** WHS-Only mode uses a message queue architecture. Your OMS sends inbound and outbound shipment orders to D365 via a source system connector. D365 processes them, executes the warehouse work, and publishes inventory updates back to the OMS. It's near-real-time with a one-minute polling interval.

**Derek Fowler:** And for receiving — when a truck shows up at the dock, the DC workers are working in D365 from that point?

**Alex Chen:** Exactly. From the moment an inbound shipment order arrives in D365, workers use the warehouse mobile app to receive, license-plate, put-away, and confirm. All directed by the system.

**Maya Hollister:** That's what we need. The full embedded WMS option — does that require us to move order management into D365?

**Alex Chen:** Not completely, but your order flow would run through D365 rather than staying in your OMS. You'd be looking at a much larger scope — AR, AP, inventory valuation, the works.

**Maya Hollister:** That's a conversation for another day. For Phase 1, let's stay focused. WHS-Only is the right call. We keep our OMS, we add warehouse execution in D365. Priya, does that work from an integration standpoint?

**Priya Anand:** Yes, I'd actually prefer it. We have eighteen years of OMS transaction history and I'm not moving that into a new system. The integration will need some build but it's a defined boundary.

**Alex Chen:** Great. So **Decision 1 is confirmed — WHS-Only Mode**. Now the second topic for today: scope of the physical footprint. How many sites and warehouses are we configuring?

**Derek Fowler:** Just the one DC for now. Seattle. We've talked about a second facility for the Eastern Washington market — Spokane area — but that's a 2028 conversation at the earliest.

**Maya Hollister:** One DC for Phase 1. The design should be clean enough that adding a second warehouse later doesn't require a rearchitecture.

**Alex Chen:** Understood. We'll design for extensibility — standardized zone structure, consistent location profiles — so a second warehouse is an additive change. **Decision 2 confirmed — single site ZAVSITE1, single warehouse ZAVDC1 in Seattle.**

---

---

## Session 2 — February 18, 2026: Warehouse Physical Structure

**Location:** Zava DIY DC, Seattle (floor walkthrough + conference call)  
**Duration:** 3 hours (including facility tour)

---

**Alex Chen:** We've walked the floor and I want to capture what we saw and translate it into the D365 zone model. Derek, can you walk us through the main physical areas?

**Derek Fowler:** So from the back of the building forward: we've got the bulk storage racking — that's where pallets come in and we hold them in full pallet positions. Then we've got the pick aisles, which are replenished from bulk. We've got a dedicated paint bay because those products need flat floor storage and temperature control monitoring. There's a seasonal section — we expand the Garden & Outdoor footprint in spring and contract it in fall.

On the ops side: receiving dock is the east end, ten bays. Staging is split — inbound staging just inside the dock, outbound staging near the west loading area. We have a QA hold area — about 20 pallet positions — and a returns area adjacent to that. Ten truck doors on the outbound side.

**Alex Chen:** That maps very cleanly to two zone groups. Storage — everything that holds inventory. Ops — everything that moves it. Let me propose a specific zone structure and you tell me where it doesn't fit. *(shares screen)*

**Derek Fowler:** *(reviewing)* BULK, PICK, SEASONAL, PAINT for storage — yes, that's right. Four distinct areas with different rules. Operations: RECV, STG-IN, STG-OUT, DOCK, QA, RETURN. That's the full picture.

**Sam Keogh:** I want to call out the SEASONAL zone specifically. In February we start bringing in Garden & Outdoor pre-build stock. We can't have packers pulling from that inventory until March 15. That needs to be a status flag, not just a zone — right?

**Alex Chen:** Right, the zone alone doesn't block reservation. We'll use an inventory status for that — SEASONAL-HLD. Items coming into the SEASONAL zone during pre-build are assigned that status and aren't available for picking until a warehouse manager releases them.

**Sam Keogh:** Perfect. That's exactly what I was worried about.

**Elena Strickland:** What about the QA area? When we quarantine product — say we get a damaged inbound shipment — can we track it to a specific bin for our inspection process?

**Alex Chen:** Absolutely. QA locations use a location profile that enables license plate tracking, so every pallet in QA is tracked individually. You can also block inventory at the LP level rather than the whole QA area if you need to.

**Alex Chen:** Location format — let me ask about the physical labeling. How are your aisles and bins labeled today?

**Derek Fowler:** Aisle letter pairs — EL, HT, HW, and so on. Then a rack number, shelf letter A through D, bin number. So a location might be EL-03-B-08.

**Alex Chen:** Great news — we can replicate that exactly in D365. The system location ID will match the physical label. No relabeling required.

**Derek Fowler:** *(relieved)* That's a big deal. Last time we brought in a system the consultants wanted to renumber everything.

**Alex Chen:** So **Decision 3 — ten zones in two zone groups**. **Decision 4 — four-segment location format AISLE-RACK-SHELF-BIN matching physical labels.** License plate tracking — Derek, your thought on where we need that?

**Derek Fowler:** Bulk storage for sure. I want to know exactly which pallet is in position BLK-LB-03-A-01 at all times, especially for lumber and heavy stuff. Staging areas — yes on both inbound and outbound. QA and Returns — definitely, we need traceability there. Pick faces — honestly, no. We run open-face picking. Adding LP scanning at every pick location would slow down our pickers and I'd have mutiny by lunch.

**Alex Chen:** That's a common and sensible approach. Pick face open — no LP tracking. Everything else that needs traceability — LP enabled. **Decision 5 confirmed.**

---

---

## Session 3 — February 25, 2026: Inventory Statuses and Reservation Logic

**Location:** Video call  
**Duration:** 1.5 hours

---

**Alex Chen:** Today we need to nail down inventory statuses and reservation hierarchy. These backstop every inventory transaction, so getting them right matters. Let me start — what inventory states does your current system track?

**Sam Keogh:** Available, hold — which covers both quality holds and damage — and we have a seasonal hold that we apply manually. Returns come in as a separate bucket until someone decides what to do with them.

**Alex Chen:** Four conceptual states. In D365 I'd recommend we be more explicit — Available, Quarantine Hold, Damaged, Return-Under-Evaluation, and Seasonal Hold. Each has a distinct workflow and transition path. The benefit is you can see exactly how much stock is in each state at any time.

**Elena Strickland:** I like the explicit QA versus Damaged split. Right now they sit in the same "hold" bucket and my team is constantly trying to figure out what's what.

**Maya Hollister:** What's the transition model? Like who authorizes moving from Quarantine to Available?

**Alex Chen:** We configure inventory status change rules. QUARANTINE to AVAIL requires an authorized status change — you can restrict that to QA Manager role. Same for RETURN-PROC to AVAIL or DAMAGED. It's controlled with an audit trail.

**Sam Keogh:** What about SEASONAL-HLD to AVAIL? That's a business event, not a quality event. We want the category manager to be able to release that.

**Alex Chen:** Same mechanism — you just assign the permission to the appropriate role. The system records who did the status change and when.

**Maya Hollister:** That'll work. **Five statuses — confirmed.**

**Alex Chen:** Reservation hierarchy. For a retail DC, the standard approach is: the order specifies site and warehouse — the system figures out location and LP at wave time. Does that match your model?

**Maya Hollister:** That's exactly how we think about it. The OMS says "ship from Seattle DC," the DC floor figures out from where exactly.

**Alex Chen:** No batch or serial number requirements? Some hardware products —

**Maya Hollister:** No. We don't track lots or serial numbers. Maybe someday for Power Tools when we start doing warranty programs, but not now.

**Alex Chen:** Clean. **Decision 7 — RETAIL-STD reservation hierarchy, site and warehouse above wave, location and LP below.** No batch or serial dimensions in scope for Phase 1.

---

---

## Session 4 — March 3, 2026: WHS Integration and Store Destination Model

**Location:** Zava DIY HQ Conference Room B  
**Duration:** 2 hours

---

**Alex Chen:** Phase 4 in our design is the WHS-Only integration layer — the source system setup. Priya, I want to walk through the settings with you alongside Derek.

**Priya Anand:** Ready. I've been reading the MS Learn docs on source systems. My main question is: can we have the OMS also push product master data to D365, or does someone have to maintain items manually in both systems?

**Alex Chen:** Great question. The source system has a "Product master source system" setting. When enabled, D365 item records are created and updated based on product messages from the source system. You don't maintain two catalogs manually.

**Priya Anand:** That's critical. We have 400+ items. Manual sync is not an option.

**Alex Chen:** Agreed. ZAVA-OMS will be set as the product master source system. Jordan, your data migration plan should account for the initial product load coming through the source system message queue rather than a direct data entity import.

**Jordan Bates:** Noted. I'll need the SKU format spec from the OMS team before I can set up the item number creation rules.

**Alex Chen:** Returns — Derek, store returns flow through the DC?

**Derek Fowler:** Yes. Stores receive customer returns, hold them 24 hours, and then consolidate into a return shipment back to the DC. The OMS knows about the return order, and we expect D365 to be ready to receive it with a work order when the truck arrives.

**Alex Chen:** We enable the returns process on the source system and configure three disposition codes — resell, damaged, requires-QA. The OMS sets the disposition on the return order; D365 reads it and routes the product to the right location automatically. Elena, does that match your workflow?

**Elena Strickland:** Yes. The stores already classify the return in the OMS at point of receipt. We just need the DC to honor that classification.

**Maya Hollister:** What about manual inbound orders — say a supplier delivers outside of a PO, or we have an emergency stock transfer?

**Alex Chen:** The "Enable manual inbound shipment order creation" flag on the source system handles that. DC office staff can create an inbound order directly in D365 without waiting for the OMS to send a message.

**Maya Hollister:** Good. We need that for edge cases.

**Alex Chen:** Source system settings confirmed. **Decision 8.** Now — consignees. You have eight stores. How do you want to group them for wave routing purposes?

**Linh Tran:** We run two delivery routes. The metro route hits Seattle, Bellevue, Redmond, and Kirkland daily — sometimes twice if Seattle has a big day. The regional route is Tacoma, Spokane, Everett — alternate days. Online is its own thing; those go out with a last-mile carrier.

**Alex Chen:** Perfect. Three consignee groups: WA-METRO, WA-REGIONAL, ONLINE. Eight individual consignees. Wave filters can be built on those groups so we can process metro wave and regional wave separately if needed. **Decision 9 confirmed.**

---

---

## Session 5 — March 5, 2026: Wave Processing and Replenishment

**Location:** Video call  
**Duration:** 2 hours

---

**Alex Chen:** Wave processing. The outbound wave is the engine that converts released shipment orders into pick work. The key design question is: auto-process or manual trigger?

**Derek Fowler:** Overall I want the system to run itself during operating hours. What does auto-process do exactly?

**Alex Chen:** Auto-process means when shipments are added to a wave, the wave executes automatically — allocates inventory, creates pick work, releases to workers — without anyone in the office having to push a button. You'd still have supervisors monitoring, but the system doesn't wait for manual approval on every wave cycle.

**Derek Fowler:** For the standard daily DC run — store replenishment orders, regular receiving — yes, I want that automated. But we have those seasonal bulk builds — like spring garden pre-positioning — those I want my ops supervisor to eyeball before we start picking 500 pallets of mulch.

**Alex Chen:** Straightforward solution — two wave templates. WAVE-OUTBOUND: auto-process on, auto-confirm on, runs every 30 minutes. WAVE-SEASONAL: auto-process off, manual trigger only. The seasonal wave only fires when a supervisor explicitly releases it.

**Derek Fowler:** That's exactly right. **Confirmed.**

**Alex Chen:** Replenishment. Your pick faces are replenished from the bulk zone. How are pick quantities managed today?

**Derek Fowler:** Manually. One of my guys walks the aisles at 6 AM, eyeballs what looks low, and puts a paper replen request in the office. It's a disaster.

**Alex Chen:** *(smiling)* So there's strong appetite for system-directed replenishment. I'd recommend three templates. Min/Max on a four-hour cycle for the continuous replenishment — keeps pick faces topped up. Wave demand triggered during wave processing — if a pick face drops below minimum mid-wave, it auto-creates replenishment work before the pick starts. And a third seasonal template for the manual pre-build — you run it once in February for Garden, once in May for Power Tools and Lumber.

**Maya Hollister:** What are the min/max values set to?

**Alex Chen:** Those are configured per location in the system, so you can set them item by item or by category. During Phase 1 master data prep, Derek's team will establish the initial min/max parameters. The seasonal multipliers — Power Tools need double stock in June-July, Paint & Finishes peaks in April —

**Sam Keogh:** We have those numbers in our demand forecast. I can provide a category-by-season multiplier table.

**Alex Chen:** Perfect. We'll configure the seasonal multipliers into the replenishment template. **Decision 11 confirmed — three replenishment templates.**

---

---

## Session 6 — March 10, 2026: Mobile Device Design and Cycle Counting

**Location:** Zava DIY DC, Seattle — Training Room  
**Duration:** 2.5 hours

---

**Alex Chen:** Mobile device setup — this is the most visible part of the project for your floor workers. Let me show you the menu structure I'm proposing. *(shares screen)*

**Derek Fowler:** Can we show this to the team? I've got two of my lead pickers here — Jamie and Rodrigo. They're the ones using these devices every day.

**Alex Chen:** Please. Jamie, Rodrigo — welcome.

**Rodrigo Medina (Lead Picker):** Thanks. How many screens do we have to go through to confirm a pick?

**Alex Chen:** Scan the LP, confirm quantity, scan the destination location. Three screens for a standard pick. If it matches the system, you're done in under ten seconds.

**Jamie Kwon (Lead Picker):** What about when it doesn't match? Like we get to a location and the item isn't there?

**Alex Chen:** Short-pick exception. You confirm the short, the system creates an override pick work from the next available location. Derek, do you want supervisor authorization on short picks?

**Derek Fowler:** For regular items, no — the pickers can handle it. For high-value stuff — Power Tools, higher-end hardware — yes, I want a supervisor to confirm.

**Alex Chen:** We'll configure that per work exception by category. The system will prompt for supervisor authorization only for the flagged product categories.

**Jamie Kwon:** Cluster picking — we do batched store picks for the metro route, right? Can the device handle multiple orders at once?

**Alex Chen:** Yes, that's the cluster pick functionality. You're picking for up to four stores in one pass through the aisle. The device tells you exactly how many units of each item go into which tote. Derek, I proposed a 4-store cluster — does that fit your tote configuration?

**Derek Fowler:** We've got a cart that holds four totes, one per store. Four is right.

**Maya Hollister:** Menu structure — I want to understand the access control model.

**Alex Chen:** Each worker's mobile device user account is assigned specific menus. An inbound receiver only sees the inbound menu. A picker only sees outbound. The main root menu is ZAVA-MAIN, with five sub-menus: Inbound, Outbound, Inventory, Returns, Inquiries. You assign which sub-menus a worker can access via their warehouse security profile.

**Derek Fowler:** That works for us. My team is specialized — inbound team, outbound team, inventory team. They don't need to see each other's work.

**Alex Chen:** Cycle counting, Sam — does the current weekly count cadence work or do you want to make changes?

**Sam Keogh:** The fast-mover count needs to be weekly. We have real volatility in Hand Tools and Hardware, especially October through December. Annual full count in January when things are quiet. And the seasonal transition counts — I need a count of the SEASONAL zone before we reload it in February and after we pull it down in October, so we know exactly what we're starting with.

**Alex Chen:** Three cycle count plans: CC-FAST for weekly high-velocity aisles, CC-ANNUAL for January, CC-SEASON for February and October transitions. Variance threshold for ad-hoc count trigger?

**Sam Keogh:** Five percent. If the system shows more than 5% deviation from our last count at a location, trigger an ad-hoc count.

**Alex Chen:** **Decisions 13, 14, 15 all confirmed.**

---

---

## Session 7 — March 12, 2026: Load Building and Shipment Consolidation

**Location:** Video call  
**Duration:** 1.5 hours

---

**Linh Tran:** I want to make sure we don't end up with three half-empty loads going to Bellevue on the same day because the system can't consolidate. That's happened before with our previous routing software.

**Alex Chen:** Shipment consolidation policies address exactly that. We can configure two policies. The first consolidates by consignee — all orders for the same store automatically go on the same load. The second adds date — same store, same calendar day, one load. So if the OMS sends three separate replenishment orders for Bellevue Store across the morning, they all roll up into one outbound load.

**Linh Tran:** That's what I need. And for the lumber loads?

**Alex Chen:** Lumber gets a separate load template — ZAVA-LOAD-LBR — configured for flatbed capacity. The load building strategy for that template is by category: LB category items load separately from the general merchandise to keep the flatbed requirement calculation accurate.

**Derek Fowler:** The auto-release timing — you mentioned 15 minutes. During early morning, from about 4 AM to 6 AM, the OMS sends the overnight orders. Can we have those queue up and not release until 6 AM when the outbound team starts?

**Alex Chen:** The auto-release schedule is configurable with an operating hours window. We'll set it to 06:00–22:00 Pacific. Orders before 6 AM queue in D365 and release in the first batch at 06:00.

**Derek Fowler:** Perfect. My team arrives at 6:15, they like to have work waiting for them.

**Maya Hollister:** **Decisions 16 and 17 confirmed then.** Alex, the 15-minute cadence — is that optimal? Could we go shorter?

**Alex Chen:** You could go to 5 minutes, but I'd caution against it. Each release cycle creates waves, which create work orders. At very short intervals you can create wave contention — two cycles fighting over the same inventory. Fifteen minutes gives the wave processor time to complete before the next release hits. With the business volume you've shared, 15 minutes keeps the queue moving perfectly.

**Maya Hollister:** Understood. Fifteen minutes stands.

---

---

## Session 8 — March 15, 2026: Background Jobs and Number Sequences

**Location:** Video call  
**Duration:** 1 hour

---

**Priya Anand:** I want to talk through the background process schedule. These jobs run in the D365 batch framework, and I need to make sure we aren't creating resource contention during operating hours.

**Alex Chen:** The five source system automation jobs are created automatically when we create the ZAVA-OMS source system — D365 does that for you. Those run at 1-minute or 10-minute intervals. The workload management jobs — inbound and outbound order completion — at 10-minute intervals. The wave processor at 30 minutes. The only heavy one is the min/max replenishment — I'd suggest every 4 hours, not more frequent. Running it every hour on a large item catalog can put significant load on the job server.

**Priya Anand:** Agreed. Four hours is fine for replenishment — pick faces won't drain out in under four hours on most items.

**Alex Chen:** Number sequences — all company-scoped for Phase 1. Priya, any objection?

**Priya Anand:** None. Single legal entity, single company. Company scope is the right boundary.

**Jordan Bates:** Can we go over the WHS-LP format — ZAV-LP-##########? Ten digits, that's 10 billion license plates. A bit generous.

**Alex Chen:** *(laughs)* Industry standard is to over-provision LP sequences. LP numbers are never reused and they show up on physical labels, so you want a consistent length. Ten digits also prevents leading zero collisions in barcode scanners. Leave it at ten.

**Jordan Bates:** Understood. **Decision 19 confirmed** for all ten sequences.

---

---

## Session 9 — March 18, 2026: Product Filters, Labels, and Returns Close-Out

**Location:** Zava DIY HQ Conference Room A  
**Duration:** 2 hours

---

**Maya Hollister:** Last design session. We need to close on product filters, label design, and returns.

**Alex Chen:** Product filters. You have nine merchandise categories. Each category maps to a specific pick aisle in the DC. For location directives to route put-aways to the right aisle automatically, product filter codes need to match those nine categories.

**Maya Hollister:** That's straightforward. PF-EL through PF-SO. What about items that span categories?

**Derek Fowler:** That's rare. Maybe a combo kit — hammer and nails — but those are usually slotted with the dominant category.

**Alex Chen:** One filter code per product is the standard. Multi-category products get the dominant category. We'll also add three product attribute flags: SEASONAL for items that need the pre-season hold logic, HAZMAT for paint and chemical products that have safety handling requirements, and HEAVY for lumber over 50 pounds that needs pallet-only handling.

**Elena Strickland:** HAZMAT — does D365 do anything with that flag automatically, or is it just informational?

**Alex Chen:** For Phase 1 it's informational — it drives the work exception configuration for over-receive and the safety text instructions on the mobile device for receiving. Full hazmat documentation routing would be a Phase 2 enhancement. Priya flagged this as a compliance check item — we should confirm before go-live whether Paint & Finishes products require any regulatory documentation beyond our current process.

**Elena Strickland:** I'll get that answer from our compliance team.

**Alex Chen:** Labels. Three types — LP labels for bulk storage, wave pick labels for the cluster picking workflow, and outbound shipment labels for the store receiving team. All auto-printed — LP labels at inbound receiving completion, shipment labels at outbound confirmation.

**Derek Fowler:** We have two ZPL printers at the inbound docks and two at the outbound staging area. Are those compatible?

**Priya Anand:** ZPL is natively supported via D365 document routing. We need the printer hostnames from IT infrastructure — I'll have that as an open item.

**Alex Chen:** Returns — final alignment. Elena, three disposition codes was agreed in Session 4. The mapping is: RETURN-RESELL flows to AVAIL, RETURN-DAMAGED to DAMAGED status, RETURN-QA to QUARANTINE. The mobile device return menu item triggers a work order that routes the product to the appropriate location based on the disposition code on the return order.

**Elena Strickland:** One question — what if a worker receiving a return disagrees with the store's disposition assessment? Like the store marked something RETURN-RESELL but it's clearly damaged?

**Alex Chen:** The work exception model handles this. We configure an override capability on the return receiving menu item — a worker with the QA override permission can change the disposition code at the point of receiving. It generates a notification to the supervisor and creates an audit entry.

**Elena Strickland:** Good. That's a real scenario. Stores aren't always careful with their assessments.

**Maya Hollister:** That's all our design topics closed. Alex, can you summarize the open items before we go?

**Alex Chen:** Five remaining open items: printer hostnames for label routing — Priya by April 5. SKU format spec from the OMS team for the source system item configuration — Jordan by April 10. The warehouse manager worker record for ZAVDC1 — pending HR records being created in D365 by April 15. Over-receive tolerance confirmation — Marcus, you were going to check if 5% is the right call for all categories or if Power Tools needs a tighter tolerance.

**Marcus Webb:** I'll check with my receiving team. Some of those items are high value enough that I'd want a tighter tolerance — maybe 2%.

**Alex Chen:** Flag it as an open item — we'll configure per work class if needed. And the fifth item — compliance review on Paint & Finishes hazmat documentation, Elena by April 20.

**Maya Hollister:** Excellent. Thank you everyone — nine sessions and we have a complete design. Runbook gets finalized this week, and we start configuration the week of March 30. Alex, we're on track?

**Alex Chen:** Fully on track. All decisions are made, all master data prep is in flight. March 30 configuration start is confirmed.

---

*— End of transcript —*

---

*This transcript was compiled from session notes and recordings captured by the project facilitator. It has been edited for clarity and brevity. Decisions referenced herein are formally recorded in document ZAVA-WHS-DEC-001.*
