# Zava Complete Configuration Plan
## Dynamics 365 Finance and Supply Chain Management Implementation

**Company:** Zava Medical Equipment Manufacturing  
**Location:** Denver, Colorado, USA  
**Industry:** Medical Device Manufacturing  
**Start Date:** February 4, 2026  
**Target Go-Live:** March 31, 2026

---

## Executive Summary

This comprehensive configuration plan implements **Dynamics 365 Finance and Supply Chain Management** for Zava, a medical equipment manufacturer. The implementation follows Microsoft Success by Design methodology and covers:

- **Finance** — General Ledger, AR, AP, Cash Management, Budgeting
- **Supply Chain** — Inventory, Warehouse, Procurement, Sales
- **Human Resources** — Recruitment, Performance, Compensation, Benefits
- **Asset Management** — Fixed Assets, Maintenance, Leases
- **Project Management & Accounting** — Project Contracts, WBS, Time & Expense, Invoicing
- **Manufacturing** — Production Control, BOM, Quality Control, Lot Tracking (FDA-compliant)

---

## Business Process Coverage (Based on BPC Catalog)

### End-to-End Business Processes

| # | Process | Description | Priority |
|---|---------|-------------|----------|
| 1 | **Record to Report** | Financial accounting, budgets, period close, reporting | Critical |
| 2 | **Order to Cash** | Sales orders, AR, credit & collections | Critical |
| 3 | **Source to Pay** | Procurement, vendor management, AP | Critical |
| 4 | **Inventory to Deliver** | Warehouse, inventory levels, quality, shipping | Critical |
| 5 | **Plan to Produce** | Production planning, operations, quality control | Critical |
| 6 | **Hire to Retire** | HR lifecycle from recruitment to offboarding | High |
| 7 | **Acquire to Dispose** | Asset lifecycle, maintenance, disposal | High |
| 8 | **Project to Profit** | Project delivery, financials, billing | High |
| 9 | **Design to Retire** | Product lifecycle, introduction, retirement | Medium |
| 10 | **Forecast to Plan** | S&OP, demand planning, business performance | Medium |

---

## Implementation Phases

### Phase 1: Foundation (COMPLETED ✅)
**Duration:** Days 1-2  
**Status:** 100% Complete

#### 1.1 Legal Entity Setup
- [x] Create legal entity ZAVA
- [x] Configure address: 1550 Broadway, Denver, CO 80202
- [x] Set timezone: Mountain Time (US & Canada)
- [x] Set localized functionality: United States
- [x] Currency: USD

#### 1.2 General Ledger Configuration
- [x] Chart of Accounts (Shared Manufacturing structure)
- [x] Fiscal Calendar (14 periods, 2026)
- [x] Ledger setup (USD, Default exchange rate)
- [x] Number sequences

---

### Phase 2: Core Financials (COMPLETED ✅)
**Duration:** Days 2-3  
**Status:** 100% Complete

#### 2.1 Accounts Receivable
- [x] Customer posting profiles (GEN)
- [x] Payment terms (COD, NET15, NET30, NET60, D2N30)
- [x] Customer groups (Wholesale, Retail, Government, Institutional)
- [x] Sales tax (CDOR authority, COST 2.9%, DENV 4.81%, CO-DEN 7.71%)
- [x] Collections (STD sequence, 30/60/90 days)
- [x] Credit management

#### 2.2 Accounts Payable
- [x] Vendor posting profiles (GEN)
- [x] Vendor groups (Domestic, International, Service, Government)
- [x] Payment methods (VendPay journal, BOFA-USD bank)
- [x] Invoice matching policies

---

### Phase 3: Supply Chain Foundation (COMPLETED ✅)
**Duration:** Days 3-4  
**Status:** 100% Complete

#### 3.1 Warehouse Management
- [x] Site: DEN (Denver Distribution Center)
- [x] Warehouse: DENWH (Denver Main Warehouse)
- [x] Locations (Receiving, Storage, Shipping, QC)

#### 3.2 Product Information Management
- [x] Item model groups (Standard, FIFO)
- [x] Item groups
- [x] Storage dimension groups
- [x] Tracking dimension groups (Batch, Serial)
- [x] Released products with inventory posting

