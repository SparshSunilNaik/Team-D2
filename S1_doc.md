# Civic Issue Reporting and Resolution Management System

**Stage S1 — Functional Requirements Engineering (Gate 1 Requirements Baseline)**
Detailed engine decomposition and requirements workbook

---

## 0. Project Details

| Item | Details |
|---|---|
| Team No. | 4 |
| Project Title | Civic Issue Reporting and Resolution Management System |
| Guide | Prof. Sunil V G |
| Date Prepared | 28/09/26 |

| Name | SRN |
|---|---|
| Akash Hugar | 01FE24BCS271 |
| Sandeepgouda Goudar | 01FE24BCS264 |
| Lahari Banakar | 01FE24BCS274 |
| Pavitra S A | 01FE24BCS270 |

**What S1 covers:** starting from the approved S0 problem, stakeholders, pain points and scope, this stage breaks the system into independently ownable technical **engines**, then specifies it through requirements (FR/NFR), use cases, acceptance criteria, priorities, a traceability matrix and detailed engine sheets.

---

## 1. Engine Decomposition

### 1.1 How the engines were derived

Each engine groups related responsibilities that share the same technical mechanism, state or control, and that can be explained, owned, implemented and tested on its own. Engines are named after a technical responsibility, not a screen or layer (no "Frontend", "Database", "Login Page"). For each engine: a problem function from S0 is identified, related functions are grouped, turned into one precise responsibility, bounded (owns / does not own), defined (I/O, state, mechanism, failures, KPI), assigned one primary owner, and finally linked to requirement IDs.

### 1.2 Engine Summary

| Engine | Name | Major Courses | Technical Problem Owned | Primary Responsibility | Owner |
|---|---|---|---|---|---|
| E1 | Complaint Processing & Assignment Engine | Web Technology + DSA + OS + DBMS | Invalid complaint data, incorrect classification, improper priority order, unsuitable officer assignment | Receive, validate and register complaints; classify and map departments; calculate priority; maintain priority order; assign eligible officers | Lahari Banakar |
| E2 | SLA, Resolution & Verification Engine | OS + Web Technology + DBMS | Delayed complaints, SLA violations, uncontrolled resolution/closure | Monitor SLA; detect and escalate breaches; manage status and resolution; verify, close and re-open complaints | Pavitra S A |
| E3 | Hotspot Analysis & Route Optimization Engine | DSA + DBMS | Difficulty identifying complaint concentrations and generating efficient visit orders | Analyze complaint locations, identify hotspots and generate optimized visit orders for multiple assigned complaints | Akash Hugar |
| E4 | Identity, Role & Access Control Engine | Web Technology + DBMS + Security | Unauthorized access and incorrect role-based permissions | Authenticate users, identify roles, enforce permissions and control access to protected functions | Sandeepgouda Goudar |

---

## 2. Software Requirements Specification (SRS)

### 2.1 Functional Requirements

