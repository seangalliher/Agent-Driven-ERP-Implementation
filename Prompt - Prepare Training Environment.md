# Prompt: Prepare D365 Project Operations Training Environment

> **Usage:** Copy this entire prompt into a Copilot chat session that has access to a Dataverse MCP server and Playwright MCP browser automation connected to your D365 Project Operations environment. Update the variables in the Configuration section before running.

## Configuration — Update These Values

ENVIRONMENT_URL: https://YOUR-ORG.crm.dynamics.com
APP_ID: (your Project Operations app module ID — find at Settings → Solutions or by navigating to the base CRM URL)
DEPLOYMENT_MODEL: Resource/Non-stocked
TRAINING_SCENARIO_NAME: (e.g., "Pinnacle Environmental - Water Treatment Facility Assessment")
CUSTOMER_ACCOUNT_NAME: (e.g., "Pinnacle Environmental Solutions")

LEGAL_ENTITIES:
  - Name: (e.g., Zava US)   | Currency: USD
  - Name: (e.g., Zava CA)   | Currency: CAD  (optional)
  - Name: (e.g., Zava MX)   | Currency: MXN  (optional)

ROLES_NEEDED:
  - Lead Engineer
  - Senior Engineer
  - Project Manager
  - Environmental Specialist
  - Compliance Officer

TEAM_MEMBERS:
  - Name: (Resource 1) | Role: Lead Engineer     | Billing: Chargeable
  - Name: (Resource 2) | Role: Environmental Specialist | Billing: Chargeable
  - Name: (Resource 3) | Role: Senior Engineer   | Billing: Chargeable
  - Name: (Resource 4) | Role: Compliance Officer | Billing: Chargeable

WBS_STRUCTURE:
  Phase 1 - Site Assessment:
    - Environmental Survey         | 5d | 40h | → Resource 1
    - Water Quality Testing        | 5d | 40h | → Resource 3
    - Existing Infrastructure Review | 3d | 24h | → Resource 2
  Phase 2 - Design & Engineering:
    - Treatment System Design      | 10d | 80h | → Resource 1
    - Regulatory Compliance Review | 5d  | 40h | → Resource 4
    - Cost-Benefit Analysis        | 5d  | 40h | → Resource 2
  Phase 3 - Implementation Planning:
    - Project Schedule Development | 3d | 24h | → Project Manager
    - Resource Allocation Plan     | 3d | 24h | → Project Manager
    - Training & Handover          | 5d | 40h | → Resource 4

TIME_ENTRIES:
  # Use PAST dates (before today) so invoicing works
  - Resource 1 | (today - 7 days) | Environmental Survey    | 8h
  - Resource 3 | (today - 6 days) | Water Quality Testing   | 8h
  - Resource 2 | (today - 5 days) | Infrastructure Review   | 8h

EXPENSES:
  - Meals   | $75.00  | (today - 7 days) | Team lunch during site assessment
  - Airfare | $450.00 | (today - 7 days) | Round trip to client site
  - Hotel   | $185.00 | (today - 6 days) | Overnight accommodation

