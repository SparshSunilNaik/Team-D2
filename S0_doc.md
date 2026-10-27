# Building Permit Approval and Inspection Management System

**Role-Based Building Permit Approval & Inspection Workflow Management System — Chicago Building Permits Dataset**
Gate 0 / Stage S0 — Problem Definition & Need Identification

---

## 0. Project Details

| Item | Details |
|---|---|
| Team No. | 2 |
| Theme No. | 1 |
| Artefact Name | Building Permit Approval and Inspection Management System |
| Dataset | Chicago Building Permits Dataset |
| Guide | Sunil Gurlahosur |
| Department | Computer Science & Engineering |

**Team Members**

| Name | USN | Roll No. |
|---|---|---|
| Sanmathi Hegde | 01FE24BCS269 | 407 |
| Annapurna Boratti | 01FE24BCS283 | 420 |
| Amruta Kutri | 01FE24BCS275 | 412 |
| Akhil Teja | 01FE24BCS284 | 421 |

**Order of work (7 steps):** (1) The Problem → (2) Who Is Involved → (3) How It Works Today → (4) Problem & Goals → (5) What's Included → (6) Can We Do This → (7) What Could Go Wrong. The sequence: understand the problem and its people, map the current process, translate observations into needs and objectives, then bound the scope and check feasibility.

---

## 1. The Problem (Step 1 of 7)

### 1.1 Foundational Courses

| # | Course | Core Concepts |
|---|---|---|
| 1 | Data Structures & Algorithms (DSA) | Searching, sorting, data organization, workflow/state handling |
| 2 | Operating Systems (OS) | Process management, concurrency, resource management |
| 3 | Database Management Systems (DBMS) | ER modelling, normalization, transactions, constraints, indexing |
| 4 | Web Technology | REST APIs, client-server architecture, HTTP methods, authentication, frontend-backend integration |
| 5 | Software Engineering | Requirements, modular design, workflow modelling, testing and validation |
| 6 | Computer Networks | Client-server communication, HTTP/HTTPS, API communication |

### 1.2 Existing Problem / Current Situation

Building permit applications pass through multiple stakeholders and stages, including submission, verification, reviews, corrections, approvals and inspections. Without a centralized workflow, tracking application status, assigning applications, managing resubmissions and controlling user actions becomes difficult. This can result in delays, poor visibility of progress and reduced accountability.

### 1.3 Who Is Affected?

- **Property Owners / Applicants** – face delays, repeated corrections, and difficulty tracking application status.
- **Contractors / Architects** – need to coordinate documents, corrections, and approvals across departments.
- **Permit Reviewers, Zoning Officers, Department Officers (Municipal / Planning Departments)** – handle multiple applications, reviews, and approval workflows.
- **Building Inspectors** – need accurate application details and inspection schedules.
- **Finance Officers, Administrators, Public Users**
- **Government Authorities** – require transparency, accountability and proper monitoring of the overall process.

### 1.4 Why the Existing Approach Is Inadequate

- **No centralized tracking** — difficult to know the current status of an application.
- **Manual application assignment** — applications may be difficult to assign to the appropriate officer.
- **Difficult correction handling** — corrections and resubmissions are harder to manage and track.
- **Uncontrolled access** — without role-based controls, unauthorized actions may occur.
- **Limited process visibility** — progress across multiple reviews, approvals and inspections is difficult to monitor.
- **Poor accountability** — tracking who performed important actions across the workflow can be difficult.

### 1.5 Evidence That This Problem Is Real

**Chicago Building Permits Dataset** — real-world historical permit records used to study the building permit process.
Link: <https://data.cityofchicago.org/Buildings/Building-Permits/ydr8-5enu/about_data>

---

## 2. Who Is Involved? (Step 2 of 7)

### 2.1 Stakeholder Table