| FR ID | Description | Priority | Source Need (from S0) |
|---|---|---|---|
| FR-01 | The system shall authenticate users and provide access to system functions according to their assigned role. | Mandatory | Role-based access to the complaint management system |
| FR-02 | The system shall allow citizens to raise a civic complaint with description, category, location and supporting evidence, validate the required information, and generate a unique complaint ID. | Mandatory | Structured and identifiable civic issue reporting |
| FR-03 | The system shall classify each complaint into a predefined category and map it to the responsible department. | Mandatory | Appropriate department routing |
| FR-04 | The system shall calculate a priority score using configured factors such as severity, impact, urgency and complaint age, and maintain pending complaints in priority order. | Mandatory | Consistent prioritization and timely handling |
| FR-05 | The system shall assign complaints to eligible field officers based on department, availability, workload and location, and record the assignment. | Mandatory | Suitable resource allocation and assignment accountability |
| FR-06 | The system shall allow field officers to view assigned complaints and update their status through defined complaint lifecycle states. | Mandatory | Complaint progress and lifecycle tracking |
| FR-07 | The system shall monitor the SLA/deadline of each complaint and identify complaints approaching or exceeding the configured SLA. | Mandatory | Timely complaint handling and SLA monitoring |
| FR-08 | The system shall automatically escalate SLA-breached or unattended complaints to the appropriate supervisor. | Mandatory | Escalation of delayed or unattended complaints |
| FR-09 | The system shall allow field officers to submit resolution details and supporting evidence, and allow supervisors to verify or reject the resolution before closure. | Mandatory | Controlled resolution, verification and accountability |
| FR-10 | The system shall allow citizens to view the current status, progress and resolution information of their submitted complaints. | Mandatory | Citizen transparency and complaint tracking |
| FR-11 | The system shall allow citizens to raise a re-open/review request when a complaint is not properly resolved, subject to the defined workflow. | Mandatory | Citizens reporting unresolved or improperly resolved issues |
| FR-12 | The system shall allow administrators to manage users, roles, departments, complaint categories, SLA rules and system configurations. | Mandatory | Role-based system administration and configuration |
| FR-13 | The system shall provide authorized users with complaint, workload, priority, SLA and resolution information through appropriate dashboards or reports. | Mandatory | Monitoring, accountability and data-driven civic management |
| FR-14 | The system shall analyze complaint locations and identify areas with high concentrations of complaints. | Challenge | Identifying recurring civic issue areas |
| FR-15 | The system shall generate an optimized visit order for multiple complaints assigned to the same field officer. | Challenge | Efficient field operations and route planning |

### 2.2 Non-Functional Requirements

| NFR ID | Description | Category | Measurable Target |
|---|---|---|---|
| NFR-01 | Timely responses for normal operations such as login, complaint submission, status viewing and dashboard loading. | Performance | At least 95% of tested requests respond within 2 seconds under the defined project test load. |
| NFR-02 | Enforce authentication and role-based authorization for protected functions. | Security | 100% of protected operations reject users without the required role/permission. |
| NFR-03 | Protect user credentials and sensitive complaint information during storage and communication. | Security | Passwords securely hashed; deployed client-server communication uses HTTPS. |
| NFR-04 | Maintain data consistency throughout the complaint lifecycle. | Data Integrity | In testing, 100% of valid lifecycle transitions preserve complaint ID, status history, assignment and resolution records. |
| NFR-05 | Provide understandable interfaces appropriate to each user role. | Usability | At least 90% of test users complete core tasks (submit, assign, update, verify) without assistance. |
| NFR-06 | Maintain an auditable history of important complaint operations. | Traceability | 100% of status, assignment, escalation and resolution changes record the responsible user and timestamp. |
| NFR-07 | Prevent invalid data from entering or corrupting the complaint workflow. | Data Validation | 100% of mandatory-field and invalid-state test cases rejected with an appropriate validation response. |

---

## 3. Use Cases / User Stories

### 3.1 Use Case Table

