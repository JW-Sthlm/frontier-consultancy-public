# Customer recap — Contoso Mobility · landing zone scoping call

**Date:** 2026-04-23
**Attendees:** Anya Lindqvist (CIO, Contoso Mobility), Marko Hansen (Head of Cloud Platforms, Contoso Mobility), Frontier Consultancy delivery team
**Source:** Teams meeting transcription + M365 Copilot recap, lightly edited for clarity

---

## What Contoso asked for

Contoso Mobility is migrating from a co-located DC to Azure over the next 12 months. They need a **production landing zone** ready in 4 weeks so the SAP and PCI workstreams can start in parallel. Specifics from the call:

- **Topology:** Hub-spoke. They want one hub for shared services (firewall, DNS, log analytics) and three spokes — corporate, PCI-scoped payments, and SAP.
- **Regions:** Primary **Sweden Central**, paired secondary **West Europe**. DR target is RPO 1h, RTO 4h on the PCI spoke specifically.
- **Compliance:**
  - PCI-DSS scope on the payments spoke. Anya was clear: assessor walks through Q3, "no surprises."
  - GDPR data residency: PII stays in Sweden Central. Cross-region replication only for non-PII.
- **Identity:** Existing Entra ID tenant. Contoso wants Privileged Identity Management on all production access. No standing admin roles.
- **Networking:** Azure Firewall Premium in the hub. Private endpoints everywhere — "no public IPs on data services" (Marko's words).
- **SAP integration:** SAP on Azure (M-series) lands in the SAP spoke. Needs ExpressRoute back to the on-prem ERP during cutover. Migration window is October.
- **Logging:** Central Log Analytics workspace in the hub. 90-day hot, 1-year archive. Sentinel on top for the PCI spoke.
- **Tagging:** Contoso has an internal tagging standard — `cm-env`, `cm-cost-center`, `cm-data-classification`, `cm-owner`. All resources must carry these four.

## What they explicitly do **not** want

- No third-party firewall in the hub. Azure Firewall only. (They had a bad experience with Palo Alto licensing.)
- No App Service in the PCI spoke. Container Apps or AKS only.
- No global admin accounts outside PIM.

## Open questions Contoso flagged for us

1. Cost ceiling on the hub for year 1 — they want a number before the November board.
2. Whether Defender for Cloud Standard is enough for the PCI assessor or if they need third-party scanning.
3. ExpressRoute circuit — Contoso has one already; can we reuse, or do we provision a new one for the cloud landing zone?

## What Frontier committed to in the call

- Reference architecture and Bicep skeleton in 1 week.
- ADO backlog with the work items broken out by spoke.
- Cost estimate for the hub and each spoke against the standard pattern.
- Decision record on the Defender vs. third-party scanning question by the next call.

---

*Next call: 2026-04-30, 14:00 CEST. Anya will bring the assessor's question list. Marko will share the on-prem network diagram before then.*
