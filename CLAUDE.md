# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Purpose

Week 2 Gateway assessment for FDE (Future Development Engineer) program. This repository contains program materials and deliverables for cognitive work assessment using ATX (Agentic Transformation) methodology.

The scenario: **Apex Distribution Ltd** — Birmingham-based regional carrier with 800 employees. Main focus is the 35-person Customer Operations function handling four work streams: delivery exceptions, ETA inquiries, dispatch adjustments, and billing disputes. The task is to design the agentic transformation of Customer Operations, assessing delegation suitability and producing an agent design that addresses real business constraints.

## Repository Structure

```
FDE/
├── Week2/
│   ├── Gate2-Participant-Pack.md        # Full gate specification and requirements
│   ├── README-Participants-Week2.md     # Week 2 overview and methodology
│   ├── references/
│   │   ├── atx-concepts.md              # Core ATX concepts (3 production factors, compounding thesis)
│   │   ├── atx-assessment.md            # ATX assessment methodology
│   │   ├── atx-agent-mapping.md         # Mapping cognitive work to agents
│   │   ├── atx-scoring.md               # Volume × value analysis, delegation scoring
│   │   └── atx-economics.md             # Economics of digital labour
│   ├── discovery-questioning-patterns.md # Discovery question techniques
│   ├── enriched_scenarios.md            # Additional scenario context
│   └── Gate2-Artefacts/                 # 7 CSV sample files + README
│       ├── APEX_BILL_DAILY_20260414.csv
│       ├── APEX_FUEL_SURCH_20260414.csv
│       ├── APEX_CREDITS_20260414.csv
│       ├── APEX_RECON_20260413.csv
│       ├── APEX_DISPUTES_OPEN_20260414.csv
│       ├── APEX_AGED_RECEIVABLES_20260410.csv
│       └── APEX_CUSTOMER_MASTER_20260401.csv
├── Intro+Week1/
│   ├── claude-md-examples-guide.md      # CLAUDE.md writing best practices
│   ├── production-spec-checklist.md     # Buildability audit checklist
│   └── spec-ambiguity-vs-builder-mistakes.md
└── Reference/
    └── production-spec-checklist.md

Specification/
└── (deliverables go here)
```

## Deliverables Format and Location

All Week 2 Gateway deliverables must be created in the `Specification/` directory as Markdown files.

### Required Deliverables (7 total)

1. **Cognitive Load Map** (`03_Cognitive_Load_Map.md`) 
   - Decompose at least 2 of 4 work streams (Delivery Exceptions, ETA Inquiries, Dispatch Adjustments, Billing Disputes)
   - Jobs to be Done → micro-tasks → cognitive dimensions
   - Map cognitive zones and breakpoints
   - Must reflect *lived* work (from artefacts), not just documented SOPs

2. **Delegation Suitability Matrix** (`04_Delegation_Suitability_Matrix.md`) 
   - Score each major task cluster on delegation dimensions
   - Assign archetypes: fully agentic / agent-led with oversight / human-led with agent support / human-only
   - **CRITICAL**: Justify every archetype assignment — "everything is fully agentic" is the most marked-down anti-pattern
   - Arbitrary assignments will be challenged

3. **Volume × Value Analysis** (`05_Volume_Value_Analysis.md`) 
   - Plot 4 work streams on volume × value axes
   - Identify primary agentic target
   - Justify why it wins over alternatives

4. **Agent Purpose Document** (`06_Agent_Purpose_Document.md`) 
   - For highest-value opportunity: purpose, scope, KPIs, autonomy matrix, escalation triggers, failure modes
   - Must be precise enough that an AI coding agent could begin building from it
   - Follow buildability checklist from `FDE/Intro+Week1/production-spec-checklist.md`

5. **System/Data Inventory** (`07_System_Data_Inventory.md`) 
   - What the agent needs to access, what's available, what's missing, what's risky
   - **CRITICAL**: Address Aurum Billing constraints (batch-file exports only, no real-time API, 24h lag, 48h ticket turnaround)
   - State assumptions explicitly where systems not fully detailed in brief

