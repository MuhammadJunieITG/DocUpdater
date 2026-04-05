# Prospects

The Prospects feature enables the business to manage potential dealers who are not yet registered in the system.

A **Prospect** represents a qualified lead that is:

- Created by HD personnel
- Enriched with information by the BDM
- Eventually converted into a Dealer Account by the MDM

The **Prospect List Page** (also referred to as the *Prospect Management Page*) is the primary entry point for viewing, filtering, and acting on all prospects and leads in the system.

## Prospect List Page

The Prospect List Page provides:

- Centralized visibility into all prospects and leads
- Action tracking for users responsible for next steps
- Efficient navigation to prospect details and creation

### Page Structure

#### Header Area

- Breadcrumb navigation
- **New Lead** button — entry point to create a new lead, then prospect
- Page title: **Prospects**

#### Tabs (Lifecycle Views)

The page is organized into three tabs:

| Tab | Description |
| --- | --- |
| **Action Required** | Prospects or leads requiring action or review by the logged-in user |
| **In Progress** | Prospects or leads currently being worked on by other users |
| **Closed** | Activated, rejected, or lost prospects and leads |

Each tab displays the same table structure and supports the same controls.

### Table Columns (All Tabs)

Each prospect row displays:

- **Contact Name** — concatenation of first name + last name
- **Phone Number**
- **Stage**
- **Region**
- **Sub-Region**
- **Created Date**
- **Last Updated Date**

### Search

Free-text search across multiple criteria:

- Name
- Phone
- Email
- City
- State code
- Company name

### Filters

Available filters:

- Regions
- Sub-Regions
- Stages
- Created Date
- Last Updated Date
- Assigned BDM

Filters can be combined and cleared independently.

### Sorting

Sorting is supported on:

- Name
- Created Date
- Last Updated Date

Sorting applies per tab.

### Pagination

Pagination options: **10, 20, 30, 50**.

Pagination state is preserved when switching tabs.

### What is pending?

- From BED, mostly ready except for **Region**, **Sub-Region**, and sorting on last names
- Pagination testing — small issues
- Chips are not showing up — but this is per the requirements
- Loading effect when removing filters

---

## Lead Creation & Conversion Flow

### Description

A **Lead** represents an early-stage potential dealer with minimal required information. Leads are created to capture opportunity quickly and can later be converted into Prospects once validated and ready for progression through approval.

### Creating a New Lead

From the **Prospect List / Prospect Management Page**, the user clicks **New Lead**.

### Lead Creation Form (Small Form)

The Lead Creation Form is a lightweight form designed for fast data capture.

#### Identity & Contact Information

- First Name
- Last Name
- Company Name
- Primary Contact (phone number or email)

#### Location

- **Region** — *Not ready yet for the BE (blocked on SAP)*
- **Sub-Region** — *Not ready yet for the BE (blocked on SAP)*

#### Assignment Logic

- **If the creator is a BDM:** the lead is automatically assigned to the creating BDM
- **If the creator is NOT a BDM:** the *Assign to BDM* field is required, and the user selects a BDM from a dropdown

#### Additional Information

- Optional additional information fields (as needed)
- Comments (optional free-text)

### Submission

1. User clicks **Submit**
2. Lead is created successfully
3. Lead appears in the Prospect List Page
4. Initial stage is set to **New**

If the user is a BDM, the CTAs will be:

- **Mark as Lost**
- **Convert to Prospect** — submits the lead and converts it into a Target prospect
- **Save** — represents a lead submission

### Lead Behavior After Creation

- Lead exists as a read-only entity, only editable for assigned BDMs through the Side Panel
- No approval process is triggered at this stage
- Lead is visible in the Prospect List under the appropriate tab

### Viewing a Lead

- Clicking a lead opens the **Side Panel**
- All lead information is pre-filled

### BDM-Specific Actions

If the logged-in user is a BDM and is assigned to the lead, the following CTAs appear:

- **Mark New Lead as Lost**
- **Convert to Prospect** (displayed at the bottom of the side panel)
- **Save**

### What is pending?

- Region and Sub-Region
- Mark as Lost in the Lead Creation Form on the FE

---

## Converting a Lead to a Prospect

When any user converts a Lead into a Prospect, the system opens the **Target Prospect Form**, a multi-tab, structured form used to enrich, validate, and qualify the potential dealer before submission and approval.

This form mirrors the Opportunity creation experience, using tabs and save-in-progress behavior.

- Leads are not submitted directly
- A Lead must first be converted into a Prospect
- Conversion can be performed by any user

### Conversion Action

1. User clicks **Convert to Prospect**
2. The Side Panel shows the **Create Prospect** form
3. Lead is transformed into a Prospect entity with a status of **Target**
4. The converted prospect still requires BDM approval to be ready for further progression

### Stage Transition

| Entity | Stage |
| --- | --- |
| Lead | New |
| Prospect | Target |

**Target** indicates that the Prospect has been created but is not yet ready for final submission or approval. The prospect remains in this stage until a BDM provides approval to advance it to ready status.

### Post-Conversion Behavior

- Prospect now follows the Prospect lifecycle
- Additional data can be captured
- Prospect requires BDM approval before submission for final approval
- Any user can perform the conversion, but BDM approval is mandatory for progression