| ID | Actor | Description / User Story | Main Flow | Exception Flow |
|---|---|---|---|---|
| UC-01 | Citizen | Submit a civic complaint with description, category, location and optional evidence so the issue can be processed. | Login → enter complaint details → select/use location → upload evidence → submit → complaint ID generated → status = Submitted | Missing/invalid data → validation error → citizen corrects and resubmits |
| UC-02 | Citizen | Track my complaint to know its current status and progress. | Login → open My Complaints → select complaint → view status, assignment/progress and updates | Complaint ID not found / unauthorized access → appropriate error |
| UC-03 | System | Classify a complaint into a predefined category and map it to the responsible department. | Complaint submitted → validate category → apply category-department mapping → store category and department | Category unavailable/ambiguous → mark for manual review |
| UC-04 | System | Calculate and maintain complaint priority so higher-priority complaints are processed first. | Complaint received → calculate severity/impact/urgency/age → generate priority score → insert into priority queue | Required priority data missing → use configured default / manual review |
| UC-05 | System | Update waiting complaints using aging so low-priority complaints are not ignored indefinitely. | Complaint remains pending → background process checks waiting time → aging score increases → priority recalculated → queue updated | Background process failure → record failure and retry/update next cycle |
| UC-06 | Supervisor / Department Official | Assign complaints to suitable officers based on department, availability and workload. | View prioritized complaints → select eligible department officers → check availability/workload → assign officer → record assignment | No suitable officer → keep complaint pending and flag for supervisor action |
| UC-07 | Field Officer | View assigned complaints and update their status so the system reflects actual progress. | Login → view assigned complaints → accept task → start work → update status → add remarks | Officer unavailable/rejects task → return complaint for reassignment |
| UC-08 | System / Supervisor | Monitor complaint deadlines and escalate complaints approaching or exceeding their SLA. | Complaint assigned → SLA timer starts → monitor deadline → warning → SLA breach → escalate to supervisor | Monitoring failure → retry monitoring and record the event |
| UC-09 | Field Officer | Submit resolution details and evidence so completed work can be verified. | Open assigned complaint → resolve issue → enter resolution description → upload solved image/evidence → submit resolution | Missing resolution evidence/details → reject submission and request correction |
| UC-10 | Supervisor | Verify an officer's resolution before closing the complaint. | View resolved complaint → check details/evidence → approve → status = Closed | Resolution inadequate → reject verification → return to officer |
| UC-11 | Citizen | Receive/view status updates to know when the issue is submitted, assigned, resolved or closed. | Status changes → notification/update generated → citizen views updated status | Notification failure → status remains available through complaint tracking |
| UC-12 | Supervisor / Admin | View complaint statistics and locations to understand workload and recurring civic issues. | Select dashboard → filter by category/location/status/time → system aggregates data → display results/hotspots | Invalid filter / no matching data → empty result with message |
| UC-13 | Field Officer | Get an optimized visit order for multiple assigned complaints to reduce unnecessary travel. | Officer has multiple assignments → obtain locations → generate route → apply route optimization → display visit order | Missing/unreachable location → exclude it and flag for correction |

### 3.2 Use Case Diagram

Actors: Citizen, Field Officer, Supervisor / Department Official, Admin and System (background process). Submitting a complaint includes providing a description, selecting a category, sharing location and uploading evidence, and leads into classification, priority calculation with aging, the priority queue, officer assignment, SLA monitoring/escalation, and recording and verifying resolution before closure. Admin manages users and roles, system parameters, audit logs and data backup/recovery.

![Use Case Diagram](S1_doc_media/civic_use_case_diagram.jpg)

---

## 4. Acceptance Criteria