6. **Discovery Questions for Main Stakeholder** (`08_Discovery_Questions.md`) 
   - Questions whose answers would *actually* change your design
   - **NOT** generic "tell me about your process" questions
   - For domain-naïve participants, this is the most direct signal of FDE judgment

7. **Project CLAUDE.md** (`../CLAUDE.md`)
   - CLAUDE.md as if you were handing off to implementation team
   - Demonstrates workflow discipline
   - Should include: build/run instructions, API integration details, Aurum constraint handling, delegation boundaries, escalation patterns, testing strategy

### Additional Deliverables Created (Not Required by Gate 2)

- **Domain Orientation** (`01_Domain_Orientation.md`) — Comprehensive domain analysis
- **Problem Statement and Success Metrics** (`02_Problem_Statement_and_Success_Metrics.md`) — Problem quantification
- **Stakeholder Presentation Strategy** (`09_Stakeholder_Presentation_Strategy.md`) — Sarah Whitmore presentation approach
- **Stakeholder Presentation** (`Stakeholder_Presentation.html`) — 14-slide HTML presentation (convertible to PDF)
- **Stakeholder Presentation PDF** (`Stakeholder_Presentation.pdf`) — PDF version of presentation (299 KB)
- **Demo Application Design** (`10_Demo_Application_Design.md`) — Complete architecture and design for browser-based Python demo
- **Demo Application Summary** (`11_Demo_Application_Summary.md`) — Build status, testing results, and deployment guide
- **Working Demo Application** (`../demo_app/`) — Fully functional Flask-based demo showcasing agent capabilities

### Naming Convention
Individual deliverable files as above, or single consolidated document: `Gate2-<FirstName>-<LastName>.md` with clear headings for each deliverable.

## Scenario Constraints and Domain Context

### Apex Distribution Ltd Key Facts
- **Scale**: 800 employees, 180 vehicles, ~3,500 deliveries/day (B2B and DTC)
- **Customer Operations**: 35 people handling 4 work streams
- **Work volumes**:
  - Delivery exceptions: ~180/day, avg 12 min/case
  - ETA inquiries: ~400/day, avg 4 min/case
  - Dispatch adjustments: ~90/day, avg 18 min/case
  - Billing disputes: ~60/day, avg 28 min/case

### System Landscape
1. **Modern CRM** (Salesforce-based) — REST APIs available
2. **Driver App** (in-house iOS/Android) — GPS, routes, scan-on-delivery, driver-dispatch messaging
3. **Dispatch Console** (Java desktop via Citrix) — limited API surface
4. **Aurum Billing** (legacy, on-prem Oracle since 2008):
   - Batch-file exports only: daily 02:00–04:00 GMT to CSV
   - **No real-time API**
   - Reconciliation file lags 24 hours behind invoice generation
   - Invoice modifications require manual ticket to Aurum support (48h turnaround)
   - Schema changes ~quarterly without prior notice

### Key Stakeholder: Sarah Whitmore (COO)
- Promoted internally 18 months ago
- Sceptical of chatbots and consultants (two prior automation failures)
- Open to "something that actually works"
- Under pressure from CEO to match competitor's £1.2M savings

## Critical Anti-Patterns to Avoid

1. **"Everything is fully agentic"** — the most marked-down failure mode
2. **Documented-not-lived work** — reflect artefacts, not just SOPs
3. **Bluffing domain knowledge** — use assumptions log for unknowns
4. **Legacy system hand-wave** — address Aurum constraints explicitly, don't ignore them
5. **Generic discovery questions** — must be specific enough to change design
6. **Vanishing dispatcher** — don't ignore dispatcher discretion/judgment in workflow
7. **Filler assumptions** — only state assumptions that are testable and material

## ATX Methodology Key Concepts

### Lived vs. Documented Work
Every enterprise has two versions:
- **Documented**: SOPs, swimlanes, compliance manuals
- **Lived**: how work actually happens when systems are slow, data is missing, customers behave unexpectedly

**Agents built from documentation will be built for an imaginary organisation.** Use the 5 artefacts in `Gate2-Artefacts/` to ground your lived-work analysis.

