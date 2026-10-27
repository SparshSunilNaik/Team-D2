# Building Permit Approval and Inspection Management System

**Stage S1 — Functional Requirements Engineering (Gate 1 Requirements Baseline)**
Detailed engine decomposition and requirements workbook

---

## 0. Project Details

| Item | Details |
|---|---|
| Team No. | 02 |
| Project Title | Building Permit Approval and Inspection Management System |
| Guide | Sunil Gurlahosur |
| Date Prepared | 27/09/2026 |

| Name | SRN |
|---|---|
| Sanmathi Hegde | 01FE24BCS269 |
| Amruta Kutri | 01FE24BCS275 |
| Annapurna Boratti | 01FE24BCS283 |
| Akhil Teja | 01FE24BCS284 |

**What S1 covers:** starting from the approved S0 problem, stakeholders, pain points and scope, this stage breaks the system into independently ownable technical **engines**, then specifies the system through requirements (FR/NFR), use cases, acceptance criteria, priorities, a traceability matrix and detailed engine sheets.

---

## 1. Engine Decomposition

### 1.1 How the engines were derived

Each engine is a group of related responsibilities that share the same technical mechanism, state or control, and that can be explained, owned, implemented and tested on its own. Engines are named after a technical responsibility (not a screen or layer such as "Frontend" or "Database"). For each engine: a problem function from S0 is identified, related functions are grouped, converted into one precise responsibility, bounded (what it owns / does not own), defined (I/O, state, mechanism, failures, KPI), assigned one primary owner, and finally linked to requirement IDs.

### 1.2 Engine Summary

| Engine ID | Engine Name | Major Courses | Technical Problem Owned | Primary Responsibility | Primary Owner |
|---|---|---|---|---|---|
| E1 | Access Control & Security Engine | Web Technology, CN, OS | Unauthorized actions and insecure sessions | Token-based login over HTTPS, role-permission checks on every request, session expiry and account lockout | Akhil Teja |
| E2 | Permit Workflow & Decision Engine | SE, DSA | Invalid stage jumps and inconsistent decisions | State machine for valid transitions, review checks before approval, correction loop and workflow notifications | Annapurna Boratti |
| E3 | Transaction, Data & Audit Integrity Engine | DBMS, OS | Partial records, conflicting updates and untraceable actions | Atomic transactions, foreign-key checks, safe concurrent updates, recovery, document versioning and append-only audit trail | Amruta Kutri |
| E4 | Assignment, Routing & Workload Engine | DSA, OS, DBMS | Wrong or delayed assignment and uneven workload | Rule-based routing by type and zone, workload-based assignment, officer override, overdue escalation and workload analytics on the Chicago data | Sanmathi Hegde |

---

## 2. Software Requirements Specification (SRS)

### 2.1 Functional Requirements

| FR ID | Description | Priority | Source Need (from S0) |
|---|---|---|---|
| FR-01 | The system shall allow administrators to create user accounts and assign roles, and shall authenticate users and restrict every action and view to the permissions of their assigned role. | Mandatory | RBAC & permission management |
| FR-02 | The system shall allow applicants and contractors/architects to create and submit a building permit application with applicant details, property address, permit type, project description, estimated cost and documents, and shall validate mandatory fields before submission. | Mandatory | Role-based workflow coordination |
| FR-03 | The system shall assign an application to a permit reviewer, zoning officer or building inspector based on its application type, zone, current stage and workload, allow a Department Officer or Admin to override the assignment, and flag applications left unreviewed beyond a set time. | Mandatory | Structured application assignment |
| FR-04 | The system shall allow applicants to resubmit corrected applications and documents and shall keep the previous versions of the documents. | Mandatory | Correction & resubmission tracking |
| FR-05 | The system shall update and track the status of an application throughout the permit workflow. | Mandatory | Centralized application status tracking |
| FR-06 | The system shall allow authorized department officers to approve or reject an application only after all required reviews are completed. | Mandatory | Need for a controlled approval process |
| FR-07 | The system shall record permit fee and payment status associated with an application. | Mandatory | Need to track permit fee/payment information |
| FR-08 | The system shall allow building inspectors to record inspection details and inspection status. | Mandatory | Structured application assignment / inspection tracking |
| FR-09 | The system shall provide notifications to relevant users (in-app notifications and SMS) when important application events or status changes occur. | Mandatory | Transparent communication and visibility |
| FR-10 | The system shall maintain an audit trail of important actions performed on permit applications. | Mandatory | Accountability and traceability |
| FR-11 | The system shall provide analytical reports on permit applications, processing time, status, and workflow trends. | Challenge | Better visibility and reporting |