| Stakeholder | Role / Description | Needs & Expectations | Current Pain Points | Influence (H/M/L) |
|---|---|---|---|---|
| **Property Owner (Applicant)** | Submits permit application and documents | Easy submission, status visibility, timely decisions | Difficult to track application progress and corrections | H |
| **Contractor (Architect)** | Provides project and construction details | Clear requirements and review feedback | Repeated corrections and unclear review status | M |
| **Permit Reviewer** | Reviews submitted application | Complete documents and organized applications | Manual review coordination and application tracking | H |
| **Zoning Officer** | Checks zoning-related requirements | Accurate application information and clear workflow | Difficulty coordinating zoning checks with other stages | H |
| **Building Inspector** | Performs inspections | Proper scheduling and access to application details | Inspection coordination and result tracking | H |
| **Department Officer (Senior)** | Reviews and approves/rejects applications | Complete review information and workflow visibility | Difficult to monitor applications across stages | H |
| **Finance Officer** | Handles permit fees/payment status | Accurate fee and payment information | Payment status may be difficult to coordinate with permit workflow | M |
| **Admin** | Manages users, roles and permissions | Secure access and centralized user management | Managing different permissions across stakeholders | H |
| **Public User** | Views permitted-project information where publicly available | Easy access to permitted-project information | Limited visibility of relevant public information | L |

### 2.2 Primary vs. Secondary Stakeholders

*Primary:* directly use or are directly affected by the system. *Secondary:* indirectly involved (e.g., administrators, oversight bodies).

| Primary Stakeholders | Secondary Stakeholders |
|---|---|
| Property Owner (Applicant), Contractor (Architect), Permit Reviewer, Zoning Officer, Building Inspector, Department Officer (Senior), Finance Officer, Admin, Public User | — |

### 2.3 Key Insight Summary

The stakeholder analysis shows that property owners, contractors, reviewers, zoning officers, inspectors, department officers and finance officers are directly involved in the permit process and therefore have the highest need for clear workflow coordination. Their main needs are better status visibility, organized application handling, timely reviews, and coordination across different stages.

The system must also provide secure role-based access for administrators and appropriate access to publicly available information for public users. Overall, priority should be given to stakeholders who directly handle or depend on the progress of permit applications.

---

## 3. How It Works Today (Step 3 of 7)

### 3.1 Current Process

A building permit application begins with the property owner/applicant submitting the application and required documents, with project and construction details provided by the contractor/architect. The application then goes through document verification and departmental reviews, including zoning-related checks. If corrections are required, the application is returned for correction and resubmission before proceeding.

After the required reviews are completed, the application moves toward approval/rejection and permit fee handling, followed by building inspection. Multiple stakeholders are involved at different stages, making it difficult to maintain a clear view of the application's current status, assignments, corrections and overall progress.

### 3.2 Step-by-Step Workflow Table

| Step | Actor / Role | Action Performed | Tool / System Used | Pain Point Observed |
|---|---|---|---|---|
| 1 | Applicant / Property Owner | Prepares and submits building permit application and required documents | City of Chicago permit services / online application process | Multiple requirements must be prepared correctly |
| 2 | Contractor / Architect | Provides project plans, construction details and supporting information | Permit application / plan submission process | Incomplete or incorrect information may require corrections |
| 3 | Department of Buildings / Permit Reviewer | Reviews application and submitted plans | Chicago Department of Buildings permit-review process | Review may involve multiple requirements and stages |
| 4 | Zoning / Relevant Review Staff | Checks applicable zoning and other departmental requirements | City departmental review process | Coordination between different review requirements |
| 5 | Applicant / Contractor | Provides corrections or additional information when requested | Permit application / resubmission process | Revisions can extend processing time |
| 6 | Department of Buildings | Completes review and approves or rejects the application | Chicago permit system/process | Applicant needs visibility into application progress |
| 7 | Applicant / Finance | Completes required permit fee/payment requirements | City payment / permit process | Payment status must be coordinated with permit processing |
| 8 | Building Inspector | Conducts required inspection(s) during construction | Chicago building inspection process | Inspection scheduling and results involve another stage of the process |

### 3.3 AS-IS Workflow Diagram