### Delegation Archetypes
- **Fully agentic**: Agent decides and acts autonomously
- **Agent-led with oversight**: Agent proposes, human approves
- **Human-led with agent support**: Human decides, agent provides context/data
- **Human-only**: Cannot/should not be delegated

Score each task cluster on:
- Determinism (rule-bound vs. judgment-bound)
- Risk/reversibility (what happens if the agent is wrong?)
- Data availability (structured, complete, real-time?)
- Stakeholder trust (will they accept agent decisions?)
- Compliance/audit requirements

### Jobs to be Done (JtD) as Cognitive Contracts
A JtD is not a task — it's a cognitive contract between actor and outcome.
- What must be **decided** vs. what must be **executed**
- Which parts are **knowledge-bound**, **rule-bound**, **exception-bound**
- Which systems and data sources participate

### Cognitive Zones and Breakpoints
Within a single JtD, cognitive effort is not uniform. Map:
- High-cognitive zones (judgment, interpretation, exception handling)
- Low-cognitive zones (lookup, rule application, routine execution)
- Breakpoints: where cognitive zone shifts (e.g., from lookup to judgment)

## When Working on Deliverables

### Before Writing
1. Read `Gate2-Participant-Pack.md` end-to-end
2. Review all 5 artefacts (voicemail, email thread, SMS, SOP fragment, batch export catalogue)
3. Examine CSV files in `Gate2-Artefacts/` for data shape and constraints
4. Read ATX reference documents in `FDE/Week2/references/`

### While Writing
- **Cognitive Load Map**: Ground every micro-task in specific artefacts (e.g., "Mark's voicemail shows dispatcher discretion drives refusal decisions")
- **Delegation Matrix**: Justify archetype assignments with reference to determinism, risk, data constraints
- **Volume × Value**: Consider both total volume and handling time (e.g., ETA inquiries are high volume but low complexity)
- **Agent Purpose**: Follow production-spec-checklist.md — every requirement testable, every entity defined, no vague modals
- **System Inventory**: Explicitly address Aurum batch-export constraints — no hand-waving
- **Discovery Questions**: Frame questions whose answers would materially change design decisions

### Assumptions Log
When domain knowledge is shallow or system details incomplete, state assumptions explicitly:
- **Format**: "ASSUMPTION: [statement]. Confidence: [high/medium/low]. Test via: [method]."
- **Example**: "ASSUMPTION: Dispatch console can send driver instructions but cannot receive real-time status. Confidence: medium. Test via: ask Sarah if dispatch receives driver GPS updates in real-time or via polling."

## Build Loop for Agent Purpose Document

Once Agent Purpose Document is drafted, test buildability:
1. Hand document to Claude Code with prompt: *"Begin building the agent described in this document. First, tell me what you can build confidently without asking questions. Second, tell me what you need to clarify before building the rest. Third, build the parts you are confident about."*
2. Review three outputs:
   - **What it built**: faithful to document or drift?
   - **What questions it asked**: each is a gap
   - **What it couldn't build**: buildability gap, usually at delegation boundary
3. Diagnose gaps against taxonomy from `spec-ambiguity-vs-builder-mistakes.md`
4. Revise Agent Purpose Document (usually autonomy matrix or escalation triggers)
5. Re-run and verify

## What Claude Code Should NOT Do

- Never invent work volumes, handling times, or system capabilities not in the brief or artefacts
- Never default to "fully agentic" without justification
- Never ignore Aurum Billing batch-export constraints
- Never write generic discovery questions ("Tell me about your process")
- Never claim domain expertise where assumptions are being made — use assumptions log
- Never create deliverables outside the `Specification/` directory

## Escalation and Clarification

If requirements are genuinely unclear:
1. Check artefacts first (voicemail, email thread, SMS, SOP, CSVs)
2. Check ATX reference docs
3. If still unclear, document as assumption with confidence level
4. If materially changes design scope, add to Discovery Questions deliverable

Discovery Questions are the appropriate place to surface unknowns — they demonstrate FDE judgment under uncertainty.

## Time Management