#### 3.3 Procure-to-Pay Cycle (Validated)
- [x] 4 Purchase Orders created, received, invoiced
- [x] Vendor payment journal posted ($13.58M)

---

### Phase 4: Human Resources
**Duration:** Days 5-8  
**Target Start:** February 10, 2026  
**Status:** NOT STARTED

#### 4.1 Develop People Strategy (55.05)
- [ ] Define HR organizational structure
- [ ] Establish personnel actions and categories
- [ ] Define employee types (Full-time, Part-time, Contractor)
- [ ] Configure worker statuses

#### 4.2 Recruit and Onboard Talent (55.10)
- [ ] Configure recruitment projects
- [ ] Define job templates and positions
- [ ] Set up applicant tracking
- [ ] Configure onboarding checklists
- [ ] Define employment contract terms

**Configuration Tasks:**
```
Menu: Human resources > Personnel management > Workers
Menu: Human resources > Recruitment > Recruitment projects
Menu: Human resources > Setup > Parameters
```

#### 4.3 Manage Workplace Compliance (55.30)
- [ ] Configure worker certificates and licenses
- [ ] Set up compliance tracking (OSHA, FDA requirements)
- [ ] Define training requirements
- [ ] Configure regulatory reporting

#### 4.4 Manage Performance and Growth (55.40)
- [ ] Configure performance goals and reviews
- [ ] Set up competency models
- [ ] Define career paths
- [ ] Configure learning management

#### 4.5 Manage Time and Attendance (55.50)
- [ ] Configure time registration
- [ ] Set up absence and leave types
- [ ] Define work calendars
- [ ] Configure flex time policies
- [ ] Set up overtime rules

**Configuration Tasks:**
```
Menu: Human resources > Time and attendance > Setup
Menu: Human resources > Leave and absence > Setup
```

#### 4.6 Manage Compensation and Benefits (55.70)
- [ ] Configure compensation plans
- [ ] Set up pay grades and bands
- [ ] Define benefit plans (Medical, Dental, Vision, 401k)
- [ ] Configure benefit eligibility rules
- [ ] Set up garnishments and deductions

**Configuration Tasks:**
```
Menu: Human resources > Compensation > Plans
Menu: Human resources > Benefits > Setup
```

#### 4.7 Offboard Talent (55.80)
- [ ] Configure termination reasons
- [ ] Set up offboarding checklists
- [ ] Define final pay calculations
- [ ] Configure COBRA administration

---

### Phase 5: Asset Management
**Duration:** Days 9-11  
**Target Start:** February 13, 2026  
**Status:** NOT STARTED

#### 5.1 Define Asset Strategy (10.05)
- [ ] Define asset classification hierarchy
- [ ] Establish capitalization thresholds
- [ ] Configure asset groups and types

#### 5.2 Acquire Assets (10.20)
- [ ] Configure acquisition methods
- [ ] Set up vendor invoices for assets
- [ ] Define asset books (Corporate, Tax, IFRS)
- [ ] Configure depreciation profiles
- [ ] Set up derived books

**Configuration Tasks:**
```
Menu: Fixed assets > Setup > Fixed asset groups
Menu: Fixed assets > Setup > Depreciation profiles
Menu: Fixed assets > Setup > Books
Menu: Fixed assets > Setup > Value models
```

**Depreciation Methods:**
| Book | Method | Life (Years) | Convention |
|------|--------|--------------|------------|
| Corporate | Straight Line | Varies | Mid-month |
| Tax | MACRS | Varies | Half-year |
| IFRS | Straight Line | Varies | Full-month |

#### 5.3 Manage Active Assets (10.40)
- [ ] Configure asset location tracking
- [ ] Set up asset lending/transfers
- [ ] Define asset insurance tracking
- [ ] Configure physical inventory counting

#### 5.4 Perform Asset Maintenance (10.50)
- [ ] Configure preventive maintenance schedules
- [ ] Set up work order types
- [ ] Define maintenance workers and resources
- [ ] Configure asset criticality levels
- [ ] Set up spare parts management