| Requirement | Acceptance Criteria | Test / Verification Method |
|---|---|---|
| FR-01 | A user is authenticated with valid credentials and granted access only to functions permitted for their role. Invalid credentials and unauthorized role access are rejected. | Role-based functional and security testing with Citizen, Field Officer, Supervisor and Admin accounts. |
| FR-02 | A citizen submits a complaint with required description, category, location and evidence. The system validates mandatory data, stores the complaint and generates a unique complaint ID with status SUBMITTED. | Functional test with valid, missing and invalid inputs; verify database record, complaint ID and initial status. |
| FR-03 | Every valid complaint is assigned exactly one predefined category and the corresponding responsible department per the configured mapping. | Test complaints from all configured categories and verify resulting category and department. |
| FR-04 | The system calculates a priority score from configured severity, impact, urgency and age factors and keeps pending complaints in correct priority order. | Unit and integration tests with predefined values; verify scores and priority queue ordering. |
| FR-05 | A complaint is assigned only to an eligible field officer from the responsible department who satisfies the configured availability, workload and location conditions. The assignment is recorded. | Assignment test with officers of different departments, availability, workload and locations; verify selected officer and assignment record. |
| FR-06 | A field officer views assigned complaints and updates status only through valid lifecycle transitions such as ASSIGNED → IN_PROGRESS → RESOLVED. | Role-based functional test with valid and invalid status transitions. |
| FR-07 | The system calculates the configured SLA deadline, continuously monitors the complaint and identifies those approaching or exceeding the deadline. | Controlled-time test with short SLA values; verify deadline calculation, warning state and breach detection. |
| FR-08 | When a complaint exceeds its SLA or stays unattended per the escalation rule, the system creates an escalation and notifies/routes it to the appropriate supervisor. | Controlled-time escalation test; verify escalation record, target supervisor and notification/status. |
| FR-09 | A field officer submits resolution details and evidence; a supervisor verifies or rejects the resolution before final closure. | End-to-end test covering resolution submission, evidence upload, supervisor approval and rejection. |
| FR-10 | A citizen views current status, progress and resolution information only for their own submitted complaints. | Citizen-role test; verify correct information is shown and access to other citizens' complaints is denied. |
| FR-11 | A citizen submits a re-open/review request for a complaint not properly resolved; it enters the defined review/rework workflow. | Test after closure; submit request and verify REOPENED/REVIEW state and supervisor workflow. |
| FR-12 | An administrator creates, updates or deactivates users and manages roles, departments, categories, SLA rules and permitted configurations. | Admin-role test; verify changes and rejection of the same operations by unauthorized roles. |
| FR-13 | Authorized users view complaint, workload, priority, SLA and resolution information by role; dashboard/report values match underlying data. | Functional and database verification with a known test dataset; compare displayed values with query results. |
| FR-14 | The system processes valid location data and identifies high-concentration areas matching the configured spatial grouping/counting rules. | Algorithm test with a predefined location dataset; compare hotspots with manually calculated reference results. |
| FR-15 | For an officer with multiple assigned complaints with valid locations, the system generates and displays a feasible visit order using the configured route optimization method. | Algorithm test with predefined locations and road/graph data; verify route feasibility and visit sequence. |

*(NFR-01 to NFR-07 are verified against the measurable targets listed in section 2.2.)*

---

## 5. Priority Classification

| Requirement | Description | Priority | Justification |
|---|---|---|---|
| FR-01 | Authenticate users and provide role-based access. | Mandatory | Citizen, Field Officer, Supervisor and Admin have different responsibilities and permissions. |
| FR-02 | Raise, validate and register a complaint; receive a unique ID. | Mandatory | Entry point of the system; the lifecycle cannot begin without it. |
| FR-03 | Classify complaints and map to department. | Mandatory | Required before appropriate assignment and processing. |
| FR-04 | Calculate priority and keep complaints in priority order. | Mandatory | Core objective; demonstrates the Priority Queue / Max Heap component. |
| FR-05 | Assign complaints to eligible field officers. | Mandatory | Converts prioritized complaints into actionable field assignments. |
| FR-06 | Officers view assignments and update status through valid transitions. | Mandatory | Needed to track a complaint from assignment through resolution. |
| FR-07 | Monitor SLA/deadlines. | Mandatory | Detects delayed complaints and supports timely handling. |
| FR-08 | Auto-escalate breached or unattended complaints. | Mandatory | Provides corrective action when complaints are delayed. |
| FR-09 | Submit resolution; supervisor verifies or rejects before closure. | Mandatory | Controlled verification completes the lifecycle reliably. |
| FR-10 | Citizens view status, progress and resolution info. | Mandatory | Citizen transparency and tracking are essential. |
| FR-11 | Citizens raise re-open/review requests. | Mandatory | Feedback mechanism when the issue remains unresolved. |
| FR-12 | Admin manages users, roles, departments, categories, SLA rules, configuration. | Mandatory | Controlled administration of the role-based workflow. |
| FR-13 | Dashboards/reports for complaints, workload, priority, SLA, resolution. | Mandatory | Lets supervisors and administrators monitor operations and performance. |
| FR-14 | Hotspot identification from complaint locations. | Challenge / Stretch | Advanced spatial/DSA processing, but the core lifecycle works without it. |
| FR-15 | Optimized visit order for multiple assigned complaints. | Challenge / Stretch | Advanced DSA (graphs, shortest paths, TSP, 2-Opt), not required for the core lifecycle. |