Swim-lane lanes: Property Owner/Applicant → Contractor/Architect → Permit Reviewer → Zoning/Department Officers → Department Officer (Senior) → Finance Officer → Building Inspector. A "Corrections required?" decision loops back through correction/resubmission and re-review; key pain points are noted below the diagram.

![AS-IS Workflow](S0_doc_media/as_is_workflow.jpg)

*Fig 1: AS-IS Workflow — how the system works currently.*

**Key pain points shown on the diagram:** difficult to track application status · poor coordination between stakeholders · correction/resubmission tracking is manual · assignment of applications is unclear · limited visibility and accountability.

### 3.4 Bottlenecks & Inefficiencies Identified

- **Difficult status tracking** across different permit stages.
- **Unclear application assignment** to the appropriate officers.
- **Manual correction and resubmission tracking** can cause delays.
- **Poor coordination** among multiple departments and stakeholders.
- **Limited workflow visibility** makes overall progress difficult to monitor.
- **Weak accountability** for actions performed during the process.

---

## 4. Problem & Goals (Step 4 of 7)

### 4.1 Observed Problems → Underlying Needs

| # | Observed Problem | Evidence / Source | Underlying Need | Linked Stakeholder(s) |
|---|---|---|---|---|
| 1 | Difficult to track application status | Project-identified workflow gap | Centralized status tracking | Applicant, Contractor, Reviewer |
| 2 | Difficult application assignment | Project-identified workflow gap | Structured assignment | Reviewer, Zoning Officer, Admin |
| 3 | Corrections/resubmissions are difficult to manage | Project-identified workflow gap | Correction & resubmission tracking | Applicant, Contractor, Reviewer |
| 4 | Multiple stakeholders must coordinate | Stakeholder/process analysis | Role-based workflow coordination | All processing roles |
| 5 | Risk of unauthorized actions | Project-identified access-control gap | RBAC & permissions | Admin, Officers, Reviewers |
| 6 | Limited process visibility/accountability | Proposed workflow requirements | Audit logs, notifications & monitoring | Admin, Department Officer |

### 4.2 Prioritization

| # | Underlying Need | Justification |
|---|---|---|
| 1 | Centralized application status tracking | Most important because stakeholders need clear visibility of where each permit application currently stands. |
| 2 | Role-based workflow coordination | Multiple stakeholders handle different stages, so proper coordination is essential for the process to move correctly. |
| 3 | Correction & resubmission tracking | Corrections can cause delays if requests and revised submissions are not properly tracked. |
| 4 | Structured application assignment | Applications need to reach the appropriate reviewer or officer to avoid delays and workflow confusion. |
| 5 | RBAC & permission management | Ensures users can perform only the actions appropriate to their roles and reduces unauthorized actions. |
| 6 | Audit logs, notifications & monitoring | Improves accountability and keeps stakeholders informed, but depends on the core workflow and tracking being established first. |

### 4.3 Problem Statement

> Building permit applications involve multiple stakeholders and stages, creating challenges in coordinating approvals and inspections, tracking application status, managing workflow activities, and maintaining accountability throughout the process.

### 4.4 Project Objectives

1. **To implement role-based access control** so that each stakeholder can perform only the actions permitted for their assigned role.
2. **To manage the complete building permit workflow** from application submission through review, approval/rejection, fee handling, and inspection.
3. **To provide centralized application status tracking** so that the current stage and progress of each permit application can be viewed by authorized users.
4. **To manage corrections and resubmissions** by recording review feedback, revised submissions, and their corresponding workflow status.
5. **To maintain an auditable record of workflow activities** including application updates, reviews, approvals/rejections, and inspection outcomes.
6. **To provide workflow reports and analytics** using the Chicago Building Permits dataset to support monitoring and analysis of permit-related activities.

---

## 5. What's Included (Step 5 of 7)

### 5.1 Proposed Solution & TO-BE Workflow

A secure, role-based web system to manage building permits from application to completion. It automates verification, assignment, reviews, corrections, approvals, payments, and inspections through a defined workflow. RBAC, status tracking, notifications, and audit logs ensure secure and transparent processing.