Gate 2 is a 3-hour timed exercise. Suggested allocation:
- 0–25 min: AI-accelerated domain orientation
- 25–55 min: Read scenario brief + artefacts twice
- 55–110 min: Cognitive Load Map + Delegation Suitability Matrix
- 110–140 min: Volume × Value + Agent Purpose Document
- 140–165 min: System Inventory + Discovery Questions
- 165–180 min: Project CLAUDE.md + final pass

Near-pass is a fail. Prioritize precision over completeness. Known gaps with explicit scope-out plans are better than silent omissions.

## Demo Application

A fully functional browser-based Python demo application has been built to showcase the ETA Inquiry Agent concept.

### Location and Structure

```
demo_app/
├── app.py                      # Flask application with REST API
├── requirements.txt            # Python dependencies (Flask, geopy, etc.)
├── README.md                   # Complete setup and usage guide
├── DEMO_GUIDE.md              # 5-minute walkthrough script
├── start.bat / start.sh       # Quick launch scripts
├── agent/
│   ├── order_validator.py     # Order ID extraction & validation
│   ├── eta_calculator.py      # ETA calculation (standard & precision)
│   └── escalation_engine.py   # Escalation trigger detection
├── data/
│   ├── mock_orders.json       # 8 sample orders for testing
│   └── mock_routes.json       # 4 routes with GPS data
└── templates/
    ├── index.html             # Customer inquiry interface
    ├── admin.html             # Admin panel (decision log)
    └── comparison.html        # Comparison view (baseline vs agent metrics)
```

### How to Run

```bash
cd demo_app
python app.py
```

Then open browser to:
- **Customer View**: http://localhost:5000/
- **Admin Panel**: http://localhost:5000/admin
- **Comparison View**: http://localhost:5000/comparison

### Key Features Demonstrated

1. **Delegation Archetypes**
   - Fully Agentic (green badge) - Standard ETA lookup, <1 sec response
   - Agent-Led (yellow badge) - Precision ETA with confidence scoring
   - Human-Only (red badge) - Escalated due to triggers (GPS stale, exceptions)

2. **Escalation Triggers**
   - GPS data stale (>30 min threshold)
   - Order not found in system
   - Delivery exception status
   - High-value package (>£500) in EXCEPTION state
   - Customer callback request

3. **Decision Transparency**
   - Real-time admin panel showing every agent decision
   - Response time tracking (milliseconds)
   - Escalation reasons visible
   - Confidence levels exposed

4. **Performance Metrics**
   - Comparison view: 96% faster response (8.5 min → 30 sec)
   - Deflection rate: 90% target (360/400 cases autonomous)
   - Business case: £301K annual savings
   - Live statistics dashboard

### Test Scenarios

| Order ID | Scenario | Expected Behavior |
|----------|----------|-------------------|
| `AX-771-3344` | Standard lookup | Fully Agentic (<1 sec, green badge) |
| `AX-771-3344` → "More specific?" | Precision ETA | GPS-based calculation, confidence shown |
| `AX-441-8821` → "More specific?" | GPS stale | Escalates (52 min > 30 min threshold) |
| `AX-996-7890` | High-value exception | Immediate escalation (£1,250, EXCEPTION) |
| `XX-999-9999` | Order not found | Validation error, escalation option |

### Demo Purpose

- **Not production-ready** - Uses mock data, no real system integrations
- **Proof-of-concept** - Validates agent capabilities before expensive integration
- **Stakeholder demo** - Shows Sarah Whitmore (COO) how agent handles inquiries
- **Low-risk validation** - Runs standalone, no disruption to live systems
- **Business case proof** - Demonstrates 96% faster response, 90% deflection, £301K savings

### Documentation

- **Design**: `Specification/10_Demo_Application_Design.md` - Complete architecture and algorithms
- **Summary**: `Specification/11_Demo_Application_Summary.md` - Build status and testing results
- **Quick Guide**: `demo_app/DEMO_GUIDE.md` - 5-minute walkthrough script
- **Full Docs**: `demo_app/README.md` - Setup, usage, and troubleshooting