*NFR-01 to NFR-07 are treated as baseline quality targets for the system.* Mandatory requirements must be satisfied for acceptance; Challenge requirements are stretch targets.

---

## 6. Requirements Traceability Matrix

Design references (S2–S4) and test references (S6) are to be added in later stages; all requirements are currently **Defined**.

| Req ID | Source Need (S0) | Owning Engine / Module | Design Owner | Test Owner |
|---|---|---|---|---|
| FR-01 | Authenticated, role-based access | E4 Identity, Role & Access Control | Sandeepgouda | Pavitra |
| FR-02 | Structured civic issue reporting | E1 Complaint Processing & Assignment | Lahari | Akash |
| FR-03 | Appropriate department routing | E1 | Lahari | Akash |
| FR-04 | Consistent prioritization and timely handling | E1 | Lahari | Akash |
| FR-05 | Resource allocation and assignment accountability | E1 | Lahari | Akash |
| FR-06 | Complaint progress and lifecycle tracking | E2 SLA, Resolution & Verification | Pavitra | Lahari |
| FR-07 | Timely handling and SLA monitoring | E2 | Pavitra | Lahari |
| FR-08 | Escalation of delayed/unattended complaints | E2 | Pavitra | Lahari |
| FR-09 | Controlled resolution, verification, accountability | E2 | Pavitra | Sandeepgouda |
| FR-10 | Citizen transparency and tracking | Supporting: E1 / E2 | Pavitra | TBD |
| FR-11 | Report unresolved/improperly resolved complaints | E2 | Pavitra | Sandeepgouda |
| FR-12 | Controlled administration of users, roles, configuration | E4 | Sandeepgouda | Akash |
| FR-13 | Monitoring, accountability, data-driven management | Supporting: E1 / E2 / E3 / E4 | Akash | Sandeepgouda |
| FR-14 | Identifying recurring civic issue areas | E3 Hotspot Analysis & Route Optimization | Akash | Sandeepgouda |
| FR-15 | Efficient field operations and route planning | E3 | Akash | Sandeepgouda |
| NFR-01 | Timely system responses | System-wide / relevant engines | Sandeepgouda | Pavitra |
| NFR-02 | Secure authentication and authorization | E4 | Sandeepgouda | Pavitra |
| NFR-03 | Protect credentials and sensitive complaint info | E4 | Sandeepgouda | Pavitra |
| NFR-04 | Data consistency across the lifecycle | System-wide / relevant engines | Sandeepgouda | Pavitra |
| NFR-05 | Understandable role-appropriate interfaces | System-wide / web interface | Pavitra | Akash |
| NFR-06 | Auditable history of operations | E2 / E4 + audit mechanism | Lahari | Akash |
| NFR-07 | Prevent invalid data corrupting the workflow | E1 / E2 + validation | Lahari | Akash |

---

## 7. Requirement Clustering

