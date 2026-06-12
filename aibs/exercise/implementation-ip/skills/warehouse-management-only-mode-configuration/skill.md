---
name: warehouse-management-only-mode-configuration
description: Complete configuration steps for Dynamics 365 Warehouse Management in WHS-only mode

---

# Warehouse Management Only Mode — Configuration Steps

> **Source**: Business Process Catalog (BPC) Reference — DEC 2025.1  
> **Scope**: Dynamics 365 Supply Chain Management — Warehouse Management module in **Warehouse Management only** mode  

---

## Overview

**Warehouse Management only mode** (also known as WHS-only mode) allows organizations to run Dynamics 365 Warehouse Management as a standalone workload, decoupled from the full Finance and Operations ERP. In this mode, the warehouse connects to an external source system (ERP) via inbound/outbound shipment orders and warehouse management integration entities.

This document lists all configuration steps required, organized by setup area.

---

## Table of Contents

1. [Warehouse Management Parameters]
2. [Warehouse Structure Setup]
3. [Warehouse Management Integration]
4. [Location Directives & Work Templates]
5. [Wave Processing Setup]
6. [Replenishment Setup]
7. [Mobile Device Setup]
8. [Load & Shipment Setup]
9. [Containerization & Packing]
10. [Product Filters & Attributes]
11. [Work Management]
12. [Cycle Counting]
13. [Return Items]
14. [Shipping Setup]
15. [Label Printing]
16. [External Services]
17. [Configuration Wizards]
18. [Number Sequences]
19. [Back-Office Workload Management (Batch Jobs)]
20. [Periodic Tasks & Clean-Up Jobs]
21. [Business Processes Covered]

---

## 1. Warehouse Management Parameters

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 1.1 | **Warehouse management parameters** | Warehouse management > Setup > Warehouse management parameters | Parameters |
| 1.2 | **Number sequences (Warehouse Management)** | Warehouse management > Setup > Warehouse management parameters > Number sequences | Number sequences |
| 1.3 | **Number sequences (Inventory Warehouse Management)** | Warehouse management > Setup > Warehouse management parameters > Number sequences | Number sequences |

> Set up general warehouse parameters to support business processes: default location types, work policies, wave processing defaults, mobile device settings, and general behavior flags.

---

## 2. Warehouse Structure Setup

### 2.1 Sites & Warehouses

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 2.1.1 | **Sites** | Warehouse management > Setup > Warehouse > Sites | List of values |
| 2.1.2 | **Warehouses** | Warehouse management > Setup > Warehouse > Warehouses | List of values |
| 2.1.3 | **Warehouse groups** | Warehouse management > Setup > Warehouse > Warehouse groups | List of values |

### 2.2 Zones & Locations

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 2.2.1 | **Warehouse zone groups** | Warehouse management > Setup > Warehouse > Warehouse zone groups | List of values |
| 2.2.2 | **Zones** | Warehouse management > Setup > Warehouse > Zones | List of values |
| 2.2.3 | **Location types** | Warehouse management > Setup > Warehouse > Location types | List of values |
| 2.2.4 | **Location formats** | Warehouse management > Setup > Warehouse > Location formats | List of values |
| 2.2.5 | **Location profiles** | Warehouse management > Setup > Warehouse > Location profiles | List of values |
| 2.2.6 | **Locations** | Warehouse management > Setup > Warehouse > Locations | List of values |
| 2.2.7 | **Location setup wizard** | Warehouse management > Setup > Warehouse > Location setup wizard | Wizard |
| 2.2.8 | **Location stocking limits** | Warehouse management > Setup > Warehouse > Location stocking limits | List of values |
| 2.2.9 | **Fixed locations** | Warehouse management > Setup > Warehouse > Fixed locations | List of values |

### 2.3 Units & License Plates

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 2.3.1 | **Unit sequence groups** | Warehouse management > Setup > Warehouse > Unit sequence groups | List of values |
| 2.3.2 | **License plates** | Warehouse management > Setup > Warehouse > License plates | List of values |
| 2.3.3 | **Pack size categories** | Warehouse management > Setup > Warehouse > Pack size categories | List of values |

### 2.4 Dock Management

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 2.4.1 | **Dock management profiles** | Warehouse management > Setup > Warehouse > Dock management profiles | List of values |

### 2.5 Catch Weight

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 2.5.1 | **Catch weight item handling policies** | Warehouse management > Setup > Warehouse > Catch weight item handling policies | List of values |

