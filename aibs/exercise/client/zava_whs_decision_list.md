# Zava DIY — Warehouse Management Configuration Decision List

> **Document ID:** ZAVA-WHS-DEC-001  
> **Version:** 1.0  
> **Date:** March 25, 2026  
> **Project:** Zava DIY WHS-Only Mode Configuration — D365 Supply Chain Management  
> **Status:** Approved  
> **Related Runbook:** ZAVA-WHS-RB-001

---

## Purpose

This document captures all implementation decisions made during the design phase of the Zava DIY Warehouse Management module configuration. Each decision includes the rationale and the name of the decision owner.

---

## Decision Log

### D-001 — WHS Deployment Mode: WHS-Only Mode Selected

| Field | Value |
|-------|-------|
| **Decision** | Deploy Warehouse Management in **WHS-Only Mode** (not embedded WMS) |
| **Owner** | IT Architect / Supply Chain Lead |
| **Status** | Approved |
| **Date** | February 12, 2026 |

**Rationale:** Zava DIY operates its own Order Management System (OMS) that handles sales orders and customer billing. The D365 environment is used exclusively for warehouse execution. WHS-Only mode allows the DC to receive inbound and outbound shipment orders from the external OMS via message queues, without requiring full D365 order management. This avoids duplication of order records across two systems and reduces licensing scope.

**Alternatives Considered:** Full embedded WMS (rejected — requires migrating OMS order management into D365), standalone WMS (rejected — target state is D365 full adoption over 3–5 years).

---

### D-002 — Single Distribution Center for Phase 1

| Field | Value |
|-------|-------|
| **Decision** | Configure **one site (ZAVSITE1)** and **one warehouse (ZAVDC1)** for Phase 1 |
| **Owner** | Supply Chain Lead |
| **Status** | Approved |
| **Date** | February 12, 2026 |

**Rationale:** Zava DIY currently operates a single distribution center in Seattle, WA, serving all 7 physical stores and the online channel. Future expansion (e.g., a second DC for Eastern Washington) is out of scope for Phase 1. The design should accommodate multi-warehouse expansion without re-architecture.

---

### D-003 — Zone Architecture: Two Zone Groups, Ten Zones

| Field | Value |
|-------|-------|
| **Decision** | Use two zone groups (ZAVA-STOR, ZAVA-OPS) with ten named zones |
| **Owner** | Warehouse Operations Manager |
| **Status** | Approved |
| **Date** | February 18, 2026 |

**Rationale:** Physical separation of the DC into storage areas and operational areas (receiving, staging, docks, QA, returns) matches the existing facility layout. Storage zones include Bulk, Pick, Seasonal, and Paint — each with different location profile rules. Operational zones manage flow and do not hold long-term inventory.

**Key zones agreed upon:**

| Zone Group | Zone | Purpose |
|------------|------|---------|
| ZAVA-STOR | BULK | Pallet-level goods |
| ZAVA-STOR | PICK | Active pick faces |
| ZAVA-STOR | SEASONAL | Garden & Outdoor seasonal items |
| ZAVA-STOR | PAINT | Temperature-stable paint storage |
| ZAVA-OPS | RECV | Inbound receiving bays |
| ZAVA-OPS | STG-IN | Inbound staging / cross-dock |
| ZAVA-OPS | STG-OUT | Outbound staging / pre-load |
| ZAVA-OPS | DOCK | Truck dock doors |
| ZAVA-OPS | QA | Quality inspections and holds |
| ZAVA-OPS | RETURN | Returns processing |

---

### D-004 — Location Format: AISLE-RACK-SHELF-BIN for Storage Aisles

| Field | Value |
|-------|-------|
| **Decision** | Adopt a 4-segment location naming convention: `AA-NN-X-NN` for pick/bulk storage |
| **Owner** | Warehouse Operations Manager |
| **Status** | Approved |
| **Date** | February 18, 2026 |

**Rationale:** The existing physical labeling in the DC uses a 4-segment structure (Aisle 2-char / Rack 2-digit / Shelf letter A–D / Bin 2-digit). Aligning the D365 location IDs to the physical labels eliminates re-labeling cost and reduces picker errors. Separate simpler formats (DOCK-FMT, STAGE-FMT) are used for operational zones.

---

### D-005 — License Plate Tracking: Enabled for Bulk and Staging; Disabled for Pick Faces