**Configuration Tasks:**
```
Menu: Asset management > Setup > Asset management parameters
Menu: Asset management > Setup > Work order types
Menu: Asset management > Setup > Maintenance plans
```

#### 5.5 Dispose of Assets (10.60)
- [ ] Configure disposal parameters
- [ ] Set up sale and scrap journals
- [ ] Define gain/loss accounts
- [ ] Configure retirement reasons

#### 5.6 Asset Leasing (IFRS 16/ASC 842)
- [ ] Configure lease parameters
- [ ] Set up lease books
- [ ] Define lease payment schedules
- [ ] Configure right-of-use asset posting

**Configuration Tasks:**
```
Menu: Asset leasing > Setup > Asset leasing parameters
Menu: Asset leasing > Setup > Lease books
```

---

### Phase 6: Project Management and Accounting
**Duration:** Days 12-15  
**Target Start:** February 17, 2026  
**Status:** NOT STARTED

#### 6.1 Develop Project Strategy (80.10)
- [ ] Define project types (Time & Material, Fixed Price, Internal)
- [ ] Configure project categories
- [ ] Establish billing rules
- [ ] Define project stages and gates

#### 6.2 Manage Project Contracts (80.20)
- [ ] Configure contract templates
- [ ] Set up billing schedules
- [ ] Define funding sources
- [ ] Configure revenue recognition rules

**Configuration Tasks:**
```
Menu: Project management and accounting > Setup > Project management and accounting parameters
Menu: Project management and accounting > Projects > Project contracts
```

#### 6.3 Plan Projects (80.30)
- [ ] Configure Work Breakdown Structure (WBS) templates
- [ ] Set up project calendars
- [ ] Define resource scheduling
- [ ] Configure project budgeting

#### 6.4 Manage Project Delivery (80.40)
- [ ] Configure hour journals
- [ ] Set up expense journals
- [ ] Define item requirements
- [ ] Configure project timesheets

**Configuration Tasks:**
```
Menu: Project management and accounting > Journals > Hour
Menu: Project management and accounting > Journals > Expense
Menu: Project management and accounting > Item tasks > Item requirements
```

#### 6.5 Manage Project Financials (80.50)
- [ ] Configure project posting profiles
- [ ] Set up WIP and accrual rules
- [ ] Define project invoicing
- [ ] Configure intercompany project accounting
- [ ] Set up project cost control

**Project Posting Accounts:**
| Transaction Type | Account |
|-----------------|---------|
| Cost | 500xxx (Project Costs) |
| Revenue | 400xxx (Project Revenue) |
| WIP - Cost | 140xxx (WIP Assets) |
| WIP - Sales | 230xxx (Deferred Revenue) |
| Accrued Revenue | 130xxx (Unbilled AR) |

---

### Phase 7: Manufacturing (Medical Equipment)
**Duration:** Days 16-25  
**Target Start:** February 24, 2026  
**Status:** NOT STARTED

> ⚠️ **CRITICAL**: Medical device manufacturing requires FDA 21 CFR Part 11 compliance for electronic records and signatures.

#### 7.1 Develop Production Strategy (70.10)
- [ ] Define manufacturing models (Discrete, Process, Lean)
- [ ] Configure production control parameters
- [ ] Establish quality standards (ISO 13485)
- [ ] Define traceability requirements (FDA UDI)

#### 7.2 Plan Production Operations (70.20)
- [ ] Configure Master Planning parameters
- [ ] Set up coverage groups
- [ ] Define planning fences
- [ ] Configure supply policies
- [ ] Set up demand forecasting

**Configuration Tasks:**
```
Menu: Master planning > Setup > Master planning parameters
Menu: Master planning > Setup > Plans > Master plans
Menu: Master planning > Setup > Coverage > Coverage groups
```

#### 7.3 Bill of Materials (BOM) Management
- [ ] Configure BOM versions
- [ ] Set up phantom BOMs
- [ ] Define co-products and by-products
- [ ] Configure BOM approval workflows