---

## 3. Warehouse Management Integration (WHS-Only Specific)

> These configuration items are **specific to Warehouse Management only mode** — they define the connection between the warehouse and the external source system (ERP).

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 3.1 | **Source systems** | Warehouse management > Setup > Warehouse management integration > Source systems | List of values |
| 3.2 | **Source system items** | Warehouse management > Setup > Warehouse management integration > Source system items | List of values |
| 3.3 | **Source system disposition codes** | Warehouse management > Setup > Warehouse management integration > Source system disposition codes | List of values |
| 3.4 | **External warehouse management system** | Warehouse management > Setup > Warehouse management integration > External warehouse management system | List of values |
| 3.5 | **Consignee groups** | Warehouse management > Setup > Warehouse management integration > Consignee groups | List of values |
| 3.6 | **Consignees** | Warehouse management > Setup > Warehouse management integration > Consignees | List of values |
| 3.7 | **Consigner groups** | Warehouse management > Setup > Warehouse management integration > Consigner groups | List of values |
| 3.8 | **Consigners** | Warehouse management > Setup > Warehouse management integration > Consigners | List of values |
| 3.9 | **Warehouse inventory owner** | Warehouse management > Setup > Warehouse management integration > Warehouse inventory owner | List of values |

### Key Concepts for WHS-Only Mode

- **Source systems**: Define the external ERP systems that send orders to the warehouse
- **Source system items**: Map external item identifiers to warehouse items
- **Source system disposition codes**: Map external disposition codes used for return/quality processing
- **Consignees/Consigners**: Define the parties receiving/shipping goods (customers and vendors in the external system)
- **Inbound shipment orders**: Replace purchase orders — received from source system for inbound processing
- **Outbound shipment orders**: Replace sales orders — received from source system for outbound processing

---

## 4. Location Directives & Work Templates

### 4.1 Location Directives

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 4.1.1 | **Location directives** | Warehouse management > Setup > Location directives | List of values |
| 4.1.2 | **Directive codes** | Warehouse management > Setup > Location directives (Directive codes) | List of values |
| 4.1.3 | **Location directive failures** | Warehouse management > Setup > Work > Location directive failures | List of values |

### 4.2 Work Templates

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 4.2.1 | **Work templates** | Warehouse management > Setup > Work > Work templates | List of values |
| 4.2.2 | **Work audit templates** | Warehouse management > Setup > Work > Work audit templates | List of values |
| 4.2.3 | **Work exceptions** | Warehouse management > Setup > Work > Work exceptions | List of values |
| 4.2.4 | **Work pools** | Warehouse management > Setup > Work > Work pools | List of values |
| 4.2.5 | **Work classes** | Warehouse management > Setup > Work > Work classes | List of values |
| 4.2.6 | **Work policies** | Warehouse management > Setup > Work > Work policies | List of values |

### 4.3 Cross-Docking & Anchoring

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 4.3.1 | **Cross docking policy** | Warehouse management > Setup > Work > Cross docking policy | List of values |
| 4.3.2 | **Anchoring groups** | Warehouse management > Setup > Work > Anchoring groups | List of values |

### 4.4 Work User Access

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 4.4.1 | **Work user access policies** | Warehouse management > Setup > Work user access policies | List of values |

---

## 5. Wave Processing Setup

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 5.1 | **Wave templates** | Warehouse management > Setup > Waves > Wave templates | List of values |
| 5.2 | **Wave process methods** | Warehouse management > Setup > Waves > Wave process methods | List of values |
| 5.3 | **Wave step codes** | Warehouse management > Setup > Waves > Wave step codes | List of values |
| 5.4 | **Wave attributes** | Warehouse management > Setup > Waves > Wave attributes | List of values |
| 5.5 | **Wave filters** | Warehouse management > Setup > Waves > Wave filters | List of values |
| 5.6 | **Wave notification policies** | Warehouse management > Setup > Waves > Wave notification profiles | List of values |
| 5.7 | **Outbound workload capacity** | Warehouse management > Setup > Waves > Outbound workload capacity | List of values |

---

## 6. Replenishment Setup

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 6.1 | **Replenishment templates** | Warehouse management > Setup > Replenishment > Replenishment templates | List of values |
| 6.2 | **Request types** | Warehouse management > Setup > Replenishment > Request types | List of values |
| 6.3 | **Slotting templates** | Warehouse management > Setup > Replenishment > Slotting templates | List of values |
| 6.4 | **Slotting unit of measure tiers** | Warehouse management > Setup > Replenishment > Slotting unit of measure tiers | List of values |

