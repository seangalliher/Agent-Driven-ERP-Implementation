# Dynamics 365 Project Operations Core Configuration Plan

## Engineering Firm — Denver, Colorado

| **Item** | **Detail** |
|---|---|
| **Company Type** | Engineering Firm |
| **Headquarters** | Denver, Colorado, USA |
| **Operating Regions** | United States, Canada, Mexico |
| **Deployment Model** | Resource/Non-stocked (Recommended for professional services) |
| **BPC Reference** | Business Process Catalog DEC 2025.1 |

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Organizational & Legal Entity Structure](#2-organizational--legal-entity-structure)
3. [Project Operations Core Configuration](#3-project-operations-core-configuration)
4. [Project to Profit (BPC 80.xx) Process Configuration](#4-project-to-profit-bpc-80xx-process-configuration)
5. [Order to Cash — Project Billing (BPC 65.xx)](#5-order-to-cash--project-billing-bpc-65xx)
6. [Source to Pay — Project Procurement (BPC 75.xx)](#6-source-to-pay--project-procurement-bpc-75xx)
7. [Record to Report — Project Financials (BPC 90.xx)](#7-record-to-report--project-financials-bpc-90xx)
8. [Multi-Country / Multi-Currency Configuration](#8-multi-country--multi-currency-configuration)
9. [Integration Strategy](#9-integration-strategy)
10. [Data Migration Plan](#10-data-migration-plan)
11. [Testing Strategy](#11-testing-strategy)
12. [Cutover & Go-Live Plan](#12-cutover--go-live-plan)
13. [Success by Design Delivery Alignment](#13-success-by-design-delivery-alignment)
14. [Appendix: Configuration Checklist](#appendix-configuration-checklist)

---

## 1. Executive Summary

This configuration plan outlines the end-to-end setup of **Dynamics 365 Project Operations (Resource/Non-stocked deployment)** for an engineering firm headquartered in Denver, Colorado, serving clients across the **United States, Canada, and Mexico**.

The plan is aligned to the **Microsoft Business Process Catalog (BPC) DEC 2025.1** and the **Success by Design** methodology to ensure best practices are followed throughout implementation. The primary end-to-end business process is **Project to Profit (BPC 80.xx)**, with supporting processes from **Order to Cash (65.xx)**, **Source to Pay (75.xx)**, and **Record to Report (90.xx)**.

### Key Objectives

- Enable project-based operations across three countries with proper legal, tax, and currency configurations
- Establish a unified project lifecycle from opportunity through invoicing and revenue recognition
- Support time & expense tracking, resource scheduling, and subcontractor management
- Provide multi-currency billing (USD, CAD, MXN) with consolidated financial reporting
- Implement approval workflows for timesheets, expenses, and invoices

---

## 2. Organizational & Legal Entity Structure

### 2.1 Legal Entities

| **Legal Entity** | **Country** | **Base Currency** | **Purpose** |
|---|---|---|---|
| US Engineering Co. | United States | USD | Primary HQ, domestic projects |
| CA Engineering Co. | Canada | CAD | Canadian client projects |
| MX Engineering Co. | Mexico | MXN | Mexican client projects |

> **BPC Reference:** *90.10.010 — Develop company structure*
> Define the financial structure and organizational policies for each legal entity.

### 2.2 Operating Units & Business Units

| **Unit** | **Type** | **Description** |
|---|---|---|
| Civil Engineering | Business Unit | Roads, bridges, infrastructure |
| Structural Engineering | Business Unit | Building structures, foundations |
| Environmental Engineering | Business Unit | Environmental assessments, remediation |
| MEP Engineering | Business Unit | Mechanical, electrical, plumbing |
| Project Management Office (PMO) | Department | Project governance & oversight |

### 2.3 Financial Dimensions

| **Dimension** | **Values (Examples)** | **Purpose** |
|---|---|---|
| Business Unit | Civil, Structural, Environmental, MEP | Revenue/cost by discipline |
| Department | Engineering, PMO, Corporate | Overhead allocation |
| Project | Dynamic (created per project) | Project-level P&L |
| Cost Center | Denver HQ, Field, Remote | Location-based cost tracking |
| Customer Region | US-West, US-East, Canada, Mexico | Regional reporting |

---

## 3. Project Operations Core Configuration

### 3.1 Project Management & Accounting Parameters

> **BPC Deliverable:** *Project management and accounting parameters* (Configuration — Parameters)

| **Parameter** | **Setting** | **Notes** |
|---|---|---|
| Default project type | Time and Material | Primary billing model for engineering |
| Funding source validation | Enabled | Validate funding on all transactions |
| Require project ID on transactions | Yes | All costs tracked to projects |
| Enable intercompany | Yes | Cross-legal entity resource sharing |
| Timesheet period frequency | Weekly | Standard for engineering firms |
| Expense approval workflow | Enabled | Manager approval required |
| Invoice approval workflow | Enabled | PM + Finance approval |
| Revenue recognition method | Percentage of completion | For fixed-price contracts |
| Default line property | Chargeable | Default for billable work |
| Budget control | Enabled | Per-project budget tracking |

### 3.2 Project Groups

> **BPC Deliverable:** *Project groups* (Configuration — List of Values)

| **Project Group** | **Project Type** | **Posting Behavior** | **Use Case** |
|---|---|---|---|
| TM-Engineering | Time & Material | Revenue accrual | Standard billable engineering work |
| FP-Engineering | Fixed Price | WIP + Revenue recognition | Fixed-price design contracts |
| Internal | Internal | Cost only | Internal R&D, training, overhead |
| Investment | Investment | Capitalize to asset | Capital project expenditures |

### 3.3 Project Categories

> **BPC Deliverables:** *Project categories*, *Category groups*, *Shared categories* (Configuration — List of Values)

| **Category Group** | **Categories** | **Transaction Type** |
|---|---|---|
| Engineering Labor | Senior Engineer, Project Engineer, Junior Engineer, CAD Technician, Field Inspector | Hour |
| Management | Project Manager, Program Manager, Principal-in-Charge | Hour |
| Consulting | Subject Matter Expert, Peer Reviewer | Hour |
| Travel | Airfare, Hotel, Meals, Mileage, Per Diem | Expense |
| Supplies | Printing, Survey Equipment Rental, Lab Testing | Expense |
| Subcontractor | Geotechnical, Surveying, Environmental Testing | Expense / Item |
| Fees | Permit Fees, Filing Fees, Application Fees | Fee |
| Milestones | Design Milestone, Review Milestone, Completion Milestone | On-account |

### 3.4 Line Properties

> **BPC Deliverable:** *Line properties*, *Project/group line properties* (Configuration — List of Values)

| **Line Property** | **Chargeable** | **Use Case** |
|---|---|---|
| Chargeable | Yes | Billable client work (default) |
| Non-chargeable | No | Internal meetings, rework, admin |
| Complimentary | No | Goodwill / warranty scope |
| Not applicable | No | Internal project hours |

### 3.5 Cost Templates & Estimates

> **BPC Deliverable:** *Cost template* (Configuration — List of Values)

| **Cost Template** | **Method** | **Applied To** |
|---|---|---|
| Percent Complete - Cost | Cost at completion | Fixed-price engineering projects |
| Percent Complete - Hours | Hours at completion | Effort-based fixed-price projects |
| Completed Contract | On completion | Small fixed-price deliverables |

### 3.6 Forecast Models

> **BPC Deliverable:** *Forecast models*, *Project allocation keys* (Configuration — List of Values)

| **Forecast Model** | **Purpose** |
|---|---|
| Budget - Original | Baseline approved budget |
| Budget - Revised | Approved budget revisions |
| Forecast - EAC | Estimate at completion (updated monthly) |
| Remaining Forecast | Hours/costs remaining to complete |

---

## 4. Project to Profit (BPC 80.xx) Process Configuration

### 4.1 Develop Project Strategy (BPC 80.10)

> *BPC 80.10.010 — Develop program charter*
> *BPC 80.10.200 — Develop project management strategy*
> *BPC 80.10.300 — Develop project governance strategy*
> *BPC 80.10.400 — Develop project approval processes*

**Configuration Actions:**

- [ ] Define project numbering sequences per legal entity (e.g., US-2026-0001, CA-2026-0001, MX-2026-0001)
- [ ] Configure project stages: Prospect → Quotation → Active → Completed → Closed
- [ ] Set up project governance roles: Principal-in-Charge, Project Manager, Task Lead
- [ ] Configure approval processes for project creation and budget changes
- [ ] Define project templates for recurring engineering project types:
  - Civil Infrastructure Design
  - Structural Analysis & Design
  - Environmental Impact Assessment
  - MEP Systems Design
  - Construction Administration

### 4.2 Manage Project Contracts (BPC 80.20)

> *BPC 80.20.010 — Estimate project contracts*
> *BPC 80.20.040 — Negotiate project contracts*
> *BPC 80.20.050 — Finalize project contracts*
> *BPC 80.20.060 — Maintain project contracts*
> *BPC 80.20.100 — Process project change requests*

**Configuration Actions:**

- [ ] Configure contract types:
  - **Time & Material** — Hourly billing with not-to-exceed (primary model)
  - **Fixed Price** — Milestone-based billing for defined deliverables
  - **Cost Plus** — Cost reimbursable with markup
  - **Retainer** — Pre-paid monthly retainers
- [ ] Set up billing rules per contract line:
  - Time & material with rate caps
  - Fixed-price milestones with completion percentage
  - Expense markup percentages (e.g., 10% on subcontractor costs)
- [ ] Configure funding limits and funding source rules
- [ ] Enable contract line tracking for multi-discipline projects
- [ ] Configure change order/amendment workflows

### 4.3 Plan Projects (BPC 80.30)

> *BPC 80.30.020 — Define project scope*
> *BPC 80.30.030 — Plan project resources*
> *BPC 80.30.040 — Plan project tasks*
> *BPC 80.30.050 — Assign project resources*
> *BPC 80.30.060 — Forecast project resources*
> *BPC 80.30.070 — Manage project budget*

**Configuration Actions:**

- [ ] Configure Work Breakdown Structure (WBS) templates:

| **Template** | **Typical Phases** |
|---|---|
| Civil Design | Survey → Preliminary Design → Final Design → Bid Documents → Construction Admin |
| Structural Design | Analysis → Schematic Design → Design Development → Construction Documents |
| Environmental Assessment | Site Investigation → Data Analysis → Report Preparation → Remediation Plan |
| MEP Design | Schematic → Design Development → Construction Documents → Shop Drawing Review |

- [ ] Set up resource scheduling parameters (hours per day: 8, days per week: 5)
- [ ] Configure resource roles and competencies:
  - Civil Engineer (PE), Structural Engineer (SE), Environmental Scientist, MEP Engineer
  - CAD Designer, GIS Specialist, Field Inspector, Survey Crew
- [ ] Configure project budget workflow (two-level: PM → Finance Director)
- [ ] Set up budget warning thresholds: 75%, 90%, 100%
- [ ] Enable project forecast capabilities for Estimate at Completion (EAC)

### 4.4 Manage Project Delivery (BPC 80.40)

> *BPC 80.40.005 — Govern projects*
> *BPC 80.40.008 — Control project scope*
> *BPC 80.40.020 — Track project expenses*
> *BPC 80.40.050 — Track project time*
> *BPC 80.40.055 — Track project fees*
> *BPC 80.40.110 — Purchase project materials*
> *BPC 80.40.140 — Subcontract project components*

**Configuration Actions:**

#### Time Entry

- [ ] Configure timesheet layout with project/task/category fields
- [ ] Set up timesheet validation rules:
  - Maximum 12 hours per day
  - Minimum 1-hour increments (0.25-hour for engineering precision preferred)
  - Required: project, task, category, line property
- [ ] Configure timesheet favorites for recurring project assignments
- [ ] Enable timesheet delegation for administrative assistants
- [ ] **Timesheet Approval Workflow**: Direct Manager → PM (for cross-department charges)

> **BPC Deliverable:** *Timesheet policy* (Configuration — List of Values)

#### Expense Entry

- [ ] Configure expense categories aligned to project categories (Travel, Supplies, Fees)
- [ ] Set up per diem policies per country:

| **Country** | **Daily Meal Rate** | **Hotel Max** | **Mileage Rate** |
|---|---|---|---|
| United States | $79/day (GSA rates) | Per GSA locality | $0.67/mile |
| Canada | CAD $105/day | Per NJC rates | CAD $0.72/km |
| Mexico | MXN $1,200/day | MXN $3,000/night | MXN $3.50/km |

- [ ] Configure expense approval workflow: Employee → Manager → Finance
- [ ] Set up receipt attachment requirements (mandatory over $25 USD equivalent)
- [ ] Enable credit card import integration

#### Subcontractor Management

> *BPC 80.40.140 — Subcontract project components*

- [ ] Configure subcontractor categories: Geotechnical, Surveying, Lab Testing, Specialty Consulting
- [ ] Set up subcontract purchase order templates
- [ ] Configure subcontractor markup rules (standard: 10% markup on cost)
- [ ] Enable subcontractor invoice matching to purchase orders

### 4.5 Manage Project Financials (BPC 80.50)

> *BPC 80.50.030 — Correct project transactions*
> *BPC 80.50.050 — Invoice project milestones*
> *BPC 80.50.055 — Invoice project transactions*
> *BPC 80.50.060 — Recognize project revenue*

**Configuration Actions:**

#### Project Invoicing

- [ ] Configure invoice formats per billing type:
  - T&M invoices: Detailed time/expense backup with summary
  - Fixed-price invoices: Milestone description with completion certification
  - Cost-plus invoices: Detailed cost breakdown with markup calculation
- [ ] Set up invoice frequency defaults: Monthly billing cycle (last business day)
- [ ] Configure invoice proposal workflows: PM Review → Finance Review → Approval
- [ ] Enable invoice line detail grouping by task, category, or worker
- [ ] Set up electronic invoicing for each country as required

#### Revenue Recognition

- [ ] Configure revenue recognition methods per project type:

| **Project Type** | **Recognition Method** | **Trigger** |
|---|---|---|
| Time & Material | As invoiced | Invoice posting |
| Fixed Price | Percentage of completion (cost-based) | Monthly estimate process |
| Internal | N/A (cost only) | N/A |

- [ ] Set up revenue recognition estimate periods (monthly)
- [ ] Configure WIP and accrued revenue posting rules
- [ ] Set up project statement reports for PM review

### 4.6 Analyze Project Performance (BPC 80.60)

> *BPC 80.60.020 — Monitor project status*
> *BPC 80.60.030 — Analyze project metrics*
> *BPC 80.60.100 — Monitor project risks*
> *BPC 80.60.200 — Manage project quality*
> *BPC 80.60.300 — Measure project progress*

**Configuration Actions:**

- [ ] Configure project dashboard KPIs:
  - Budget vs. Actuals (cost and hours)
  - Earned Value metrics (CPI, SPI)
  - Utilization rate by engineer/discipline
  - Unbilled WIP aging
  - Revenue backlog
- [ ] Set up project status reporting (weekly PM reports for active projects)
- [ ] Configure project analytics workspace in Power BI
- [ ] Enable project profitability analysis by discipline, client, and region

---

## 5. Order to Cash — Project Billing (BPC 65.xx)

> *BPC 65.30.010 — Issue sales invoices (Project)*
> *BPC 65.30.030 — Issue customer credits (Project)*
> *BPC 65.30.055 — Recognize revenue*
> *BPC 65.30.100 — Process customer payments*

### Configuration Actions

- [ ] Configure customer groups for engineering clients:
  - Government (Federal, State/Provincial, Municipal)
  - Private Sector (Commercial, Industrial)
  - Institutional (Education, Healthcare)
- [ ] Set up payment terms per client type:

| **Client Type** | **Payment Terms** | **Notes** |
|---|---|---|
| Government — US | Net 45 | Retainage common (5-10%) |
| Government — CA | Net 30 | Provincial variations |
| Government — MX | Net 60 | VAT considerations |
| Private — US | Net 30 | Standard |
| Private — CA | Net 30 | Standard |
| Private — MX | Net 45 | Standard |

- [ ] Configure retainage tracking for construction/government contracts
- [ ] Set up accounts receivable aging reports (30/60/90/120 days)
- [ ] Configure customer credit and collections workflows
- [ ] Set up project credit note processing for billing corrections

---

## 6. Source to Pay — Project Procurement (BPC 75.xx)

> *BPC 75.30 — Manage supplier relationships*
> *BPC 75.35.070 — Contract suppliers for services*
> *BPC 75.40 — Procure goods and services*
> *BPC 75.50 — Manage accounts payable*

### Configuration Actions

- [ ] Configure procurement categories for project-related purchases:
  - Professional subcontractor services
  - Survey equipment & supplies
  - Lab testing & analysis
  - Printing & reproduction
  - Travel services
- [ ] Set up vendor groups:
  - Subcontractors (Engineering, Geotechnical, Environmental, Survey)
  - Suppliers (Office supplies, Equipment rental, Lab testing)
  - Consultants (Legal, Specialty engineering)
- [ ] Configure purchase requisition workflows for project purchases
- [ ] Set up purchase order approval limits:

| **Role** | **Approval Limit** |
|---|---|
| Task Lead | $5,000 |
| Project Manager | $25,000 |
| Department Director | $100,000 |
| VP/Principal | $250,000 |
| CFO | Unlimited |

- [ ] Configure vendor invoice matching (2-way: PO to Invoice)
- [ ] Set up payment terms for subcontractors (Net 30 standard)
- [ ] Enable cross-legal entity procurement for intercompany resource sharing

---

## 7. Record to Report — Project Financials (BPC 90.xx)

> *BPC 90.10 — Define accounting policies*
> *BPC 90.30 — Manage budgets*
> *BPC 90.50 — Record financial transactions*

### 7.1 Chart of Accounts — Project-Specific

| **Account Range** | **Category** | **Description** |
|---|---|---|
| 4100-4199 | Revenue | Engineering service revenue by type |
| 4200-4299 | Revenue | Subcontractor pass-through revenue |
| 4300-4399 | Revenue | Reimbursable expense revenue |
| 5100-5199 | COGS | Direct labor costs |
| 5200-5299 | COGS | Subcontractor costs |
| 5300-5399 | COGS | Direct project expenses |
| 1500-1599 | WIP | Work in progress — project costs |
| 2600-2699 | Deferred Revenue | Unearned project revenue |

### 7.2 Ledger Posting Setup

> **BPC Deliverable:** *Ledger posting setup* (Configuration — List of Values)

| **Posting Type** | **Debit Account** | **Credit Account** |
|---|---|---|
| Hour - Cost | 5100 Direct Labor | 2100 Accrued Payroll |
| Hour - Revenue | 1200 AR / 1500 WIP | 4100 Service Revenue |
| Expense - Cost | 5300 Direct Expense | 2000 AP / Bank |
| Expense - Revenue | 1200 AR | 4300 Reimbursable Revenue |
| Fee - Revenue | 1200 AR | 4100 Service Revenue |
| On-account (Milestone) | 1200 AR | 2600 Deferred Revenue |
| WIP - Invoiced on-account | 2600 Deferred Revenue | 4100 Service Revenue |
| Accrued Revenue | 1550 Accrued Revenue | 4100 Service Revenue |

### 7.3 Indirect Cost Configuration

> **BPC Deliverable:** *Indirect cost components*, *Indirect cost component groups* (Configuration — List of Values)

| **Indirect Cost Component** | **Rate Basis** | **Rate** | **Applied To** |
|---|---|---|---|
| Fringe Benefits | % of Direct Labor | 35% | All labor hours |
| General & Administrative | % of Direct Labor | 15% | All projects |
| Facilities Overhead | % of Direct Labor | 12% | Denver HQ projects |
| Field Overhead | % of Direct Labor | 8% | Field-based projects |

### 7.4 Multi-Currency & Consolidation

- [ ] Configure reporting currency: USD (consolidated)
- [ ] Set up exchange rate types and providers
- [ ] Configure financial reporting for consolidated P&L across legal entities
- [ ] Enable intercompany elimination entries

---

## 8. Multi-Country / Multi-Currency Configuration

### 8.1 Currency Configuration

| **Currency** | **Legal Entity** | **Exchange Rate Type** | **Source** |
|---|---|---|---|
| USD | US Engineering Co. | Default | Base currency |
| CAD | CA Engineering Co. | Daily Average | Bank of Canada |
| MXN | MX Engineering Co. | Daily Average | Banco de México |

### 8.2 Tax Configuration

| **Country** | **Tax Type** | **Standard Rate** | **Configuration** |
|---|---|---|---|
| **United States** | Sales Tax | Varies by state/locality | Tax groups per state; Denver: CO state + RTD + Denver city |
| | | | Professional services exemptions as applicable |
| **Canada** | GST/HST | 5% GST (federal) | Federal GST + Provincial PST/HST |
| | PST | Varies by province | Provincial sales tax where applicable |
| **Mexico** | IVA (VAT) | 16% | Standard VAT; CFDI electronic invoicing required |
| | ISR | Varies | Income tax withholding on payments |

**Configuration Actions:**

- [ ] Set up tax groups and item tax groups per country
- [ ] Configure tax registration numbers per legal entity
- [ ] Set up withholding tax for Mexico (ISR) and Canada (non-resident withholding if applicable)
- [ ] Configure CFDI electronic invoicing for Mexico
- [ ] Set up 1099 reporting for US subcontractors
- [ ] Configure Canadian T4A reporting for subcontractors

### 8.3 Intercompany Configuration

- [ ] Enable intercompany project transactions
- [ ] Configure transfer pricing for cross-entity resource sharing:
  - Borrowing entity bills client at contracted rate
  - Lending entity charges at cost + markup (standard: cost + 10%)
- [ ] Set up intercompany invoicing and settlement workflows
- [ ] Configure intercompany posting rules and elimination entries

---

## 9. Integration Strategy

> **SbD Delivery Plan:** *Integration Strategy — Define integration points, Technical integration strategy*

| **System** | **Integration Type** | **Direction** | **Technology** | **Frequency** |
|---|---|---|---|---|
| Microsoft Project / Project for the Web | Schedule sync | Bidirectional | Native | Real-time |
| SharePoint / Teams | Document management | Bidirectional | Native | Real-time |
| Power BI | Reporting & analytics | Outbound | Dataverse | Daily refresh |
| Payroll System | Labor cost import | Inbound | Data entities / API | Bi-weekly |
| CRM (Dynamics 365 Sales) | Opportunity to project | Inbound | Dual-write | Real-time |
| Banking / Treasury | Payment processing | Bidirectional | Electronic banking | Daily |
| ADP / Payroll | Employee data sync | Inbound | API / SFTP | Daily |
| Procore / Bluebeam | Construction admin | Bidirectional | API | As needed |

---

## 10. Data Migration Plan

> **SbD Delivery Plan:** *Data management — Configuration data and data migration*

### Migration Sequence

| **Seq** | **Data Entity** | **Source** | **Est. Records** | **Priority** |
|---|---|---|---|---|
| 1 | Chart of Accounts | Legacy ERP | 500 | Critical |
| 2 | Financial Dimensions | Legacy ERP | 200 | Critical |
| 3 | Customers | Legacy CRM/ERP | 2,000 | Critical |
| 4 | Vendors / Subcontractors | Legacy ERP | 1,500 | Critical |
| 5 | Employees / Resources | HRIS | 500 | Critical |
| 6 | Project Categories | Manual | 100 | Critical |
| 7 | Price Lists (rate tables) | Legacy / Spreadsheets | 300 | Critical |
| 8 | Active Projects | Legacy ERP | 200 | High |
| 9 | Active Contracts | Legacy / Documents | 150 | High |
| 10 | Open AR (balances forward) | Legacy ERP | 500 | High |
| 11 | Open AP (balances forward) | Legacy ERP | 300 | High |
| 12 | GL Opening Balances | Legacy ERP | 1 journal | Critical |
| 13 | WIP Balances | Legacy ERP | 200 | High |
| 14 | Historical Projects (reference) | Legacy ERP | 5,000 | Medium |

### Migration Approach

- [ ] Perform 3 test data loads minimum before cutover (per SbD best practice)
- [ ] Use Data Management Framework (DMF) for bulk imports
- [ ] Validate all data with business stakeholders between each load
- [ ] Establish data quality rules and cleansing procedures
- [ ] Document data mapping from legacy system to D365

---

## 11. Testing Strategy

> **SbD Delivery Plan:** *Testing strategy — Plan testing strategy, Implement testing approach*

| **Test Phase** | **Scope** | **Timeline** | **Exit Criteria** |
|---|---|---|---|
| Unit Testing | Individual configurations, forms, workflows | Weeks 8-10 | All configurations validated |
| Process Testing | End-to-end business process scenarios | Weeks 11-13 | All BPC 80.xx processes pass |
| Integration Testing | System-to-system data flows | Weeks 14-15 | All integration points functional |
| Data Migration Testing | 3 full migration cycles | Weeks 12, 14, 16 | <2% error rate, timing validated |
| User Acceptance Testing (UAT) | Business user validation | Weeks 17-19 | Sign-off from all stakeholders |
| Performance Testing | Load/volume testing | Week 16 | Response times within SLA |
| Security Testing | Role-based access validation | Week 15 | All security roles verified |

### Key Test Scenarios (Project to Profit)

1. Create T&M project → Enter time → Approve → Invoice → Receive payment
2. Create Fixed-price project → Set milestones → Track progress → Invoice milestones → Recognize revenue
3. Intercompany resource sharing: US resource billing to Canada project
4. Subcontractor PO → Receive invoice → Apply markup → Bill to client
5. Expense entry with multi-currency → Approve → Reimburse → Bill to client
6. Project budget exceeded → Alert → Budget revision → Approval workflow
7. Project credit note → Reversal → Re-invoice
8. Month-end: WIP calculation → Revenue recognition → Financial reporting

---

## 12. Cutover & Go-Live Plan

> **SbD Delivery Plan:** *Cutover to production, Cutover strategy workshop*

### Cutover Checklist

| **Step** | **Task** | **Duration** | **Owner** |
|---|---|---|---|
| 1 | Freeze legacy system for final data extract | Day 0 | IT |
| 2 | Extract and validate final data from legacy | Day 0-1 | Data team |
| 3 | Import master data (customers, vendors, employees) | Day 1 | Data team |
| 4 | Import opening balances (GL, AR, AP) | Day 1-2 | Finance |
| 5 | Import active projects and WIP balances | Day 2 | PMO / Finance |
| 6 | Validate imported data | Day 2-3 | Business leads |
| 7 | Configure security roles and user access | Day 3 | IT |
| 8 | Execute smoke tests (critical paths) | Day 3 | Test team |
| 9 | Go/No-Go decision checkpoint | Day 3 | Steering committee |
| 10 | Go-Live: Enable user access | Day 4 | IT |
| 11 | Hypercare support (2 weeks) | Days 4-18 | Full team |

### Go-Live Readiness Criteria

> **BPC Reference:** *99.01.400 — Prepare to go live*

- [ ] All SIT and UAT test cases passed with sign-off
- [ ] Data migration validated and reconciled
- [ ] All integration points tested with production credentials
- [ ] User training completed for all roles
- [ ] Support model and escalation path documented
- [ ] Cutover plan rehearsed via mock cutover (minimum 1 full rehearsal)
- [ ] Rollback plan documented and tested

---

## 13. Success by Design Delivery Alignment

> Aligned to **Success by Design Delivery Plan DEC 2025**

### Phase 1: Strategize

| **Task** | **Deliverable** | **Status** |
|---|---|---|
| Create transformation roadmap | Roadmap document | ☐ |
| Define change management strategy | Change management plan | ☐ |
| Define organizational change and communication strategy | Communication plan | ☐ |
| Manage project goals and readiness | Readiness assessment | ☐ |

### Phase 2: Initiate / Discover (Process-Focused Solutions)

| **Task** | **Deliverable** | **Status** |
|---|---|---|
| 80.01 Project to profit scenario board discovery workshop | Workshop output | ☐ |
| 80.01.001 Create project to profit user stories | User stories backlog | ☐ |
| 80.01.002 Configure project to profit solution | Configured system | ☐ |
| 80.01.003 Design project to profit high-level solution architecture | Architecture doc | ☐ |
| 90.01 Record to report scenario board discovery workshop | Workshop output | ☐ |
| 90.01.002 Configure record to report solution | Configured system | ☐ |
| 65.01 Order to cash scenario board discovery workshop | Workshop output | ☐ |
| 75.01 Source to pay scenario board discovery workshop | Workshop output | ☐ |

### Phase 3: Implement / Design Review

| **Task** | **Deliverable** | **Status** |
|---|---|---|
| 80.02 Project to profit storyline design review workshop | Design review | ☐ |
| 80.02.001 Document project to profit gaps and RAID | RAID log | ☐ |
| 80.02.002 Refine project to profit user stories | Updated backlog | ☐ |
| 80.02.003 Plan project to profit detailed design workshops | Workshop plan | ☐ |
| 80.02.004 Project to profit design document | Design document | ☐ |
| 90.02.004 Record to report design document | Design document | ☐ |

### Phase 4: Prepare

| **Task** | **Deliverable** | **Status** |
|---|---|---|
| Testing strategy execution | Test results, sign-off | ☐ |
| Data migration execution (3 loads) | Migration reports | ☐ |
| User training | Training completion records | ☐ |
| Mock cutover | Cutover timing validated | ☐ |

### Phase 5: Operate

| **Task** | **Deliverable** | **Status** |
|---|---|---|
| Go-live readiness assessment | Readiness checklist | ☐ |
| Cutover execution | Production go-live | ☐ |
| Hypercare support | Support log, issue resolution | ☐ |

---

## Appendix: Configuration Checklist

### A. Organizational Setup

- [ ] Create legal entities (US, CA, MX)
- [ ] Configure operating units and business units
- [ ] Set up financial dimensions
- [ ] Configure number sequences per legal entity
- [ ] Set up currencies and exchange rate providers
- [ ] Configure fiscal calendars (US: Jan-Dec, can vary per entity)

### B. Project Operations Parameters

- [ ] Project management and accounting parameters
- [ ] Project groups (T&M, Fixed Price, Internal, Investment)
- [ ] Project categories and category groups
- [ ] Shared categories across legal entities
- [ ] Line properties (Chargeable, Non-chargeable, Complimentary)
- [ ] Cost templates and estimate methods
- [ ] Forecast models and allocation keys
- [ ] Default offset accounts for expenses
- [ ] Ledger posting setup for all project transaction types

### C. Pricing & Rate Tables

- [ ] Standard billing rates by role/category
- [ ] Cost rates by employee/resource
- [ ] Expense rate tables (per diem, mileage) per country
- [ ] Subcontractor markup rules
- [ ] Intercompany transfer pricing

### D. Workflows & Approvals

- [ ] Timesheet approval workflow
- [ ] Timesheet line approval workflow
- [ ] Expense report approval workflow
- [ ] Project invoice proposal review workflow
- [ ] Project quotation review workflow
- [ ] Project budget review (original and revision)
- [ ] Resource request workflow
- [ ] Purchase requisition workflow
- [ ] Vendor invoice workflow

### E. Tax & Compliance

- [ ] US sales tax configuration (state/local)
- [ ] Canada GST/HST/PST configuration
- [ ] Mexico IVA/ISR configuration
- [ ] CFDI electronic invoicing (Mexico)
- [ ] 1099 reporting setup (US subcontractors)
- [ ] Withholding tax configuration
- [ ] Intercompany transfer pricing documentation

### F. Security Roles

| **Role** | **Access Level** | **Key Capabilities** |
|---|---|---|
| Project Manager | Project-level | Create/manage projects, approve time, create invoices |
| Project Accountant | Cross-project | Revenue recognition, financial adjustments, reporting |
| Engineer / Resource | Task-level | Time entry, expense entry, task updates |
| Subcontractor | Limited | Time/expense entry on assigned projects only |
| Finance Manager | Entity-level | GL posting, period close, financial reporting |
| PMO Director | All projects | Cross-project reporting, resource management |
| System Administrator | Full | Configuration, security, system maintenance |

### G. Reporting & Analytics

- [ ] Configure project management workspace
- [ ] Set up project cost control views
- [ ] Configure utilization reports by resource/discipline
- [ ] Set up project profitability analysis
- [ ] Configure unbilled WIP aging reports
- [ ] Build Power BI dashboards for executive reporting
- [ ] Set up financial consolidation reports across entities

---

*Document generated from BPC Reference DEC 2025.1 — Business Process Catalog Tree, Deliverables Tree, and Success by Design Delivery Plan.*

*Last updated: February 8, 2026*