**Medical Equipment BOM Structure:**
```
Finished Medical Device (MED-001)
├── Subassembly A (SUBASM-A)
│   ├── Component 1 (Lot-tracked)
│   ├── Component 2 (Serial-tracked)
│   └── Raw Material (Batch-tracked)
├── Subassembly B (SUBASM-B)
│   └── Components...
└── Packaging Materials
```

#### 7.4 Route Management
- [ ] Configure route groups
- [ ] Set up operations and resources
- [ ] Define work centers and resource groups
- [ ] Configure operation scheduling

**Configuration Tasks:**
```
Menu: Production control > Setup > Routes > Route groups
Menu: Production control > Setup > Resources > Resources
Menu: Production control > Setup > Resources > Resource groups
```

#### 7.5 Run Production Operations (70.30)
- [ ] Configure production order types
- [ ] Set up production pools
- [ ] Define production stages
- [ ] Configure job card terminals
- [ ] Set up manufacturing execution

#### 7.6 Control Production Quality (70.60)
- [ ] Configure quality parameters
- [ ] Set up test instruments and variables
- [ ] Define quality associations
- [ ] Configure non-conformance management
- [ ] Set up quality orders (automatic generation)

**Quality Control Configuration:**
```
Menu: Inventory management > Setup > Quality management > Quality associations
Menu: Inventory management > Setup > Quality management > Test groups
Menu: Inventory management > Setup > Quality management > Quality orders
```

**Quality Association Triggers:**
| Event | Trigger | Test Group |
|-------|---------|------------|
| Receipt | Raw material receipt | RAW-QC |
| Production | Production output | PROD-QC |
| Sales | Before shipment | SHIP-QC |

#### 7.7 Lot/Batch Tracking (FDA Compliance)
- [ ] Configure batch attributes
- [ ] Set up lot/batch numbers (automatic)
- [ ] Define shelf life tracking
- [ ] Configure product recalls procedures
- [ ] Set up device history records (DHR)

**Tracking Dimensions:**
| Product Type | Batch | Serial | Best Before |
|--------------|-------|--------|-------------|
| Raw Materials | ✅ | ❌ | ✅ |
| Components | ✅ | ✅ | ❌ |
| Finished Goods | ✅ | ✅ | ✅ |

#### 7.8 Regulatory Compliance (21 CFR Part 11)
- [ ] Configure electronic signatures
- [ ] Set up audit trails
- [ ] Define record retention policies
- [ ] Configure user authentication
- [ ] Set up change control workflows

---

### Phase 8: Order to Cash (Sales Operations)
**Duration:** Days 26-28  
**Target Start:** March 5, 2026  
**Status:** NOT STARTED

#### 8.1 Develop Sales Policies (65.05)
- [ ] Configure sales agreements
- [ ] Set up pricing (trade, discount, rebate)
- [ ] Define delivery terms
- [ ] Configure allocation rules

#### 8.2 Manage Sales Orders (65.20)
- [ ] Configure order entry parameters
- [ ] Set up order types
- [ ] Define reservation policies
- [ ] Configure ATP (Available-to-Promise)
- [ ] Set up sales quotations

**Configuration Tasks:**
```
Menu: Sales and marketing > Setup > Sales and marketing parameters
Menu: Sales and marketing > Sales orders > All sales orders
Menu: Sales and marketing > Sales quotations > All quotations
```

#### 8.3 Manage Credit and Collections (65.50)
- [ ] Configure credit limits by customer
- [ ] Set up credit hold policies
- [ ] Define collection letter sequences
- [ ] Configure aging periods
- [ ] Set up write-off procedures

---

### Phase 9: Forecasting and Planning
**Duration:** Days 29-30  
**Target Start:** March 10, 2026  
**Status:** NOT STARTED

#### 9.1 Conduct Sales and Operations Planning (50.25)
- [ ] Configure demand forecasting
- [ ] Set up statistical baseline forecasts
- [ ] Define forecast models
- [ ] Configure consensus planning

#### 9.2 Execute Sales and Operations (50.35)
- [ ] Configure action messages
- [ ] Set up planned order firming
- [ ] Define supply chain visibility
- [ ] Configure exception management