### 2.2 Non-Functional Requirements

| NFR ID | Description | Category | Measurable Target |
|---|---|---|---|
| NFR-01 | The system shall respond to normal user requests within an acceptable time under normal load. | Performance | 95% of requests receive a response within 3 seconds with up to 50 concurrent users. |
| NFR-02 | The system shall restrict access to functions and data based on the user's assigned role. | Security | 100% of protected functions require appropriate authorization. |
| NFR-03 | The system shall protect user authentication credentials and authenticated sessions. | Security | 100% of passwords securely hashed; sessions expire after 30 minutes of inactivity. |
| NFR-04 | The system shall provide a clear and consistent interface for users to perform permit-related tasks. | Usability | At least 90% of test users can submit a valid permit application within 5 minutes without technical assistance. |
| NFR-05 | The system shall preserve application and workflow records when individual operations fail. | Reliability | After an operation failure, recovery completes within 10 seconds without losing successfully saved records. |
| NFR-06 | The system shall maintain traceable records of important application activities. | Auditability | Every audit record contains 4 fields: user ID, action, date and timestamp. |
| NFR-07 | The system shall maintain data integrity between related application, review, payment and inspection records. | Data Integrity | A payment, review or inspection record cannot be saved unless its application ID exists in the database. |
| NFR-08 | The system shall deliver notifications promptly after key events. | Performance | In-app notifications appear within 5 seconds and SMS is sent within 60 seconds of the event. |

---

## 3. Use Cases / User Stories

### 3.1 Use Case Table

| ID | Actor | Description / User Story | Main Flow | Exception Flow |
|---|---|---|---|---|
| UC-01 | Admin | Manage users and their assigned roles. | Admin logs in → creates/updates user → assigns role → system saves authorization details. | Invalid role/user information → system rejects the operation and displays an error. |
| UC-02 | All users | Log in securely and access role-based features. | User enters credentials → system verifies → role dashboard is displayed. | Wrong credentials → error shown. 5 failed attempts → account locked. Session idle for 30 minutes → user logged out. |
| UC-03 | Applicant | Submit a building permit application with required details and documents. | Login → enter application details → upload documents → validate → submit → system generates application record. | Missing/invalid information → system displays errors → applicant corrects and resubmits. |
| UC-04 | Department Officer | Assign an application to a reviewer, zoning officer or inspector. | Officer logs in → opens submitted application → selects assignee → confirms → system records assignment. | Already assigned → system asks to confirm reassignment. Unauthorized user → access denied. |
| UC-05 | Permit Reviewer | Review a submitted permit application and its documents. | Reviewer logs in → views assigned application → checks details/documents → records review result. | Missing/invalid documents → reviewer requests corrections. |
| UC-06 | Zoning Officer | Perform zoning verification for an application. | Officer opens application → checks zoning-related information → records zoning decision. | Zoning information insufficient → application is sent for correction/review. |
| UC-07 | Applicant | Respond to correction requests and resubmit the application. | Applicant views correction request → makes corrections → uploads updated documents → resubmits. | Required correction not completed → system blocks resubmission and shows a message. |
| UC-08 | Applicant | Track the current status of a submitted permit application. | Login → view applications → select application → system displays current status and relevant updates. | Application not found or unauthorized access → system denies access and displays a message. |
| UC-09 | Senior Department Officer | Approve or reject an application after required reviews. | Officer reviews completed application → selects approve/reject → records decision → system updates status. | Required review incomplete → system prevents final decision. |
| UC-10 | Finance Officer | Record and update the payment status of a permit application. | Finance Officer opens application → views fee information → records payment status → system updates record. | Payment information invalid/incomplete → status remains Pending and the issue is recorded. |
| UC-11 | Building Inspector | Record the inspection result for an approved application. | Inspector opens assigned application → performs inspection → records details/result → system updates inspection status. | Inspection cannot be completed → inspector records the reason and reschedules / follows the next workflow step. |