| Cluster | Responsibility Area | Requirements | Common Technical Responsibility | Engine |
|---|---|---|---|---|
| C1 | Identity, authentication & access control | FR-01, FR-12, NFR-02, NFR-03, NFR-06 | Authenticate users, manage roles and permissions, protect credentials and control access to protected functions. | E4 |
| C2 | Complaint processing, classification, priority & assignment | FR-02, FR-03, FR-04, FR-05 | Validate/register complaints, classify and map departments, calculate priority and assign eligible officers. | E1 |
| C3 | SLA, resolution & verification | FR-06, FR-07, FR-08, FR-09, FR-11 | Manage lifecycle, monitor SLA, escalate delays, verify resolution, close and re-open complaints. | E2 |
| C4 | Complaint tracking & operational reporting | FR-10, FR-13 | Provide citizen status/progress information and authorized dashboards/reports from system data. | Supporting: E1 / E2 / E3 / E4 |
| C5 | Location, hotspot & route optimization | FR-14, FR-15 | Analyze complaint locations, identify hotspots and generate efficient visit orders. | E3 |
| C6 | System-wide performance, integrity & validation | NFR-01, NFR-04, NFR-05, NFR-07 | Maintain timely responses, data consistency, role-appropriate usability and validation. | System-wide / relevant engines |

---

## 8. Engine Decomposition Matrix

| | E1 — Complaint Processing & Assignment | E2 — SLA, Resolution & Verification | E3 — Hotspot Analysis & Route Optimization | E4 — Identity, Role & Access Control |
|---|---|---|---|---|
| **Primary responsibility** | Receive, validate, classify, prioritize and assign complaints to eligible field officers. | Monitor SLAs, escalate delays, manage resolution, verify complaints and control closure/reopening. | Analyze complaint locations, identify hotspots and optimize visit order for multiple assigned complaints. | Authenticate users and enforce role-based access to protected functions. |
| **Inputs** | Complaint details, location, category, severity, impact, urgency, officer data | Complaint ID, assignment, SLA, status, time, resolution details | Complaint coordinates, categories, statuses, assignments, road/network data | Login details, user role, access request |
| **Outputs** | Complaint ID, category, department, priority, assigned officer | SLA status, escalation, updated status, verification and closure result | Hotspots, location counts, optimized visit order | Authentication result, session/token, ALLOW/DENY |
| **State / data owned** | Complaint details, priority, queue and assignment data | SLA status, lifecycle status, resolution and verification data | Spatial groups, hotspot data and route information | Users, roles, permissions and session data |
| **Core mechanism** | Validation + DBMS + rule-based classification + Max Heap/Priority Queue + eligibility filtering | Deadline checking + background processing + state transitions + role-based workflow | Hash Map + spatial grouping + Top-K + Graph + Dijkstra + TSP/2-Opt | Authentication + RBAC + password hashing + permission checking |
| **Dependencies** | E4 for authorization; E2 receives assigned complaints | E1 assignment data; E4 authorization; supervisor interface | E1 complaint/assignment data; field officer interface | DBMS; all engines requiring authorization |
| **Owner** | Lahari Banakar | Pavitra S A | Akash Hugar | Sandeepgouda Goudar |

---

## 9. Engine Description Sheets

### 9.1 Engine E1 — Complaint Processing & Assignment Engine

**Owner:** Lahari Banakar · **Requirements:** FR-02, FR-03, FR-04, FR-05 · **Area:** Web Technology + DSA + OS + DBMS

**Purpose.** Receives civic complaints and ensures only valid complaints enter the workflow. It registers the complaint, generates a unique Complaint ID, classifies it and maps it to the responsible department, then calculates priority, maintains the processing order and assigns the complaint to an eligible field officer. It combines complaint-entry and processing responsibilities into one independently testable unit.

**Boundary**

| Owns | Does NOT Own |
|---|---|
| Mandatory-field and data-format validation; unique Complaint ID generation and registration; predefined category/department mapping; priority score and priority queue state; aging updates for pending complaints; officer eligibility filtering and assignment records | User authentication and role management (E4); SLA monitoring and escalation (E2); resolution verification and closure (E2); hotspot analysis and route optimization (E3) |

**Inputs, outputs and state**

| Inputs / Trigger | Outputs / Result | State / Data Owned |
|---|---|---|
| Complaint description, category, location, evidence, citizen ID, classification rules, severity, impact, urgency, age, department, officer availability, workload and location | Validated complaint, unique Complaint ID, category, responsible department, priority score/order, selected officer, assignment record and status | Complaint details, classification, priority score, queue position, assignment records and processing status |