---

### Phase 10: Integration and Reporting
**Duration:** Days 31-35  
**Target Start:** March 12, 2026  
**Status:** NOT STARTED

#### 10.1 Financial Reporting
- [ ] Configure Financial Reporter
- [ ] Set up row/column definitions
- [ ] Define report trees
- [ ] Configure management reports

#### 10.2 Operational Reporting
- [ ] Configure Power BI integration
- [ ] Set up operational dashboards
- [ ] Define KPI metrics
- [ ] Configure alerts and notifications

#### 10.3 System Integrations
- [ ] Configure Dataverse integration
- [ ] Set up API connections
- [ ] Define data entities for export
- [ ] Configure batch jobs

---

### Phase 11: Testing and Validation
**Duration:** Days 36-42  
**Target Start:** March 17, 2026  
**Status:** NOT STARTED

#### 11.1 Unit Testing
- [ ] Test GL postings
- [ ] Test AR/AP transactions
- [ ] Test inventory movements
- [ ] Test production orders
- [ ] Test project transactions

#### 11.2 Integration Testing
- [ ] Test end-to-end Order to Cash
- [ ] Test end-to-end Source to Pay
- [ ] Test end-to-end Plan to Produce
- [ ] Test end-to-end Project to Profit

#### 11.3 User Acceptance Testing (UAT)
- [ ] Configure UAT environment
- [ ] Execute UAT scripts
- [ ] Document defects
- [ ] Obtain sign-offs

#### 11.4 Performance Testing
- [ ] Test with production volumes
- [ ] Validate response times
- [ ] Test batch job performance

---

### Phase 12: Go-Live Preparation
**Duration:** Days 43-45  
**Target Start:** March 26, 2026  
**Status:** NOT STARTED

#### 12.1 Cutover Planning
- [ ] Define cutover schedule
- [ ] Prepare data migration
- [ ] Configure production environment
- [ ] Validate security roles

#### 12.2 Training
- [ ] Train end users
- [ ] Train power users
- [ ] Train administrators
- [ ] Document procedures

#### 12.3 Go-Live
- [ ] Execute final data migration
- [ ] Validate all configurations
- [ ] Obtain go-live approval
- [ ] Monitor hypercare period

---

## Configuration Summary by Module

### Module Configuration Matrix

| Module | Menu Path | Key Configurations |
|--------|-----------|-------------------|
| **General Ledger** | General ledger > Setup | Chart of accounts, Journals, Ledger, Calendar |
| **Accounts Receivable** | Accounts receivable > Setup | Posting profiles, Payment terms, Customer groups |
| **Accounts Payable** | Accounts payable > Setup | Posting profiles, Payment methods, Vendor groups |
| **Inventory** | Inventory management > Setup | Item groups, Dimensions, Posting |
| **Warehouse** | Warehouse management > Setup | Sites, Warehouses, Locations |
| **Production** | Production control > Setup | Routes, BOMs, Resources, Parameters |
| **Master Planning** | Master planning > Setup | Plans, Coverage, Fences |
| **Quality** | Inventory management > Setup > Quality | Tests, Associations, Orders |
| **Human Resources** | Human resources > Setup | Workers, Positions, Benefits |
| **Fixed Assets** | Fixed assets > Setup | Groups, Books, Depreciation |
| **Asset Management** | Asset management > Setup | Types, Maintenance, Work orders |
| **Projects** | Project management > Setup | Categories, Contracts, Posting |

---

## Number Sequences Required

| Area | Reference | Format | Scope |
|------|-----------|--------|-------|
| General Ledger | Voucher | ZAVA-###### | Company |
| Sales | Sales order | SO-###### | Company |
| Sales | Quotation | QT-###### | Company |
| Purchasing | Purchase order | PO-###### | Company |
| Inventory | Transfer | TR-###### | Company |
| Production | Production order | PRD-###### | Company |
| Projects | Project ID | PRJ-###### | Company |
| HR | Personnel number | EMP-###### | Company |
| Fixed Assets | Asset number | FA-###### | Company |
| Quality | Quality order | QO-###### | Company |