### 3.2 Use Case Diagram

All role actors are specializations of a general "User" and log in through UC-02 (`<<include>>`). UC-09 (approve/reject) includes UC-05 (review) and UC-06 (zoning verification), so a final decision always follows those outcomes. UC-07 (respond to corrections & resubmit) `<<extend>>`s UC-03 (submit application) as an optional/conditional path.

![Use Case Diagram](S1_doc_media/use_case_diagram.png)

---

## 4. Acceptance Criteria

| Requirement | Acceptance Criteria | Test / Verification Method |
|---|---|---|
| FR-01 | Admin creates users with one role each. Users log in with valid credentials and see only their role's features. Other actions are denied. | Log in as each role and check the menus. Try a restricted action and confirm it is denied. Create a duplicate username and confirm it is rejected. |
| FR-02 | Submission works only when all mandatory fields and a document are given. The system creates a unique application ID and sets the status to "Submitted". | Submit a valid application and check the ID and status. Leave each mandatory field blank and confirm it is blocked. |
| FR-03 | Only a Department Officer or Admin can assign. The assignee must suit the current stage. The assignment is saved. Reassignment asks for confirmation. | Assign as an officer and check the assignee sees it. Try as an Applicant and confirm it is denied. Reassign and check the prompt appears. |
| FR-04 | Applicant can resubmit only after a correction request and after making the changes. The old version is kept and the status becomes "Resubmitted". | Request a correction, resubmit and check the status. Resubmit without changes and confirm it is blocked. |
| FR-05 | Every action updates the status to a defined value. Only valid transitions are allowed. Applicant sees the latest status. | Run the full workflow and check each status. Try an invalid jump (Submitted → Approved) and confirm it is blocked. |
| FR-06 | Approve/Reject is allowed only after the review and zoning checks are complete. Rejection needs a reason. The decision is added to the audit log. | Try to approve with zoning pending and confirm it is blocked. Complete all reviews, approve, and check the status and audit entry. Reject without a reason and confirm it is blocked. |
| FR-07 | Finance Officer records the fee, payment status and date. Invalid data keeps the status "Pending". | Save a valid payment and check it. Enter a negative amount and confirm the status stays Pending. Try as another role and confirm it is denied. |
| FR-08 | Inspector records the date, result (Pass / Fail / Could not complete) and remarks. A reason is required if not completed. | Record each result and check it is saved. Choose "Could not complete" with no reason and confirm it is blocked. |
| FR-09 | In-app and SMS notifications are sent to the right users for key events. Each one shows the application ID and event. | Trigger each event and check the right user gets both. Confirm unrelated users get none. |
| FR-10 | Every important action creates an audit record. Audit records cannot be edited or deleted. | Perform each action and check the audit entry. Try to edit or delete a record and confirm it is not possible. |
| FR-11 | Reports show counts by status, average processing time and monthly trend. They can be filtered by date and permit type. Only authorized roles can view them. | Load known test data and compare the report with manual counts. Apply a date filter. Try as an Applicant and confirm it is denied. |
| NFR-01 | 95% of requests respond within 3 seconds with 50 users. | Run a load test with 50 users and check the 95th percentile is ≤ 3 s. |
| NFR-02 | All protected functions need the right role. Wrong or missing access returns 401/403. | Call every protected endpoint with no token and with the wrong role. Confirm all are denied. |
| NFR-03 | Passwords are stored hashed. Sessions expire after 30 minutes idle. | Check the database for plain-text passwords. Stay idle for 30 minutes and confirm logout. |
| NFR-04 | 90% of test users submit a valid application within 5 minutes without help. | Time 10 users. At least 9 must finish within 5 minutes. |
| NFR-05 | After a failure, the system recovers within 10 seconds. Saved records stay intact. No partial records remain. | Stop the service mid-save and restart. Check recovery time and that no half-saved record exists. |
| NFR-06 | Every audit record has user ID, action, date and timestamp, with none empty. | Query the audit table and confirm no nulls in the 4 fields. |
| NFR-07 | Payment, review and inspection records are rejected if the application ID does not exist. | Insert each with a fake application ID and confirm an error. |
| NFR-08 | In-app notifications appear within 5 seconds. SMS is sent within 60 seconds. | Trigger 20 events and check at least 19 meet both limits. |

