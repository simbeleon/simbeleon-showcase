# Warranty Process System

Six years of warranty and contract management at HDW Belux (Benelux) — built from scratch, scaled to handle ±1,660 claims and ±€1.25M in processed value.

This is what operations work actually looks like when you take it seriously.

---

## Context

HDW Belux is a technical service and solutions company operating across the Benelux region. When I joined as Warranty & Contract Manager in 2019, there was no structured warranty process. Claims were tracked informally, acceptance rates were low, and there was no systematic approach to managing the full claim lifecycle.

I built the system from zero.

---

## What Was Built

### Claim Management Process
- End-to-end workflow from claim intake to resolution and reporting
- Structured intake templates to capture required information upfront
- Classification system by claim type, asset category, and contract tier
- Escalation paths for disputed or high-value claims

### Tracking & Reporting Infrastructure
- Central claim register with full lifecycle tracking (submitted → assessed → approved/rejected → settled)
- KPI dashboards: acceptance rate, average resolution time, outstanding value, aging analysis
- Monthly difference analysis and budget variance reporting
- Manufacturer communication logs tied to individual claim records

### Contract Management Layer
- ±150 active maintenance contracts managed across Ores, Sibelga, Equans, and Fluvius
- Contract terms mapped to claim eligibility rules
- Renewal tracking and expiry alerts
- SLA compliance monitoring per contract

---

## Scale

| Metric | Value |
|--------|-------|
| Claims managed | ±1,660 |
| Total claim value | ±€1,250,000 |
| Active maintenance contracts | ±150 |
| Key clients | Ores, Sibelga, Equans, Fluvius |
| Operating scope | Benelux |

---

## Results

The headline number: **acceptance rate from 63% to 88%**.

That improvement came from process, not luck. Details in [results.md](./results.md).

---

## Approach

No off-the-shelf warranty module fit the operation, so the system was built on Excel (advanced), Navision (ERP data), and structured process documentation. The tooling was secondary — the logic of the process was the work.

Later stages incorporated AI-assisted triage and structured output pipelines to reduce manual processing time on high-volume periods. See the [AI Agents](../ai-agents/) section for how that layer was designed.

---

> *Built from nothing. Still running. Numbers speak.*