**Core mechanism**

| Mechanism / Rule | Why It Is Needed | Requirements |
|---|---|---|
| Input and mandatory-field validation; unique ID generation; DBMS transaction; predefined classification rules with Hash Map/DBMS lookup; priority scoring; Priority Queue/Max Heap; aging via background processing; eligibility filtering and workload/availability/location-based officer selection | Keeps the complaint-to-assignment pipeline consistent and lets priority information drive assignment directly | FR-02, FR-03, FR-04, FR-05 |

**Dependencies, failures and KPI**

| Interface / Dependency | Failure / Boundary Case | Handling / Recovery | KPI |
|---|---|---|---|
| E4 provides authorization; uses DBMS data; passes assigned complaints to E2; data also supports E3 and dashboards | Invalid/missing complaint data; database failure; unmapped category; invalid priority factors; no eligible officer | Reject/flag invalid input; retry DB operation; manual review for unmapped category; default/manual review for invalid priority data; keep unassigned and notify supervisor | ≥95% of valid complaints correctly processed; 100% invalid submissions rejected; 100% valid classifications mapped to a department; 100% tested assignments select eligible officers |

### 9.2 Engine E2 — SLA, Resolution & Verification Engine

**Owner:** Pavitra S A · **Requirements:** FR-06, FR-07, FR-08, FR-09, FR-11 (supports FR-10) · **Area:** OS + Web Technology + DBMS

**Purpose.** Manages the complaint after assignment. It monitors deadlines, identifies approaching or breached SLAs and escalates delayed or unattended complaints. It also manages status progression, resolution evidence, supervisor verification, closure and the citizen re-open/review workflow, giving controlled completion of the complaint lifecycle.

**Boundary**

| Owns | Does NOT Own |
|---|---|
| SLA deadlines and status; escalation records; lifecycle status and valid transitions; resolution details and evidence; supervisor verification; closure and re-open/review handling | Complaint intake, classification, priority and assignment (E1); hotspot and route processing (E3); authentication and access control (E4) |

**Inputs, outputs and state**

| Inputs / Trigger | Outputs / Result | State / Data Owned |
|---|---|---|
| Assigned complaint, assignment/start time, SLA duration, status, current time, resolution details and evidence, supervisor decision, citizen re-open/review request | SLA status, warning/breach status, escalation record, updated status, resolution record, verification result, closure or re-open/review state | SLA deadline/status, escalation state, status history, resolution record, verification status |

**Core mechanism**

| Mechanism / Rule | Why It Is Needed | Requirements |
|---|---|---|
| Deadline calculation; scheduler/background processing; time comparison; escalation rules; controlled lifecycle state machine; role-based resolution workflow; supervisor verification | Prevents complaints remaining unresolved beyond configured limits and prevents closure without controlled resolution and verification | FR-06, FR-07, FR-08, FR-09, FR-11 (supports FR-10) |

**Dependencies, failures and KPI**

| Interface / Dependency | Failure / Boundary Case | Handling / Recovery | KPI |
|---|---|---|---|
| E1 provides assigned complaints; E4 authorizes protected actions; supervisor, field-officer and citizen interfaces; DBMS stores lifecycle and resolution data | Invalid SLA; monitoring failure; already-resolved complaint; invalid status/resolution; supervisor rejection; invalid re-open request | Flag invalid SLA; retry/log failed checks; never escalate resolved complaints; reject invalid updates; return rejected resolution for correction; reject invalid re-open request | 100% of tested SLA breaches detected and escalated correctly; 100% invalid lifecycle transitions rejected; 100% tested closures have valid supervisor verification; 100% unauthorized updates blocked |

### 9.3 Engine E3 — Hotspot Analysis & Route Optimization Engine

**Owner:** Akash Hugar · **Requirements:** FR-14, FR-15 · **Area:** DSA + DBMS