---

## 5. Priority Classification

| Requirement | Description | Priority | Justification |
|---|---|---|---|
| FR-01 | Create users, assign roles, authenticate and restrict actions by role. | Mandatory | Core of the project (RBAC). All other features depend on it. |
| FR-02 | Submit a permit application with details and documents, with validation. | Mandatory | Starting point of the workflow. Nothing else works without it. |
| FR-03 | Assign an application to a reviewer, zoning officer or inspector. | Mandatory | Needed so each application reaches the right officer. |
| FR-04 | Resubmit corrected applications and documents. | Mandatory | Completes the correction loop, a main pain point in S0. |
| FR-05 | Update and track application status through the workflow. | Mandatory | Solves the main S0 problem of no status visibility. |
| FR-06 | Approve or reject only after all required reviews are done. | Mandatory | Enforces a controlled approval process. |
| FR-07 | Record permit fee and payment status. | Mandatory | Payment is a required stage in the permit lifecycle. |
| FR-08 | Record inspection details and status. | Mandatory | Inspection is the final stage of the permit lifecycle. |
| FR-09 | Send in-app and SMS notifications for key events and status changes. | Mandatory | Keeps users informed and improves transparency. |
| FR-10 | Maintain an audit trail of important actions. | Mandatory | Needed for accountability and traceability. |
| FR-11 | Provide reports on applications, processing time, status and trends. | Challenge | Useful for analysis, but the workflow works without it. |
| NFR-01 | 95% of requests respond within 3 seconds with 50 users. | Challenge | Needs load testing. A target to improve after core features work. |
| NFR-02 | Restrict functions and data by assigned role. | Mandatory | Directly supports the RBAC objective. |
| NFR-03 | Hash passwords and expire sessions after 30 minutes idle. | Mandatory | Basic security needed to protect user accounts. |
| NFR-04 | 90% of test users submit an application within 5 minutes. | Mandatory | Checks that the system is easy to use. |
| NFR-05 | Recover within 10 seconds without losing saved records. | Mandatory | Prevents loss of application and workflow data. |
| NFR-06 | Audit records contain user ID, action, date and timestamp. | Mandatory | Makes the audit trail complete and useful. |
| NFR-07 | Reject records whose application ID does not exist. | Mandatory | Keeps application, payment, review and inspection data consistent. |
| NFR-08 | In-app notifications within 5 seconds and SMS within 60 seconds. | Challenge | SMS timing depends on an external service. |

---

## 6. Requirements Traceability Matrix

Each requirement is traced from its S0 source need to the owning engine, with design references to be added in later stages (S2–S4) and test cases defined for S6. All requirements are currently at status **Specified**.

| Req ID | Source Need (S0) | Owning Engine | Test Ref |
|---|---|---|---|
| FR-01 | RBAC & permission management | E1 Access Control & Security | TC-FR-01 |
| FR-02 | Role-based workflow coordination | E2 Permit Workflow & Decision | TC-FR-02 |
| FR-03 | Structured application assignment | E4 Assignment, Routing & Workload | TC-FR-03 |
| FR-04 | Correction & resubmission tracking | E2 Permit Workflow & Decision (document versions: E3) | TC-FR-04 |
| FR-05 | Centralized application status tracking | E2 Permit Workflow & Decision | TC-FR-05 |
| FR-06 | Controlled approval process | E2 Permit Workflow & Decision | TC-FR-06 |
| FR-07 | Permit fee and payment tracking | E2 Permit Workflow & Decision | TC-FR-07 |
| FR-08 | Inspection management and result tracking | E2 Permit Workflow & Decision | TC-FR-08 |
| FR-09 | Transparent communication and visibility | E2 Permit Workflow & Decision | TC-FR-09 |
| FR-10 | Accountability and traceability | E3 Transaction, Data & Audit Integrity | TC-FR-10 |
| FR-11 | Better visibility and reporting | E4 Assignment, Routing & Workload | TC-FR-11 |
| NFR-01 | Role-based workflow coordination (timely response) | E3 Transaction, Data & Audit Integrity | TC-NFR-01 |
| NFR-02 | RBAC & permission management | E1 Access Control & Security | TC-NFR-02 |
| NFR-03 | RBAC & permission management | E1 Access Control & Security | TC-NFR-03 |
| NFR-04 | Role-based workflow coordination (ease of use) | All engines | TC-NFR-04 |
| NFR-05 | Centralized application status tracking (reliable records) | E3 Transaction, Data & Audit Integrity | TC-NFR-05 |
| NFR-06 | Audit logs, notifications & monitoring | E3 Transaction, Data & Audit Integrity | TC-NFR-06 |
| NFR-07 | Centralized application status tracking (consistent records) | E3 Transaction, Data & Audit Integrity | TC-NFR-07 |
| NFR-08 | Audit logs, notifications & monitoring | E2 Permit Workflow & Decision | TC-NFR-08 |