SCREENSHOT_PREFIX: training_  (screenshots saved with this prefix + step number)
OUTPUT_LAB_MANUAL: "Training Lab Manual - D365 Project Operations End-to-End.md"
```

---

## Prompt

You are an expert Dynamics 365 Project Operations consultant. Prepare the environment at `{ENVIRONMENT_URL}` for a complete training session covering the full project lifecycle. Execute every step below end-to-end, taking screenshots at each milestone for a lab manual.

### Phase 0 — Environment Discovery & Validation

Before creating any data, query the Dataverse environment to inventory existing reference data. Use `mcp_dataverse_mcp_read_query` for each:

1. **Organizational Units** — `SELECT msdyn_organizationalunitid, msdyn_name FROM msdyn_organizationalunit`
2. **Bookable Resource Categories (Roles)** — `SELECT bookableresourcecategoryid, name FROM bookableresourcecategory`
3. **Price Lists** — `SELECT pricelevelid, name, msdyn_module FROM pricelevel`
4. **Bookable Resources** — `SELECT bookableresourceid, name, resourcetype FROM bookableresource`
5. **Customer Accounts** — `SELECT accountid, name FROM account`
6. **Transaction Categories** — `SELECT msdyn_transactioncategoryid, msdyn_name FROM msdyn_transactioncategory`
7. **Expense Categories** — `SELECT msdyn_expensecategoryid, msdyn_name, msdyn_expensetype FROM msdyn_expensecategory`
8. **Currencies** — `SELECT transactioncurrencyid, currencyname, isocurrencycode FROM transactioncurrency`
9. **System Users** — `SELECT systemuserid, fullname FROM systemuser WHERE isdisabled = 0`
10. **Project Parameters** — `SELECT msdyn_projectparameterid, msdyn_defaultorganizationalunit FROM msdyn_projectparameter`

**Report any gaps** (missing org units, roles, price lists, resources, categories). If critical reference data is missing, create it via Dataverse MCP before proceeding.

**Validation rules:**
- At least 1 Org Unit with currency must exist
- At least 1 Cost and 1 Sales price list must exist with role price lines
- At least 4 Bookable Resources linked to system users must exist
- Expense categories (Meals, Airfare, Hotel) must exist

### Phase 1 — Create Opportunity

1. Use `mcp_dataverse_mcp_create_record` to create an Opportunity:
   - `name`: `{TRAINING_SCENARIO_NAME}`
   - `customerid`: lookup to `{CUSTOMER_ACCOUNT_NAME}` account (format: `{"recordId": "GUID", "relatedTable": "account"}`)
   - `transactioncurrencyid`: lookup to USD currency
   - `estimatedvalue`: 250000

2. Navigate the browser to the Opportunities list and take **Screenshot 01** showing the opportunity.

3. Open the opportunity and take **Screenshot 02** of the form.

### Phase 2 — Create Quote & Win → Contract

1. Open the Opportunity in the browser.
2. Click **+ New Quote** to create a Quote from the Opportunity.
3. Set the **Price List** (Sales price list) and **Contracting Org Unit**.
4. Save the Quote. Take **Screenshot 03**.
5. Add a **Quote Line**:
   - Name: `{scenario name} - T&M`
   - Billing Method: Time and Material
   - Include Time: Yes
   - Include Expense: Yes
6. Save. Take **Screenshot 04** showing the quote with the line.
7. Click **Activate** to move the Quote to Active status.
8. Click **Close as Won** → confirm the dialog.
9. The system auto-creates a **Project Contract**. Navigate to it. Take **Screenshot 05**.

### Phase 3 — Create Project

1. Switch to the **Projects** area.
2. Create a new project via `mcp_dataverse_mcp_create_record` on `msdyn_project`:
   - `msdyn_subject`: Project name from config
   - `msdyn_customer`: customer account lookup
   - `msdyn_contractorganizationalunitid`: org unit lookup
   - `msdyn_projectmanager`: system user lookup
   - `msdyn_schedulemode`: 192350001 (Fixed Duration)
   - `msdyn_scheduledstart`: start date

3. Navigate to the project in the browser. Take **Screenshot 06**.

### Phase 4 — Build WBS

1. Navigate to the **Tasks** tab on the project.
2. Add all tasks flat using the **+ Add new task** button in the WBS grid.
3. Take **Screenshot 07** of flat task list.
4. For each child task, use **More options (Alt+M) → Make subtask** to create the hierarchy.
5. Take **Screenshot 08** of the hierarchical WBS.
6. Set Duration and Effort on each leaf task by clicking the cell twice to enter edit mode, typing the value, and pressing Enter.
7. Take **Screenshot 09** of the complete WBS with values.

> **Critical notes for WBS editing:**
> - The WBS grid loads inside an iframe named `iframe_pexwebcontrol`.
> - Direct Dataverse updates to `msdyn_projecttask` duration/effort are **blocked by the PSS plugin**. You must use the UI grid.
> - Use Enter (submit) to commit values, not Tab (which navigates out of the iframe).
> - Summary tasks auto-calculate from children.

### Phase 5 — Add Team Members

1. Use `mcp_dataverse_mcp_create_record` on `msdyn_projectteam` for each team member:
   - `msdyn_project`: project lookup
   - `msdyn_bookableresourceid`: resource lookup
   - `msdyn_resourcecategory`: role lookup
   - `msdyn_name`: resource name

2. Navigate to the **Team** tab. Take **Screenshot 10**.

### Phase 6 — Assign Resources to Tasks

1. Navigate to the **Tasks** tab.
2. For each leaf task in the WBS grid:
   - Click the **Assigned to** cell.
   - Click the **"Assign this task"** icon button.
   - In the resource picker popup, click the desired resource.
   - Wait for the toast confirmation.
3. Take **Screenshot 11** of the fully assigned WBS.

### Phase 7 — Create & Submit Time Entries

1. Use `mcp_dataverse_mcp_create_record` on `msdyn_timeentry` for each entry:
   - `msdyn_date`: **past date** (critical for invoicing)
   - `msdyn_duration`: minutes (480 = 8 hours)
   - `msdyn_start`: same as date
   - `msdyn_project`: project lookup
   - `msdyn_projecttask`: task lookup
   - `msdyn_bookableresource`: resource lookup
   - `msdyn_type`: 192350000 (Work)

2. Submit each entry via `mcp_dataverse_mcp_update_record`:
   - Set `msdyn_entrystatus` to `192350003` (Submitted)

3. Navigate to Time Entries view. Take **Screenshot 12**.

### Phase 8 — Create & Submit Expenses

1. Use `mcp_dataverse_mcp_create_record` on `msdyn_expense` for each expense:
   - `msdyn_amount`, `msdyn_price`, `msdyn_quantity`: expense details
   - `msdyn_expensecategory`: category lookup
   - `msdyn_project`: project lookup
   - `msdyn_transactiondate`: **past date**
   - `msdyn_unit`, `msdyn_unitgroup`: unit lookups
   - `transactioncurrencyid`: currency lookup

2. Submit via `msdyn_expensestatus` → `192350001` (Submitted)

3. Take **Screenshot 13** of the Expenses list.

### Phase 9 — Approve Time & Expenses

**Important — Approval requires a two-step process:**

1. **First, approve the underlying entries:**
   - Time: Update `msdyn_timeentry.msdyn_entrystatus` → `192350002` (Approved)
   - Expense: Update `msdyn_expense.msdyn_expensestatus` → `192350002` (Approved)

2. **Then, approve the Project Approval records:**
   - Query: `SELECT msdyn_projectapprovalid FROM msdyn_projectapproval WHERE msdyn_project = '{project_guid}'`
   - Update each: `msdyn_recordstage` → `2` (Approved)

3. Verify actuals were created:
   ```sql
   SELECT msdyn_transactiontypecode, msdyn_amount, msdyn_documentdate
   FROM msdyn_actual
   WHERE msdyn_project = '{project_guid}'
   ```

4. Navigate to the Approvals view. Take **Screenshot 14**.

### Phase 10 — Confirm Contract

1. Navigate to the Project Contract in the browser.
2. **Verify** the contract line has the `msdyn_project` field linked to the project.
   - If null, update via: `mcp_dataverse_mcp_update_record` on `salesorderdetails/{contract_line_guid}` → set `msdyn_project`
3. Click **More commands (⋮) → Confirm**.
4. Click **OK** on the confirmation dialog.
5. Take **Screenshot 15** of the confirmed contract.

### Phase 11 — Mark Ready to Invoice

1. Navigate to **Sales → Billing → Time and Material Billing Backlog**.
2. Select all rows (Toggle selection of all rows checkbox).
3. Click **More commands (⋮) → Ready to invoice**.
4. Verify billing status updated:
   ```sql
   SELECT msdyn_billingstatus FROM msdyn_actual
   WHERE msdyn_transactiontypecode = 192350005
   AND msdyn_project = '{project_guid}'
   ```
   Should show `192350004` (Ready to Invoice).
5. Take **Screenshot 16**.

### Phase 12 — Create Proforma Invoice

1. Navigate to the Project Contract.
2. Click **More commands (⋮) → Create Invoice**.
3. The system creates an invoice and navigates to it.
4. If it shows $0.00 Total, click **More commands → Recalculate** or **Refresh Invoice Line Transactions**.
5. Take **Screenshot 17** of the proforma invoice.
6. Verify invoice line transactions:
   ```sql
   SELECT msdyn_amount, msdyn_quantity, msdyn_documentdate
   FROM msdyn_invoicelinetransaction
   WHERE msdyn_invoice = '{invoice_guid}'
   ```

### Phase 13 — Generate Lab Manual

Create a comprehensive markdown lab manual with:
- 12 labs covering each lifecycle step
- Step-by-step instructions with field values and navigation paths
- Tables showing exact data to enter
- Screenshots referenced at each step
- Key concepts explaining the "why" behind each step
- Entity reference appendix
- Status code reference appendix
- Troubleshooting appendix covering common errors
- Screenshots index

Save as `{OUTPUT_LAB_MANUAL}` in the workspace.

---

## Dataverse MCP Syntax Reference

### Lookup Field Format
All LOOKUP and CUSTOMER fields use this format:
```json
{"recordId": "GUID-here", "relatedTable": "logicalname"}
```
Example: `{"recordId": "ae1aaf54-...", "relatedTable": "msdyn_organizationalunit"}`

### CHOICE Field Format
Use the **integer option value**, not the label text:
```json
{"msdyn_schedulemode": 192350001}
```

### Fetch by ID
Format: `entityCollectionName/GUID`
```
msdyn_projects/d88015e0-ab48-4f22-8747-17bf4cc15f64
```

### Common Status Values

| Entity | Field | Draft | Submitted | Approved |
|--------|-------|-------|-----------|----------|
| Time Entry | `msdyn_entrystatus` | 192350000 | 192350003 | 192350002 |
| Expense | `msdyn_expensestatus` | 192350000 | 192350001 | 192350002 |
| Project Approval | `msdyn_recordstage` | 3 (Pending) | 0 | 2 |

### Transaction Type Codes (`msdyn_transactiontypecode`)
| Value | Type |
|-------|------|
| 192350000 | Cost |
| 192350005 | Unbilled Sales |
| 192350004 | Billed Sales |
| 192350007 | Inter-Organizational Sales |
| 192350008 | Resourcing Unit Cost |

### Billing Status (`msdyn_billingstatus`)
| Value | Status |
|-------|--------|
| 192350004 | Ready to Invoice |

---

## Known Issues & Workarounds

### 1. PSS Plugin Blocks Direct Task Updates
**Problem:** `msdyn_projecttask` duration/effort cannot be updated via Dataverse API.  
**Workaround:** Use the WBS grid UI — click cell twice to enter edit mode, type value, press Enter.

### 2. Invoice Creation Fails — "No past dated transactions"
**Requirements for invoice creation:**
- Contract must be **Confirmed** (not Draft)
- Contract line must have `msdyn_project` linked
- Unbilled Sales actuals must exist with **past dates** (before today)
- Actuals must have `msdyn_billingstatus = 192350004` (Ready to Invoice)

### 3. No Unbilled Sales Actuals After Approval
**Cause:** Contract was not confirmed prior to approving entries.  
**Fix:** Confirm contract first, then create new time entries with past dates and approve them.

### 4. Approval Two-Step Process
**Problem:** Updating only `msdyn_projectapproval` without first updating the underlying entry fails.  
**Fix:** First update the entry status (time/expense) to Approved, then update the approval record.

### 5. Tab Key Exits WBS Iframe
**Problem:** Pressing Tab in the WBS grid navigates out of the iframe context.  
**Fix:** Use Enter (submit=true) to commit cell values.

### 6. Select-All Checkbox in Grid
**Problem:** The "Toggle selection of all rows" checkbox may be intercepted by an icon overlay.  
**Fix:** Click the wrapper element adjacent to the checkbox, not the checkbox itself.

### 7. Area Switcher Dropdown Closes
**Problem:** The D365 area switcher dropdown may close before you can click an area.  
**Fix:** Navigate directly via URL with the correct `pagetype` and `etn` parameters.