**Purpose.** Uses complaint location data for spatial analysis and field planning. It identifies areas with high concentrations of complaints and generates efficient visit orders when an officer has multiple assigned complaints. The two location-based responsibilities are combined because both depend on complaint coordinates and spatial/graph processing.

**Boundary**

| Owns | Does NOT Own |
|---|---|
| Spatial grouping/cells and complaint counts; hotspot results; selected complaint locations for routing; route order and calculated distance/cost where available | Complaint intake and assignment (E1); SLA and resolution workflow (E2); user authentication and access control (E4) |

**Inputs, outputs and state**

| Inputs / Trigger | Outputs / Result | State / Data Owned |
|---|---|---|
| Complaint latitude/longitude, category, status, assigned complaint locations, officer start location, road/network data | Location-based counts, hotspot areas, optimized visit order, route distance/travel cost where available | Spatial groups/cells, counts, hotspot information, selected locations, route order and cost |

**Core mechanism**

| Mechanism / Rule | Why It Is Needed | Requirements |
|---|---|---|
| Spatial bucketing + Hash Map + counting/Top-K + DBMS aggregation for hotspots; graph representation + Dijkstra for shortest paths; TSP-like visit ordering; 2-Opt heuristic for practical route improvement | Identifies recurring high-complaint areas and reduces unnecessary travel when several complaints are handled in one visit | FR-14, FR-15 |

**Dependencies, failures and KPI**

| Interface / Dependency | Failure / Boundary Case | Handling / Recovery | KPI |
|---|---|---|---|
| Consumes complaint/location data from E1 and assignment/status data from E1/E2; uses DBMS, road/network data and the field-officer interface | Missing/invalid location; unreachable location; unavailable network data; too many locations | Flag/exclude invalid location; report unreachable location; report network-data failure; use practical route heuristic | ≥95% correct hotspot results against defined test datasets; ≥95% of valid route test cases produce feasible visit orders within the acceptable route distance/cost range |

### 9.4 Engine E4 — Identity, Role & Access Control Engine

**Owner:** Sandeepgouda Goudar · **Requirements:** FR-01, FR-12, NFR-02, NFR-03, NFR-06

**Purpose.** Authenticates users and determines what functions they may access, supporting role-based access for citizens, field officers, supervisors and administrators. It protects credentials and records important access-related operations for traceability, and provides the authorization boundary used by the other engines.

**Boundary**

| Owns | Does NOT Own |
|---|---|
| User authentication; role and permission mappings; authorization decisions; secure password handling; authentication/session information; access and authorization audit records | Complaint processing and assignment (E1); SLA/resolution workflow (E2); hotspot and route processing (E3) |

**Inputs, outputs and state**

| Inputs / Trigger | Outputs / Result | State / Data Owned |
|---|---|---|
| Login credentials, user/role information, protected-function access requests | Authentication result, session/token, authorization decision (ALLOW / DENY), audit information | User accounts, role/permission mappings, authentication/session information, audit records |

**Core mechanism**

| Mechanism / Rule | Why It Is Needed | Requirements |
|---|---|---|
| Authentication + role-based access control (RBAC) + secure password hashing + authorization checks + audit logging | Different actors have different permissions, so access must be controlled consistently across every protected operation | FR-01, FR-12, NFR-02, NFR-03, NFR-06 |

**Dependencies, failures and KPI**

| Interface / Dependency | Failure / Boundary Case | Handling / Recovery | KPI |
|---|---|---|---|
| DBMS stores user and role data; web interfaces invoke authentication/authorization; E1/E2/E3 rely on E4 for protected operations | Invalid credentials/session; insufficient permission; invalid role | Reject/re-authenticate; deny the protected operation; deny access and record important access events | 100% of protected operations require authentication and authorization; 100% of unauthorized role-access attempts rejected; 100% of tested access/authorization operations contain required audit information |