![TO-BE Workflow](S0_doc_media/to_be_workflow.png)

*Fig 2: TO-BE Workflow Diagram* — Application Submitted → Document Verification → Application Assigned → Technical/Building Review → Zoning Review → Other Department Reviews → **Approved?** — *No:* Correction Required → Resubmission → back to Document Verification (resubmission cycle); *Yes:* Fee Payment → Permit Issued → Construction/Work Execution → Inspection Scheduled → Inspection Conducted → Final Inspection → Project Closed → End.

### 5.2 In-Scope

| # | In-Scope Item |
|---|---|
| 1 | User & Role Management |
| 2 | Building Permit Application Management |
| 3 | Permit Approval Workflow |
| 4 | Inspection Management |
| 5 | Status Tracking, Notifications & Audit Logs |
| 6 | Reports & Analytics |

### 5.3 Out-of-Scope

| # | Out-of-Scope Item | Reason for Exclusion |
|---|---|---|
| 1 | Actual legal issuance of Chicago building permits | Academic workflow system; cannot replace the official government permit issuance process. |
| 2 | Real financial/payment processing | The system may record payment/fee status, but will not process real monetary transactions. |
| 3 | Real government authentication or identity verification | Implementing official government authentication is outside the semester project's scope. |
| 4 | Legally binding approval or rejection of permits | Decisions made within the prototype carry no legal or regulatory authority. |
| 5 | Integration with live Chicago government systems | Direct integration with production municipal systems is beyond the project's technical and access constraints. |
| 6 | Physical inspection activities | The system records/tracks inspection information, but actual inspections remain outside the software's scope. |

### 5.4 Assumptions

- The Chicago Building Permits dataset is available and suitable for project analysis and testing.
- Users will have valid accounts and be assigned appropriate roles and permissions.
- Workflow activities such as reviews, approvals, corrections, payments, and inspections can be simulated within the system.
- The required development tools, database, and computing resources will be available throughout the semester.

### 5.5 Constraints

- Limited project time during the semester.
- Limited team size and development resources.
- Dependence on the available Chicago Building Permits Dataset.
- No access to live Chicago government systems.
- Real payments and legally binding permit decisions are not supported.

---

## 6. Can We Do This? (Step 6 of 7)

### 6.1 Proposed Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React |
| Backend | Spring Boot + Spring Data JPA |
| Database | PostgreSQL |
| Authentication & Security | Spring Security + JWT |
| ML/AI Services | Python + FastAPI |
| API Documentation | Swagger |
| Testing | JUnit + Mockito |
| API Integration | Axios |
| Version Control | Git + GitHub |


### 6.2 Technical Feasibility — Feasible

| Aspect | Assessment | Justification |
|---|---|---|
| Technology Stack | Feasible | React, Spring Boot + Spring Data JPA, PostgreSQL and Python/FastAPI are suitable for the proposed system. |
| Development Skills | Feasible | The required skills can be acquired and applied within the project duration. |
| Database & Dataset | Feasible | The database can manage workflow data and the Chicago Building Permits Dataset can support analysis. |
| System Integration | Feasible | React can communicate with the Spring Boot backend through REST APIs. |

### 6.3 Operational Feasibility — Feasible

| Aspect | Assessment | Justification |
|---|---|---|
| User Roles | Feasible | Different stakeholders can use the system according to their assigned roles and permissions. |
| Workflow Usage | Feasible | The system supports the major permit activities through a structured workflow. |
| User Adoption | Feasible | Centralized status tracking makes it easier for users to monitor application progress. |

### 6.4 Time Feasibility — Feasible

| Aspect | Assessment | Justification |
|---|---|---|
| 15-Week Timeline | Feasible | The defined scope can be completed within the semester by developing the core workflow first and adding supporting features afterward. |
| Development Phases | Feasible | Requirements, design, implementation, testing and final demonstration can be completed in planned stages. |
| Scope Management | Feasible | Clear in-scope and out-of-scope boundaries help prevent scope creep during the semester. |