---

## 7. Mobile Device Setup

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 7.1 | **Mobile device menu items** | Warehouse management > Setup > Mobile device > Mobile device menu items | List of values |
| 7.2 | **Mobile device menu** | Warehouse management > Setup > Mobile device > Mobile device menu | List of values |
| 7.3 | **Mobile device display settings** | Warehouse management > Setup > Mobile device > Mobile device display settings | List of values |
| 7.4 | **Mobile device text instructions** | Warehouse management > Setup > Mobile device > Mobile device text instructions | List of values |
| 7.5 | **Cluster profiles** | Warehouse management > Setup > Mobile device > Cluster profiles | List of values |
| 7.6 | **Detour steps and detour step assignment** | Warehouse management > Setup > Mobile device > Detours | List of values |
| 7.7 | **Promoted fields and step priorities** | Warehouse management > Setup > Mobile device > Promoted fields | List of values |
| 7.8 | **Custom icons and step titles** | Warehouse management > Setup > Mobile device > Step icons and titles | List of values |

> Set up mobile device menus and menu items for all WHS processes: receiving, put-away, picking, packing, cycle counting, replenishment, and movement.

---

## 8. Load & Shipment Setup

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 8.1 | **Load templates** | Warehouse management > Setup > Load > Load templates | List of values |
| 8.2 | **Load building templates** | Warehouse management > Setup > Load > Load building templates | List of values |
| 8.3 | **Shipment consolidation policies** | Warehouse management > Setup > Release to warehouse > Shipment consolidation policies | List of values |
| 8.4 | **Auto release to warehouse** | Warehouse management > Setup > Release to warehouse > Automatic release to warehouse | List of values |

---

## 9. Containerization & Packing

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 9.1 | **Container types** | Warehouse management > Setup > Containers > Container types | List of values |
| 9.2 | **Container groups** | Warehouse management > Setup > Containers > Container groups | List of values |
| 9.3 | **Container packing policies** | Warehouse management > Setup > Containers > Container packing policies | List of values |
| 9.4 | **Container build templates** | Warehouse management > Setup > Containers > Container build templates | List of values |
| 9.5 | **Packing profiles** | Warehouse management > Setup > Packing > Packing profiles | List of values |
| 9.6 | **Containerization groups** | Warehouse management > Setup > Containers > Containerization groups | List of values |
| 9.7 | **Container closing profiles** | Warehouse management > Setup > Containers > Container closing profiles | List of values |

---

## 10. Product Filters & Attributes

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 10.1 | **Product filter codes** | Warehouse management > Setup > Product filters > Product filter codes | List of values |
| 10.2 | **Product filter groups** | Warehouse management > Setup > Product filters > Product filter groups | List of values |
| 10.3 | **Product filter attributes** | Warehouse management > Setup > Product filters > Product filter attributes | List of values |

---

## 11. Work Management

### 11.1 Worker Setup

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 11.1.1 | **Workers** | Warehouse management > Setup > Worker | List of values |

> All warehouse worker operations (picking, moving, counting) are recorded using mobile device scanning. Each worker must be registered.

### 11.2 Inventory Statuses

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 11.2.1 | **Inventory statuses** | Warehouse management > Setup > Inventory > Inventory statuses | List of values |
| 11.2.2 | **Inventory status change** | Warehouse management > Setup > Inventory > Inventory status change rules | List of values |
| 11.2.3 | **Reservation hierarchies** | Warehouse management > Setup > Inventory > Reservation hierarchies | List of values |

---

## 12. Cycle Counting

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 12.1 | **Cycle count plans** | Warehouse management > Setup > Cycle counting > Cycle count plans | List of values |
| 12.2 | **Cycle count thresholds** | Warehouse management > Setup > Cycle counting > Cycle count thresholds | List of values |
| 12.3 | **Cycle count reasons** | Warehouse management > Setup > Cycle counting > Cycle count reasons | List of values |

---

## 13. Return Items

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 13.1 | **Return item policies** | Warehouse management > Setup > Return items > Return item policies | List of values |

---

## 14. Shipping Setup

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 14.1 | **Outbound shipment processing policies** | Warehouse management > Setup > Shipping > Outbound shipment processing policies | List of values |

---