---

## 7. Requirement Clustering

Related requirements are grouped by common technical responsibility (not by UI screen or frontend/backend layer).

| Cluster | Responsibility Area | Requirements | Common Technical Responsibility | Engine |
|---|---|---|---|---|
| CL-01 | Access control and session security | FR-01, NFR-02, NFR-03 | Verify identity, check role permissions on every request, hash passwords and expire idle sessions. | E1 |
| CL-02 | Workflow state and decision control | FR-02, FR-04, FR-05, FR-06 | Allow only valid stage transitions, require reviews before approval and manage the correction loop. | E2 |
| CL-03 | Stage records and workflow notifications | FR-07, FR-08, FR-09, NFR-08 | Record payment and inspection results against the current stage and notify users when events occur. | E2 |
| CL-04 | Data consistency, audit and recovery | FR-10, NFR-01, NFR-05, NFR-06, NFR-07 | Save related records atomically, enforce foreign keys, recover from failures and keep an append-only audit trail. | E3 |
| CL-05 | Assignment, routing and workload analytics | FR-03, FR-11 | Route applications by type, zone and workload, allow officer override and report on workload and processing time. | E4 |

---

## 8. Engine Decomposition Matrix

| | E1 — Access Control & Security | E2 — Permit Workflow & Decision | E3 — Transaction, Data & Audit Integrity | E4 — Assignment, Routing & Workload |
|---|---|---|---|---|
| **Clusters** | CL-01 | CL-02, CL-03 | CL-04 | CL-05 |
| **Primary responsibility** | Verify identity and allow only role-permitted actions on every request. | Control stage transitions and decisions, record stage results and notify users. | Keep related records consistent, recoverable and traceable. | Choose the right officer for each application and report on workload and processing time. |
| **Inputs** | Credentials, session token, user role, requested action. | Submitted application, review and zoning results, correction requests, payment and inspection details. | Save and update requests, document uploads, audit events. | Application type, zone, stage, officer workload, override request. |
| **Outputs** | Access granted or denied, session token, lockout status. | Updated status, correction request, approve/reject decision, notifications. | Saved or rolled-back result, document versions, audit records. | Assigned officer, reassignment record, workload and processing-time reports. |
| **State / data owned** | Users, roles, permissions, sessions, failed-login count. | Application status, review results, correction history, payment and inspection records. | Applications, documents and versions, payments, reviews, inspections, audit log. | Assignment records, officer workload counts, routing rules. |
| **Core mechanism** | Password hashing, token sessions, deny-by-default role checks, 30-minute idle expiry, lockout after 5 failed logins. | State machine with allowed transitions, review checks before approval, correction loop. | Atomic transactions with rollback, foreign-key constraints, locking for concurrent updates, document version numbers, append-only audit table. | Rule matching by type and zone, priority queue picks least-loaded eligible officer, officer override, aggregation of Chicago data. |
| **Dependencies** | Every engine calls E1 before acting. E3 stores the user data. | E1 for permission checks, E3 for saving data, E4 for the assigned officer. | E1 for user identity in audit records. Used by E2 and E4 to store data. Relational database. | E1 for override permission. E2 asks E4 for an assignee. E3 for data. |
| **Failure cases / recovery** | Wrong password gives an error. 5 failed logins lock the account. Expired or missing token gives 401/403. | Invalid stage jump blocked. Approval with pending reviews blocked. Resubmission without corrections blocked. Failed save rolled back by E3. | Failed save rolled back with no partial record. Invalid application ID rejected. Concurrent edit: second user gets a conflict message. Crash recovered on restart. | No eligible officer: application goes to an unassigned queue and an officer is alerted. Already assigned: confirmation before reassignment. Unauthorized override denied. |
| **Primary KPI** | 100% of protected functions require authorization. 100% of passwords hashed. Sessions expire after 30 min idle. | 100% of invalid transitions blocked. 0 approvals with incomplete reviews. In-app notification within 5 s, SMS within 60 s. | Recovery within 10 s with no lost records. 0 records with a missing application ID. 100% of audit records have all 4 fields. 95% of requests within 3 s at 50 users. | 100% of applications assigned to an eligible officer. Workload difference between officers within 2 applications in test data. Report figures match manual counts. |
| **Owner** | Akhil Teja | Annapurna Boratti | Amruta Kutri | Sanmathi Hegde |