### 6.5 Resource Feasibility — Feasible

| Aspect | Assessment | Justification |
|---|---|---|
| Team & Skills | Feasible | The project can be divided among team members based on frontend, backend, database and data analysis tasks. |
| Data Availability | Feasible | The Chicago Building Permits Dataset is available for project development and analysis. |
| Software & Tools | Feasible | The required development frameworks, database and programming tools are accessible to the team. |

### 6.6 Overall Feasibility Conclusion

The project is feasible within the available time, resources and technology stack. The core workflow can be developed using the available tools and the Chicago Building Permits Dataset can support analysis and testing. However, the scope should be controlled and complex integrations such as live government systems, real payments and legally binding permit decisions should remain out of scope.

---

## 7. What Could Go Wrong (Step 7 of 7)

### 7.1 Project-Level Risks

| Risk ID | Risk Description | Category | Likelihood | Impact | Mitigation Strategy |
|---|---|---|---|---|---|
| R1 | Large dataset may affect database performance | Technical | M | H | Use proper indexing and optimize database queries |
| R2 | Complex multi-role workflow may be difficult to implement correctly | Technical | M | H | Develop and test each workflow stage separately |
| R3 | Unauthorized users may access restricted functions | Security | M | H | Implement role-based access control and permission checks |
| R4 | Project scope may expand beyond the available semester time | Scope | H | H | Keep core features prioritized and strictly follow the defined scope |
| R5 | Difficulties integrating frontend, backend and Python/FastAPI services | Technical | M | M | Define clear APIs and integrate modules incrementally |
| R6 | Missing or inconsistent data in the Chicago Building Permits Dataset may limit analysis | Data | M | M | Perform data cleaning and use only relevant available fields |
| R7 | Development delays may affect testing and final demonstration | Timeline | M | H | Follow a phased development plan and complete core features first |

### 7.2 Risk Owner Summary

| Risk ID | Risk Description | Risk Owner |
|---|---|---|
| R1 | Large dataset may affect database performance | Annapurna Boratti |
| R2 | Complex multi-role workflow may be difficult to implement correctly | Amruta Kutri |
| R3 | Unauthorized users may access restricted functions | Sanmathi Hegde |
| R4 | Project scope may expand beyond the available semester time | Akhil Teja |
| R5 | Difficulties integrating frontend, backend and Python/FastAPI services | Annapurna Boratti |
| R6 | Missing or inconsistent data in the Chicago Building Permits Dataset may limit analysis | Sanmathi Hegde |
| R7 | Development delays may affect testing and final demonstration | Amruta Kutri |

---

## 8. Success Criteria, Applications & Learning Outcomes

### 8.1 Success Criteria

- **Secure Access:** Users can log in securely and access only authorised features.
- **Workflow Management:** Permits follow valid workflow stages with proper assignment, review, correction, and approval.
- **Inspection Management:** Inspections can be scheduled and their results recorded.
- **Security & Auditing:** Unauthorized actions are blocked and important activities are logged.
- **Data Management:** Database operations are reliable and transaction-safe.
- **Tracking & Reporting:** Users can track permit status, workflow history and view reports/dashboard analytics.

### 8.2 Need & Application

**Why is this needed?** Building permits involve multiple stages and stakeholders. A centralised workflow system can make the process easier to track and provide accountability.

**Applications** — the system can be used as an academic model for: building permit management · construction approval · inspection management · municipal workflow automation · application tracking · officer assignment.

### 8.3 Intended Understanding

- **RBAC & Security:** Authentication, authorization, and role-based access.
- **Workflow Management:** State transitions, approvals, corrections, and inspections.
- **Database Management:** Relational database design, transactions and data handling.
- **Backend & APIs:** REST APIs using Spring Boot and frontend integration.
- **Testing & Auditing:** Access-control testing, validation, error handling, and audit logs.
- **Scalability & Performance:** Handling multiple users and permit applications efficiently.