## 15. Label Printing

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 15.1 | **Document routing layouts** | Warehouse management > Setup > Document routing > Document routing layouts | List of values |
| 15.2 | **Document routing** | Warehouse management > Setup > Document routing > Document routing | List of values |
| 15.3 | **Wave label templates** | Warehouse management > Setup > Wave label templates | List of values |
| 15.4 | **License plate label routing** | Warehouse management > Setup > Document routing > License plate label routing | List of values |

---

## 16. External Services

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 16.1 | **External service instances** | Warehouse management > Setup > External Services > External service instances | List of values |

---

## 17. Configuration Wizards

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| 17.1 | **Warehouse management initiation wizard** | Warehouse management > Setup > Wizards > Warehouse management initiation wizard | Wizard |
| 17.2 | **Inbound configuration wizard** | Warehouse management > Setup > Wizards > Inbound configuration wizard | Wizard |
| 17.3 | **Outbound configuration wizard** | Warehouse management > Setup > Wizards > Outbound configuration wizard | Wizard |

> Use these wizards to accelerate the initial setup of warehouse management and validate the configuration.

---

## 18. Number Sequences

| # | Configuration Item | Menu Path |
|---|---|---|
| 18.1 | Number sequences: Warehouse Management | Warehouse management > Setup > Warehouse management parameters > Number sequences |
| 18.2 | Number sequences: Inventory Warehouse Management | Warehouse management > Setup > Warehouse management parameters > Number sequences |

---

## 19. Back-Office Workload Management (Batch Jobs)

> These batch jobs are critical for **WHS-only mode** — they synchronize orders and status between the warehouse and the external source system.

| # | Job | Menu Path |
|---|---|---|
| 19.1 | **Scale unit to hub message processor** | Warehouse management > Periodic tasks > Back-office workload management |
| 19.2 | **Complete inbound warehouse orders** | Warehouse management > Periodic tasks > Back-office workload management |
| 19.3 | **Complete outbound warehouse orders** | Warehouse management > Periodic tasks > Back-office workload management |
| 19.4 | **Generate missing outbound warehouse orders** | Warehouse management > Periodic tasks > Back-office workload management |
| 19.5 | **Register source order receipts** | Warehouse management > Periodic tasks > Back-office workload management |
| 19.6 | **Create source document details** | Warehouse management > Periodic tasks > Workload Management |
| 19.7 | **Process wave table records** | Warehouse management > Periodic tasks > Workload Management |
| 19.8 | **Warehouse hub to scale unit message processor** | Warehouse management > Periodic tasks > Workload Management |
| 19.9 | **Process warehouse order line receipts** | Warehouse management > Periodic tasks > Workload Management |
| 19.10 | **Create external warehouse inbound shipment order requests** | Warehouse management > Periodic tasks |
| 19.11 | **Inbound shipment order receiving completed** | Warehouse management > Periodic tasks |
| 19.12 | **Process outbound shipments** | Warehouse management > Periodic tasks |
| 19.13 | **Create source system on-hand inventory report** | Warehouse management > Inquiries and reports > Physical inventory reconciliation |

---

## 20. Periodic Tasks & Clean-Up Jobs

### 20.1 Release to Warehouse

| # | Job | Menu Path |
|---|---|---|
| 20.1.1 | Automatic release of purchase orders | Warehouse management > Release to warehouse |
| 20.1.2 | Automatic release of sales orders | Warehouse management > Release to warehouse |
| 20.1.3 | Automatic release of transfer orders | Warehouse management > Release to warehouse |
| 20.1.4 | Automatic release of outbound shipment orders | Warehouse management > Release to warehouse |
| 20.1.5 | Automatic release of BOM and formula lines | Warehouse management > Release to warehouse |

### 20.2 Wave Processing

| # | Job | Menu Path |
|---|---|---|
| 20.2.1 | Process waves | Warehouse management > Outbound waves |
| 20.2.2 | Auto add shipments to wave | Warehouse management > Outbound waves |

### 20.3 Replenishment

| # | Job | Menu Path |
|---|---|---|
| 20.3.1 | Load demand replenishment | Warehouse management > Replenishment |
| 20.3.2 | Replenishments | Warehouse management > Replenishment |
| 20.3.3 | Run slotting | Warehouse management > Replenishment |

### 20.4 Cycle Counting

| # | Job | Menu Path |
|---|---|---|
| 20.4.1 | Cycle count work by item | Warehouse management > Cycle counting |
| 20.4.2 | Cycle count work by location | Warehouse management > Cycle counting |