| Field | Value |
|-------|-------|
| **Decision** | LP tracking **enabled** for BULK, STG-IN, STG-OUT, QA, and Returns; **disabled** for RECV and PICK profiles |
| **Owner** | Warehouse Operations Manager |
| **Status** | Approved |
| **Date** | February 18, 2026 |

**Rationale:** Pick faces are replenished from bulk; tracking LPs at the individual pick location adds overhead without benefit since pick faces use open-face picking. Bulk storage and staging areas require LP control for accurate load building and quality traceability.

---

### D-006 — Inventory Statuses: Five Statuses Defined

| Field | Value |
|-------|-------|
| **Decision** | Implement five inventory statuses: AVAIL, QUARANTINE, DAMAGED, RETURN-PROC, SEASONAL-HLD |
| **Owner** | Supply Chain Lead / Quality Manager |
| **Status** | Approved |
| **Date** | February 25, 2026 |

**Rationale:** Standard D365 available/blocked model is insufficient for Zava DIY's operating model. The SEASONAL-HLD status enables pre-season stocking of Garden & Outdoor items without releasing them for picking until the season opens. QUARANTINE and RETURN-PROC statuses support the returns handling workflow. Only AVAIL is reservation-enabled.

---

### D-007 — Reservation Hierarchy: Site and Warehouse Above Wave; Location and LP Below

| Field | Value |
|-------|-------|
| **Decision** | Use hierarchy RETAIL-STD: dimensions above wave = Site, Warehouse; below wave = Location, License Plate |
| **Owner** | Supply Chain Lead |
| **Status** | Approved |
| **Date** | February 25, 2026 |

**Rationale:** Standard retail DC practice. Orders from the OMS specify a site and warehouse; the warehouse management system resolves exact location and LP at wave time. Batch and serial number tracking is not required for Zava DIY's product catalog at this time.

---

### D-008 — Source System Integration: Single ZAVA-OMS Source System

| Field | Value |
|-------|-------|
| **Decision** | Configure one source system record **(ZAVA-OMS)** as the sole external integration point |
| **Owner** | IT Architect |
| **Status** | Approved |
| **Date** | March 3, 2026 |

**Rationale:** All inbound and outbound shipment orders originate from the Zava OMS. A single source system simplifies message processing and audit tracing. Future additional source systems (e.g., a vendor portal for drop-ship) can be added without altering the current design.

**Key settings:**

| Setting | Decision |
|---------|----------|
| Returns enabled | Yes — stores send return orders to DC via OMS |
| Manual inbound order creation | Yes — DC staff can create ad-hoc inbound orders |
| Product master source system | ZAVA-OMS — D365 item master derives from OMS catalog |
| Outbound policy | ZAVA-OUTBOUND-POLICY with enforced shipment-to-order matching |
| Packing slip posting delay | 1 day (allows for same-day correction window) |
| Receipt posting delay | 1 day |

---

### D-009 — Consignee Structure: Three Store Groups, Eight Consignees

| Field | Value |
|-------|-------|
| **Decision** | Group stores into WA-METRO, WA-REGIONAL, and ONLINE consignee groups |
| **Owner** | Supply Chain Lead |
| **Status** | Approved |
| **Date** | March 3, 2026 |

**Rationale:** Wave filtering and shipment consolidation at the store group level allows the DC to batch outbound work by delivery route. Metro stores (Seattle, Bellevue, Redmond, Kirkland) are served by daily direct delivery. Regional stores (Tacoma, Spokane, Everett) are on alternate-day delivery with larger loads. Online orders are packed individually and handed off to carrier.

---

### D-010 — Outbound Wave Processing: Auto-Process for Standard Wave; Manual for Seasonal

| Field | Value |
|-------|-------|
| **Decision** | WAVE-OUTBOUND = auto-process and auto-confirm; WAVE-SEASONAL = manual trigger |
| **Owner** | Warehouse Operations Manager |
| **Status** | Approved |
| **Date** | March 5, 2026 |

**Rationale:** The standard outbound wave runs on a 30-minute cycle during operating hours with automatic work creation. High-volume seasonal orders (e.g., spring garden pre-build) require supervisor review before wave release due to cross-dock risk and available staging space constraints.

---

### D-011 — Replenishment Strategy: Three Templates (Min/Max, Wave Demand, Seasonal)