---

## 9. Engine Description Sheets

### 9.1 Engine E1 — Access Control & Security Engine

**Owner:** Akhil Teja (01FE24BCS284) · **Requirements:** CL-01 — FR-01, NFR-02, NFR-03

**Purpose.** This engine is responsible for checking who a user is and what that user is allowed to do. It exists because a permit system has many roles, and each role must perform only its own actions. It solves the problem of unauthorized actions and insecure sessions by checking identity and role permission on every request. Passwords are stored hashed, sessions expire after inactivity and repeated failed logins lock the account. Every other engine depends on it before acting.

**Boundary**

| Primary Responsibility | Owns | Does NOT Own |
|---|---|---|
| Verify identity and allow only role-permitted actions on every request. | User accounts and role assignment, login and logout, password hashing, session tokens, role-permission checks, session expiry, account lockout. | Workflow stage decisions (E2), officer assignment (E4), data storage and audit records (E3), screen design. |

**Inputs, outputs and state**

| Inputs / Trigger | Outputs / Result | State / Data Owned |
|---|---|---|
| Username and password, user role, create/update user request from Admin. | Login success or failure, session token, user created with role, lockout status. | Users, roles, permissions, hashed passwords, failed-login count. |
| Session token and the requested action from any engine. | Access granted, or access denied (401/403). | Active sessions and their last-activity time. |

**Core mechanism**

| Mechanism / Rule | Why It Is Needed | Requirements |
|---|---|---|
| Deny-by-default role-permission check on every request. An action is allowed only if the role has that permission. | Stops users from doing actions outside their role. | FR-01, NFR-02 |
| Password hashing and token-based sessions that expire after 30 minutes of inactivity. | Protects stored credentials and closes unused sessions. | NFR-03 |
| Account lockout after 5 failed login attempts. | Prevents repeated password guessing. | FR-01, NFR-03 |

**Dependencies, failures and KPI**

| Interface / Dependency | Failure / Boundary Case | Handling / Recovery | KPI |
|---|---|---|---|
| E2, E3 and E4 call E1 before every protected action. | Missing, expired or invalid token, or wrong role. | Request denied with 401/403 and no data returned. User sent to login page. | 100% of protected functions require authorization (checked on every endpoint). |
| E3 saves user and role data. E1 supplies the user ID for audit records. | Wrong credentials, or 5 failed attempts. | An error is shown. After 5 attempts the account is locked until the Admin unlocks it. | 100% of stored passwords hashed. Account locks after 5 failed attempts. |
| Admin creates and updates users through E1. | Invalid role or duplicate user information (UC-01). | Operation rejected with an error; nothing saved. | Sessions expire after 30 minutes of inactivity. |

### 9.2 Engine E2 — Permit Workflow & Decision Engine

**Owner:** Annapurna Boratti (01FE24BCS283) · **Requirements:** CL-02 — FR-02, FR-04, FR-05, FR-06; CL-03 — FR-07, FR-08, FR-09, NFR-08