### 20.5 Inventory Operations

| # | Job | Menu Path |
|---|---|---|
| 20.5.1 | Inventory status change | Warehouse management > Periodic tasks |
| 20.5.2 | WMS inventory status change | Warehouse management > Periodic tasks |
| 20.5.3 | Create external inventory adjustment journals | Warehouse management > Periodic tasks |
| 20.5.4 | Post external inventory adjustment journals | Warehouse management > Periodic tasks |
| 20.5.5 | Change reservation hierarchy for items | Warehouse management > Periodic tasks |
| 20.5.6 | Change tracking dimension group for items | Warehouse management > Periodic tasks |

### 20.6 Other Periodic Tasks

| # | Job | Menu Path |
|---|---|---|
| 20.6.1 | Load packing slip posting | Warehouse management > Periodic tasks |
| 20.6.2 | Receiving completed | Warehouse management > Periodic tasks |
| 20.6.3 | Update product receipts | Warehouse management > Periodic tasks |
| 20.6.4 | Process warehouse app events | Warehouse management > Periodic tasks |

### 20.7 Clean-Up Jobs

| # | Job | Menu Path |
|---|---|---|
| 20.7.1 | Wave batch cleanup | Warehouse management > Periodic tasks > Clean up |
| 20.7.2 | Wave label history cleanup | Warehouse management > Periodic tasks > Clean up |
| 20.7.3 | Wave labels cleanup | Warehouse management > Periodic tasks > Clean up |
| 20.7.4 | Wave processing history log cleanup | Warehouse management > Periodic tasks > Clean up |
| 20.7.5 | Wave processing removed shipment cleanup | Warehouse management > Periodic tasks > Clean up |
| 20.7.6 | Wave processing temporary work line cleanup | Warehouse management > Periodic tasks > Clean up |
| 20.7.7 | Work creation history cleanup | Warehouse management > Periodic tasks > Clean up |
| 20.7.8 | Work line history log cleanup | Warehouse management > Periodic tasks > Clean up |
| 20.7.9 | Work user session log cleanup | Warehouse management > Periodic tasks > Clean up |
| 20.7.10 | Clean up work exception logs | Warehouse management > Periodic tasks > Clean up |
| 20.7.11 | Clean up License plate registration history | Warehouse management > Periodic tasks > Clean up |
| 20.7.12 | Clean up ASN/Packing structure | Warehouse management > Periodic tasks > Clean up |
| 20.7.13 | Clean up return details | Warehouse management > Periodic tasks > Clean up |
| 20.7.14 | Clean up hub environment after deleting workloads | Warehouse management > Periodic tasks > Clean up |
| 20.7.15 | Containerization history cleanup | Warehouse management > Periodic tasks > Clean up |
| 20.7.16 | Cycle count plan cleanup | Warehouse management > Periodic tasks > Clean up |
| 20.7.17 | Mobile device activity log cleanup | Warehouse management > Periodic tasks > Clean up |
| 20.7.18 | Optimize location directive queries | Warehouse management > Periodic tasks > Clean up |
| 20.7.19 | Recalculate load/shipment status | Warehouse management > Periodic tasks > Clean up |
| 20.7.20 | Reset shipment order line inventory transaction link type | Warehouse management > Periodic tasks > Clean up |
| 20.7.21 | Catch weight deleted tags purge | Warehouse management > Periodic tasks > Clean up |

---

## 21. Business Processes Covered

The following end-to-end business processes from the BPC catalog are supported in Warehouse Management only mode:

### 21.1 Manage Warehouse Operations (60.10)

| Seq | Process | Description |
|---|---|---|
| 60.10.010 | Define warehouse processes | Establish operational procedures for receiving, put-away, picking, packing, shipping, movements |
| 60.10.020 | Design warehouse layout | Set up physical/logical structure: zones, aisles, bins, shelves, locations |
| 60.10.030 | Document warehouse policies | Formalize rules for inventory handling, quality, safety, compliance |
| 60.10.040 | Manage work assignments | Allocate picking, put-away, counting, replenishment tasks to workers |

### 21.2 Maintain Inventory Levels (60.20)

| Seq | Process | Description |
|---|---|---|
| 60.20.010 | Track supplier managed and consignment inventory | Track inventory owned by suppliers at your locations |
| 60.20.015 | Track customer managed inventory | Track inventory owned by customers at your locations |
| 60.20.020 | Process inventory movements | Transfers between locations, warehouses, or legal entities |
| 60.20.030 | Stage inventory | Temporary holding in designated areas before final put-away/picking |
| 60.20.040 | Count inventory | Physical inventory counts and cycle counts |
| 60.20.060 | Adjust inventory levels | Correct balances due to damage, loss, overages |