---

## Security Roles Required

| Role | Description | Modules |
|------|-------------|---------|
| Financial Controller | Full finance access | GL, AR, AP, FA |
| AR Clerk | Accounts receivable processing | AR |
| AP Clerk | Accounts payable processing | AP |
| Inventory Manager | Inventory and warehouse | INV, WMS |
| Production Planner | Production scheduling | MRP, PROD |
| Production Supervisor | Shop floor operations | PROD, MES |
| Quality Manager | Quality control | QC |
| HR Administrator | Human resources | HR |
| Project Manager | Project delivery | PROJ |
| Asset Manager | Fixed assets and maintenance | FA, AM |

---

## Timeline Summary

```
February 2026
├── Week 1 (Feb 4-7)   ✅ Foundation, Core Finance, Supply Chain
├── Week 2 (Feb 10-14)    Human Resources
└── Week 3 (Feb 17-21)    Asset Management, Projects

March 2026
├── Week 1 (Feb 24-28)    Manufacturing Setup
├── Week 2 (Mar 3-7)      Manufacturing & Order to Cash
├── Week 3 (Mar 10-14)    Forecasting, Integration, Reporting
├── Week 4 (Mar 17-21)    Testing & UAT
├── Week 5 (Mar 24-28)    Go-Live Prep
└── Mar 31                🚀 GO-LIVE
```

---

## Risk Register

| ID | Risk | Probability | Impact | Mitigation |
|---|------|-------------|--------|-----------|
| R01 | FDA compliance gaps | Medium | Critical | Engage regulatory consultant early |
| R02 | Manufacturing complexity | Medium | High | Phase implementation, parallel testing |
| R03 | Data migration issues | Medium | High | Multiple mock cutover rehearsals |
| R04 | User adoption | Medium | Medium | Comprehensive training program |
| R05 | Integration failures | Low | High | Early integration testing |
| R06 | Performance issues | Low | High | Load testing with production volumes |

---

## Success Criteria

| Metric | Target | Measurement |
|--------|--------|-------------|
| Go-live on schedule | March 31, 2026 | Project milestone |
| All critical processes functional | 100% | UAT sign-off |
| User training complete | 100% of users | Training records |
| Data migration accuracy | 99.9% | Reconciliation |
| System availability | 99.5% | Monitoring |
| FDA audit readiness | Pass | Mock audit |

---

## Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | February 7, 2026 | AI Configuration Agent | Initial comprehensive plan |

---

## Appendix A: BPC Process Reference

Source: Business Process Catalog Tree (Why) - Full DEC 2025.1.xlsx

### Applicable End-to-End Processes

1. **Record to Report (90.xx)** — Financial accounting and reporting
2. **Order to Cash (65.xx)** — Sales and collections
3. **Source to Pay (75.xx)** — Procurement and AP
4. **Inventory to Deliver (60.xx)** — Warehouse and logistics
5. **Plan to Produce (70.xx)** — Manufacturing
6. **Hire to Retire (55.xx)** — Human resources
7. **Acquire to Dispose (10.xx)** — Asset management
8. **Project to Profit (80.xx)** — Project accounting
9. **Design to Retire (40.xx)** — Product lifecycle
10. **Forecast to Plan (50.xx)** — S&OP planning

---

## Appendix B: Success by Design Alignment

Source: Success by Design Delivery Plan DEC 2025.xlsx

| SbD Phase | Project Phase | Status |
|-----------|---------------|--------|
| Strategize | Pre-project planning | ✅ Complete |
| Initiate | Phase 1-3 (Foundation) | ✅ Complete |
| Implement - Design | Phase 4-10 | 🔄 In Progress |
| Implement - Develop | Phase 7 (Manufacturing) | ⏳ Upcoming |
| Implement - Test | Phase 11 | ⏳ Upcoming |
| Prepare | Phase 12 | ⏳ Upcoming |
| Operate | Post go-live | ⏳ Upcoming |

---

*This plan is generated based on Microsoft Dynamics 365 Business Process Catalog (BPC) December 2025.1 and Success by Design methodology.*