**Purpose.** This engine is responsible for moving a permit application through its stages in the correct order. It exists because many roles act on one application, and each step must happen only when the previous one is complete. It solves the problem of invalid stage jumps and inconsistent decisions. It allows only valid status changes, blocks approval until the required reviews are done, and manages the correction and resubmission loop. It also records payment and inspection results and notifies users when important events occur.

**Boundary**

| Primary Responsibility | Owns | Does NOT Own |
|---|---|---|
| Control stage transitions and decisions, record stage results and notify users. | Application submission and field validation, status transitions, review and zoning completion checks, correction requests and resubmission, approve/reject decision, payment status, inspection result, in-app and SMS notifications. | Login and permission checks (E1), saving data, constraints, audit records and document versions (E3), choosing the officer for an application (E4), workload reports (E4). |

**Inputs, outputs and state**

| Inputs / Trigger | Outputs / Result | State / Data Owned |
|---|---|---|
| Application details and documents, corrected applications, review and zoning results, correction requests. | Application accepted with a unique ID, updated status, correction request to the Applicant. | Application status, review results, correction and resubmission history. |
| Approve/reject decision, payment details, inspection details. | Final status (Approved or Rejected), updated payment status, updated inspection status. | Decision and reason, payment records, inspection records. |
| Any important event or status change. | In-app notification and SMS to the relevant users. | Notification status. |

**Core mechanism**

| Mechanism / Rule | Why It Is Needed | Requirements |
|---|---|---|
| Mandatory-field validation and a state machine with allowed status transitions. | Stops incomplete applications and invalid stage jumps. | FR-02, FR-05 |
| Prerequisite check: approval allowed only after review and zoning are complete. | No application is approved before all required reviews. | FR-06 |
| Correction loop: resubmission allowed only after corrections are made, and the application returns to review. | Handles rework without losing track of it. | FR-04 |
| Stage records and event-triggered notifications: payment and inspection results attach to the correct stage, and each status change sends a notification. | Keeps fee and inspection data on the right step and keeps users informed. | FR-07, FR-08, FR-09, NFR-08 |

**Dependencies, failures and KPI**

| Interface / Dependency | Failure / Boundary Case | Handling / Recovery | KPI |
|---|---|---|---|
| E1 checks the role before every action. E3 saves all changes. | Wrong role tries an action, or a save fails midway. | Action denied, or E3 rolls back. Status stays at the last valid stage. | 100% of invalid transitions blocked. 0 half-updated applications. |
| E4 supplies the assigned officer. | Approval with a review pending, or resubmission without corrections. | Action blocked and a message shown. | 0 approvals with incomplete reviews. |
| Notification service (in-app and SMS). | Invalid payment information, inspection not completed, or SMS unavailable. | Payment stays Pending, inspection reason is recorded, and the in-app notification is still sent. | In-app within 5 s and SMS within 60 s, for 95% of events. |

### 9.3 Engine E3 — Transaction, Data & Audit Integrity Engine

**Owner:** Amruta Kutri (01FE24BCS275) · **Requirements:** CL-04 — FR-10, NFR-01, NFR-05, NFR-06, NFR-07

**Purpose.** This engine is responsible for keeping all permit records consistent, recoverable and traceable. It exists because many users update related records, such as the application, review, payment and inspection, and a failure in the middle must not leave partial data. It solves the problem of incomplete or conflicting records by saving related changes as one unit, rejecting records that point to a missing application and handling simultaneous updates safely. It also keeps older document versions and records every important action in an audit trail that cannot be edited.

**Boundary**

| Primary Responsibility | Owns | Does NOT Own |
|---|---|---|
| Keep related records consistent, recoverable and traceable. | Atomic saving with rollback, foreign-key checks, safe concurrent updates, recovery after failure, document versions, append-only audit trail. | Role checks (E1), stage rules and decisions (E2), officer assignment and reports (E4), screen design. |

**Inputs, outputs and state**

| Inputs / Trigger | Outputs / Result | State / Data Owned |
|---|---|---|
| Save or update requests from E2 and E4, including application, review, payment and inspection records. | Saved record, or rolled-back result with an error. | Application, review, payment and inspection records. |
| Document uploads and resubmissions. | New document version stored, earlier versions kept. | Documents and their versions. |
| Important action events with the user ID from E1. | Audit record with user ID, action, date and timestamp. | Audit log. |