### 21.3 Process Inbound Goods (60.30)

| Seq | Process | Description |
|---|---|---|
| 60.30.010 | Receive goods | Register arrival against purchase orders/inbound shipment orders |
| 60.30.020 | Label received goods | Print and apply barcoded labels during/after receipt |
| 60.30.030 | Put away received goods | Move from receiving to storage using system-directed logic |
| 60.30.040 | Cross dock received goods | Directly allocate received goods to outbound orders |
| 60.30.060 | Quarantine received goods | Place in quality hold for inspection before availability |

### 21.4 Process Outbound Goods (60.40)

| Seq | Process | Description |
|---|---|---|
| 60.40.015 | Allocate goods | Reserve inventory for outbound orders |
| 60.40.020 | Release goods for picking | Generate pick tickets and instruct warehouse staff |
| 60.40.030 | Pick goods | Retrieve items from storage using system-directed logic |
| 60.40.040 | Pack goods | Consolidate picked items into containers, generate packing slips |
| 60.40.060 | Load goods for shipping | Move packed goods to dock, assign to shipments |
| 60.40.070 | Cross dock produced goods | Allocate produced goods directly to outbound orders |
| 60.40.080 | Return goods to vendor | Create return orders, process return shipments |

### 21.5 Manage Inventory Quality (60.50)

| Seq | Process | Description |
|---|---|---|
| 60.50.010 | Define quality procedures and tools | — |
| 60.50.020 | Build a quality plan for a product | — |
| 60.50.030 | Maintain quality certifications | — |
| 60.50.040 | Inspect inventory | — |
| 60.50.050 | Report quality non-conformance | — |
| 60.50.060 | Handle quarantine goods | — |
| 60.50.070 | Perform corrective and preventative actions | — |
| 60.50.090 | Scrap defective inventory | — |

### 21.6 Analyze Warehouse Operations (60.80)

| Seq | Process | Description |
|---|---|---|
| 60.80.100 | Define warehouse management KPIs | Inventory accuracy, order picking accuracy, put-away efficiency |
| 60.80.200 | Measure warehouse performance | Reports on picking rates, put-away times, worker productivity |
| 60.80.300 | Analyze inventory levels | Real-time visibility by location, product, batch, or other dimensions |
| 60.80.400 | Report on inventory quality | Quality orders, nonconformance tracking, quarantine management |

---

## Recommended Configuration Sequence

1. **Warehouse management parameters** — Set global defaults
2. **Sites and Warehouses** — Define organizational structure
3. **Warehouse management integration** — Configure source systems, items, consignees/consigners *(WHS-only specific)*
4. **Zones, location types, location profiles** — Design warehouse layout
5. **Location formats and locations** — Create physical locations (or use wizard)
6. **Inventory statuses and reservation hierarchy** — Define inventory tracking
7. **Unit sequence groups and pack size categories** — Set up measurement logic
8. **Work classes, work templates, work policies** — Define how work is created
9. **Location directives** — Define where to put/pick items
10. **Wave templates and wave process methods** — Configure wave processing
11. **Replenishment templates** — Set up replenishment strategies
12. **Containerization and packing** — Configure packing operations
13. **Mobile device menu items and menus** — Build the warehouse app experience
14. **Workers** — Register warehouse workers
15. **Document routing and labels** — Configure label printing
16. **Number sequences** — Verify all number sequences are configured
17. **Back-office workload management jobs** — Schedule batch jobs for WHS-only synchronization
18. **Clean-up jobs** — Schedule periodic maintenance
19. **Validate with wizards** — Run inbound/outbound configuration wizards to verify setup

---

## Delivery Plan Workshops (Success by Design)

| Workshop | Description |
|---|---|
| **60.01 — Inventory to deliver scenario board discovery** | Establish understanding of end-to-end inventory management and delivery process |
| **60.02 — Inventory to deliver storyline design review** | Refine design of inventory management and delivery process |
| **60.10.001 — Manage warehouse operations deep-dive discovery** | Deep-dive into warehouse operations using Dynamics 365 |
| **60.80.001 — Analyze warehouse operations deep-dive discovery** | Deep-dive into warehouse analytics and reporting |