| Field | Value |
|-------|-------|
| **Decision** | Implement three replenishment templates with distinct triggers and strategies |
| **Owner** | Supply Chain Lead / Warehouse Operations Manager |
| **Status** | Approved |
| **Date** | March 5, 2026 |

**Rationale:**

| Template | Strategy | Trigger |
|----------|----------|---------|
| REPLEN-MINMAX | Min/Max quantity | Every 4 hours — continuous replenishment |
| REPLEN-DEMAND | Wave demand | Triggered by wave when pick face below minimum |
| REPLEN-SEASON | Fixed quantity | Manual — pre-season build (Feb for Garden; May for Power Tools/Lumber) |

Seasonal multipliers were agreed: Power Tools 2.0× June–July; Paint & Finishes 2.2× April; Garden & Outdoor 1.0× spring build.

---

### D-012 — Packing: Pack by Store Destination

| Field | Value |
|-------|-------|
| **Decision** | Containerize outbound orders by store destination (one shipment per consignee per wave) |
| **Owner** | Warehouse Operations Manager |
| **Status** | Approved |
| **Date** | March 5, 2026 |

**Rationale:** Delivery trucks are dispatched by store route. Mixing consignees in a single load causes unloading errors at stores. Carton containers (SM/MD/LG) are used for most categories; pallet containers for bulk items (Lumber, Power Tools); flat packs for lumber boards.

---

### D-013 — Cycle Counting: Three Plans (Weekly Fast Movers, Annual Full Count, Seasonal Transition)

| Field | Value |
|-------|-------|
| **Decision** | Three cycle count plans covering different frequency, zone, and trigger criteria |
| **Owner** | Inventory Control Manager |
| **Status** | Approved |
| **Date** | March 10, 2026 |

**Rationale:**

| Plan | Zones | Frequency |
|------|-------|-----------|
| CC-FAST | PICK — HT, HW, EL aisles | Weekly |
| CC-ANNUAL | All zones in ZAVDC1 | January annually |
| CC-SEASON | SEASONAL zone only | Feb (spring build) and Oct (fall teardown) |

Ad-hoc count threshold set at 5% variance from system on-hand.

---

### D-014 — Mobile Device Menu: Five Sub-Menus Under One Root Menu

| Field | Value |
|-------|-------|
| **Decision** | Organize 15 menu items into 5 functional sub-menus under ZAVA-MAIN root |
| **Owner** | Warehouse Operations Manager |
| **Status** | Approved |
| **Date** | March 10, 2026 |

**Rationale:** Workers specialize by function (inbound, outbound, inventory, returns, inquiry). Separate sub-menus reduce cognitive load on the device and support role-based access control at the menu level. Cluster picking is included in outbound for high-velocity store picks.

---

### D-015 — Cluster Picking: Enabled for Outbound (4-Zone Cluster)

| Field | Value |
|-------|-------|
| **Decision** | Enable cluster picking with a 4-zone cluster profile (CLUSTER-PICK-4) |
| **Owner** | Warehouse Operations Manager |
| **Status** | Approved |
| **Date** | March 10, 2026 |

**Rationale:** Seattle and Bellevue stores are high-frequency (3.0× and 2.6× order multiplier). A single picker can simultaneously service pick work for up to 4 stores in one pass through the pick aisles, significantly reducing travel time during peak outbound windows.

---

### D-016 — Shipment Consolidation: By Consignee, Then by Consignee + Date

| Field | Value |
|-------|-------|
| **Decision** | Two consolidation policies: CONSOL-BY-STORE and CONSOL-BY-DATE (same-day consolidation) |
| **Owner** | Logistics Lead |
| **Status** | Approved |
| **Date** | March 12, 2026 |

**Rationale:** Most stores receive a single daily delivery. Same-day orders for the same store should be consolidated into one load. The secondary policy (by consignee + ship date) prevents unnecessary multiple small loads to the same store on the same day.

---

### D-017 — Auto-Release to Warehouse: Every 15 Minutes During Operating Hours

| Field | Value |
|-------|-------|
| **Decision** | Configure auto-release batch job for outbound shipment orders on a 15-minute cycle, 06:00–22:00 Pacific |
| **Owner** | IT Architect / Warehouse Operations Manager |
| **Status** | Approved |
| **Date** | March 12, 2026 |