**Core mechanism**

| Mechanism / Rule | Why It Is Needed | Requirements |
|---|---|---|
| Atomic transactions with rollback and recovery on restart. | A failed save never leaves a partial record, and saved data survives a failure. | NFR-05 |
| Foreign-key checks and locking for concurrent updates. | Rejects records with a missing application ID and stops two users overwriting each other. | NFR-07 |
| Append-only audit records with 4 fields (user ID, action, date, timestamp), plus document version numbers. | Keeps a trace of every action and every document version. | FR-10, NFR-06, FR-04 |

**Dependencies, failures and KPI**

| Interface / Dependency | Failure / Boundary Case | Handling / Recovery | KPI |
|---|---|---|---|
| E2 and E4 send save requests. E1 supplies the user ID. | A save fails midway, or the system crashes. | Change rolled back; system recovers on restart with saved records intact. | Recovery within 10 s with no lost records. |
| E2 and E4 send records linked to an application. | Application ID does not exist, or two users edit the same record. | Save rejected with an error, or second user gets a conflict message. | 0 records saved without a valid application ID. |
| All engines send events to be audited. | An audit entry is missing a field, or someone tries to edit or delete it. | Entry rejected; audit records cannot be changed. | 100% of audit records have all 4 fields. 95% of requests within 3 s at 50 users. |

### 9.4 Engine E4 — Assignment, Routing & Workload Engine

**Owner:** Sanmathi Hegde (01FE24BCS269) · **Requirements:** CL-05 — FR-03, FR-11

**Purpose.** This engine is responsible for choosing the right officer for each application and reporting on workload and processing time. It exists because applications can stall when no one knows who should handle them, or when a few officers get all the work. It solves the problem of wrong or delayed assignment by matching each application to an eligible officer by type, zone and stage, and picking the one with the lowest workload. An officer with the right permission can override the choice, and an application left unreviewed too long is flagged. The engine also turns assignment and processing data into reports.

**Boundary**

| Primary Responsibility | Owns | Does NOT Own |
|---|---|---|
| Choose the right officer for each application and report on workload and processing time. | Routing rules by type and zone, workload-based assignment, officer override and reassignment, overdue flagging, workload and processing-time reports. | Application status and decisions (E2), role checks (E1), saving data and audit records (E3), notifications (E2). |

**Inputs, outputs and state**

| Inputs / Trigger | Outputs / Result | State / Data Owned |
|---|---|---|
| Request from E2 for an assignee, with application type, zone and stage. | Assigned officer, or an unassigned queue entry if none is eligible. | Assignment records and routing rules. |
| Override or reassignment request from a Department Officer or Admin. | Updated assignment with the change recorded. | Reassignment history and officer workload counts. |
| Report request, with date range or filters. | Workload and processing-time reports, and a flag for overdue applications. | Report results built from stored data. |

**Core mechanism**

| Mechanism / Rule | Why It Is Needed | Requirements |
|---|---|---|
| Rule matching by type, zone and stage to find eligible officers. | Applications reach an officer who can handle them. | FR-03 |
| Priority queue that picks the least-loaded eligible officer, with officer override. | Keeps workload even and still lets an officer correct the choice. | FR-03 |
| Aggregation of assignment and processing-time data, and a check for applications unreviewed past a set time. | Shows bottlenecks and finds stalled applications. | FR-11, FR-03 |

**Dependencies, failures and KPI**

| Interface / Dependency | Failure / Boundary Case | Handling / Recovery | KPI |
|---|---|---|---|
| E2 asks E4 for an assignee. E4 returns the officer and never changes the status. | No eligible officer is available. | Application goes to an unassigned queue and a Department Officer is alerted. | 100% of applications assigned to an eligible officer. |
| E1 checks permission for override. | Application already assigned (UC-04), or an unauthorized override. | System asks for confirmation before reassigning, or denies the override. | Workload difference between officers within 2 applications in test data. |
| E3 supplies and stores the data. | Missing data for a report. | Report shows the available data and marks the gap. | Report figures match manual counts. |