**Rationale:** Zava OMS sends orders throughout the day as stores place replenishment requests. A 15-minute release cycle ensures the DC always has fresh work without overwhelming the wave processor. Outside operating hours, orders queue and are released at 06:00.

---

### D-018 — Background Process Intervals: Agreed Schedule

| Field | Value |
|-------|-------|
| **Decision** | Background process automation schedule as defined in Phase 18 of the runbook |
| **Owner** | IT Architect |
| **Status** | Approved |
| **Date** | March 15, 2026 |

**Key intervals:**

| Process | Interval |
|---------|----------|
| Process source system product messages | 1 minute |
| Process shipment order messages | 1 minute |
| Publish warehouse inventory update log | 10 minutes |
| Post shipment packing slips | 10 minutes (1-day posting delay) |
| Post shipment receipts | 10 minutes (1-day posting delay) |
| Complete inbound warehouse orders | 10 minutes |
| Complete outbound warehouse orders | 10 minutes |
| Replenishment (min/max) | Every 4 hours |
| Wave processing | Every 30 minutes |
| Process warehouse app events | 1 minute |

---

### D-019 — Number Sequence Scope: All at Company (ZAV1) Level

| Field | Value |
|-------|-------|
| **Decision** | All 10 WHS number sequences scoped to **company ZAV1**, not warehouse-level |
| **Owner** | IT Architect |
| **Status** | Approved |
| **Date** | March 15, 2026 |

**Rationale:** Single-warehouse deployment in Phase 1 makes company-level scoping equivalent to warehouse-level. Company scoping is simpler to maintain and avoids the need to reconfigure sequences if a second warehouse is added to the same legal entity later.

---

### D-020 — Product Filter Model: Nine Category Filter Codes

| Field | Value |
|-------|-------|
| **Decision** | Create nine product filter codes matching Zava DIY's nine merchandise categories |
| **Owner** | Supply Chain Lead |
| **Status** | Approved |
| **Date** | March 18, 2026 |

**Rationale:** Location directives for put-away route products to category-specific aisles. Without category-level filter codes, zone and aisle routing cannot be automated. Three additional product attribute flags (SEASONAL, HAZMAT, HEAVY) support special handling rules for Paint & Finishes and Lumber.

---

### D-021 — Label Printing: Three Label Types with Printer Routing

| Field | Value |
|-------|-------|
| **Decision** | Implement LP label, wave pick label, and outbound shipment label with document routing to dock printers |
| **Owner** | Warehouse Operations Manager / IT |
| **Status** | Approved |
| **Date** | March 18, 2026 |

**Rationale:** License plate labels are mandatory for bulk storage LP tracking (D-005). Wave labels support cluster picking. Outbound shipment labels are required by store receiving staff for PO matching. Label printing is triggered automatically at receiving completion and shipment confirmation.

---

### D-022 — Return Processing: Three Disposition Codes

| Field | Value |
|-------|-------|
| **Decision** | Three return disposition codes: RETURN-RESELL (→ AVAIL), RETURN-DAMAGED (→ DAMAGED), RETURN-QA (→ QUARANTINE) |
| **Owner** | Supply Chain Lead / Quality Manager |
| **Status** | Approved |
| **Date** | March 18, 2026 |

**Rationale:** Store returns arrive at the DC with a disposition intent already set in the OMS. The WMS maps OMS disposition codes to D365 inventory status transitions at the point of receiving, enabling automated work routing without manual status overrides.

---

## Open Items

| ID | Issue | Owner | Target Date |
|----|-------|-------|-------------|
| OI-001 | Confirm exact printer hostnames for document routing setup (LP and shipping labels) | IT Infrastructure | April 5, 2026 |
| OI-002 | Validate SKU format mapping from Zava OMS product catalog for Source System Items configuration | Data Migration Lead | April 10, 2026 |
| OI-003 | Assign warehouse manager worker record to ZAVDC1 once HR records are created in D365 | HR / WMS Config Lead | April 15, 2026 |
| OI-004 | Confirm over-receive tolerance percentage with DC Operations (currently proposed at 5%) | DC Operations Manager | April 5, 2026 |
| OI-005 | Determine if Paint & Finishes category requires HAZMAT documentation routing (regulatory check) | Compliance | April 20, 2026 |
