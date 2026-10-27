# Civic Issue Reporting and Resolution Management System

**Data-Driven, Role-Based Workflow Management System**
Gate 0 / Stage S0 — Problem Definition & Need Identification

---

## 0. Project Details

| Item | Details |
|---|---|
| Team No. | 4 |
| Theme No. | 1 |
| Artefact Name | Civic Issue Reporting and Resolution Management System |
| Dataset | NYC 311 Open Data (NYC Open Data Portal) |
| Guide | Sunil V G |
| Department | Computer Science & Engineering |

**Team Members**

| Name | Roll No. |
|---|---|
| Sandeepgouda Goudar | 403 |
| Pavitra Adur | 408 |
| Akash Hugar | 409 |
| Lahari Banakar | 411 |

**Order of work (7 steps):** (1) The Problem → (2) Who Is Involved → (3) How It Works Today → (4) Problem & Goals → (5) What's Included → (6) Can We Do This → (7) What Could Go Wrong.

---

## 1. The Problem (Step 1 of 7)

### 1.1 Foundational Courses

| # | Course | Core Concepts |
|---|---|---|
| 1 | DSA | Priority queue for urgent complaints, hashing for duplicate detection, graphs/Dijkstra for route optimization |
| 2 | DBMS | Store citizens, complaints, departments, officers, locations and status history efficiently |
| 3 | Computer Networks | Client-server communication through HTTP/HTTPS, REST APIs |
| 4 | OOPS | Model entities such as Citizen, Officer, Complaint and Department as objects |
| 5 | Software Engineering | Requirement analysis, modular architecture, workflows, testing and maintainability |
| 6 | Web Technology | Role-based dashboards, complaint submission, authentication and responsive interfaces |

### 1.2 Existing Problem / Current Situation

Civic issues such as garbage accumulation, noise, illegal parking, damaged roads, water leakage and streetlight failures are continuously reported by citizens. Existing channels mainly focus on *collecting* complaints, but reporting an issue does not ensure timely or efficient resolution.

- Citizens report through multiple channels (phone calls, websites, mobile platforms).
- Complaints are handled separately by different departments, making coordination difficult.
- Manual classification and assignment can lead to delays or incorrect routing.
- All complaints may get the same priority even when severity and impact differ.
- Repeated complaints about the same issue create duplicate work.
- Citizens have limited visibility into progress and expected resolution time.
- Authorities lack a unified view of hotspots, department workload and SLA delays.
- As volume grows, manual monitoring and resource allocation become difficult.

### 1.3 Who Is Affected?

- **Citizens** – difficulty reporting issues, tracking complaints and getting timely resolution.
- **Field Officers** – receive complaints without effective prioritization, so it is hard to know what needs immediate attention.
- **Government Departments** – high complaint volumes, workload imbalance and inefficient manual assignment.
- **Supervisors** – difficulty monitoring pending complaints, SLA breaches and officer performance.
- **Municipal Administration** – lacks a unified view of hotspots, recurring issues and overall service performance.

### 1.4 Pain Points

- **Complaint overload** – growing numbers and varieties of complaints make manual management difficult.
- **No effective prioritization** – not every complaint has the same urgency or impact.
- **Delayed resolution** – complaints may go unattended without deadline monitoring and escalation.
- **Duplicate complaints** – repeated complaints about the same issue add unnecessary workload.
- **Lack of visibility** – authorities need better visibility into workload, hotspots, recurring issues and resolution performance.

### 1.5 Why the Existing Approach Is Inadequate

- Manual classification can cause incorrect or delayed department assignment.
- Complaints are treated alike, without prioritization by severity, public impact or urgency.
- Repeated complaints are handled as separate cases.
- Manual assignment ignores officer workload, availability or proximity.
- Limited SLA-based monitoring makes it hard to spot complaints at risk of delay.
- Citizens lack transparent, real-time visibility into the resolution process.
- Authorities lack a unified view of hotspots, recurring issues and department workload.
- Increasing volumes make manual monitoring and resource allocation inefficient.

### 1.6 Evidence That This Problem Is Real

Analysis of 10,000 complaints from the NYC 311 dataset:

- **42.7%** of complaints were noise-related — strong concentration in specific issue categories.
- **Brooklyn** accounted for about **31%** of all complaints — geographic concentration.
- Complaint volume rose in the late evening, with **22:00** the peak hour.
- Workload varied greatly between departments — need for better workload management.
- About **34.9%** of records had no recorded closure date — need to track unresolved complaints.
- Multiple complaints occur around the same issue type/location — need for duplicate / recurring-issue detection.

**Takeaway:** civic complaints are not uniformly distributed. They concentrate by issue type, location and time, while unresolved cases and uneven departmental workloads create a need for intelligent prioritization, assignment and monitoring.

### 1.7 Sources / References

- NYC 311 Open Data and NYC Open Data Portal — real-world complaint patterns, categories, locations and resolution status.
- Existing 311 civic complaint systems — reviewed for current reporting and tracking workflows.
- Stakeholder discussions — inputs from students/citizens on difficulties in reporting and tracking issues.
- Academic references — DBMS, DSA, Computer Networks and Software Engineering concepts behind the proposed workflow.

---

## 2. Who Is Involved? (Step 2 of 7)

### 2.1 Stakeholder Table

| Stakeholder | Role / Description | Needs & Expectations | Current Pain Points | Influence |
|---|---|---|---|---|
| **Citizens** | Report civic issues, upload evidence, track status and receive updates | Easy reporting, evidence upload, status tracking and timely updates | Delayed resolution and limited transparency | H |
| **Field Officers** | Receive prioritized tasks, view location, update progress and resolve issues | Correctly prioritized tasks, location information, efficient task handling, easy progress updates | Inefficient task assignment and resource allocation | H |
| **Department Officials** | Manage complaints, allocate resources and monitor department workload | Efficient complaint management, resource allocation and workload monitoring | Manual management, workload issues, inefficient resource allocation | H |
| **Supervisors** | Monitor SLA, identify delayed issues, reassign tasks and handle escalations | SLA monitoring, identification of delays, reassignment and escalation management | Delayed issues and difficulty managing escalations | H |
| **Government / Administration** | Analyse civic trends, identify hotspots and make data-driven resource decisions | Accurate data, trend analysis, hotspot identification, better resource decisions | Limited data-driven decision making and inefficient resource allocation | H |
| **Admin** | Manage users, roles, departments, permissions and system configuration | Effective user/role management, permissions and configuration | Difficulty managing roles, departments and configuration | H |

### 2.2 Primary vs. Secondary Stakeholders

| Primary (directly use / affected) | Secondary (indirectly involved) |
|---|---|
| Citizens – report issues and track resolution | Government / Municipal Administration – policy and resource planning |
| Field Officers – receive and resolve assigned issues | Data / Analytics Teams – analyze trends and civic hotspots |
| Department Officials – manage complaints and workload | Oversight / Regulatory Bodies – monitor service performance and accountability |
| Supervisors – monitor SLA, progress and escalations | |
| System Administrators – manage users, roles and configuration | |

### 2.3 Key Insight Summary

The system must primarily prioritize **citizens by making civic issue reporting simple, transparent and easy to track**. Field officers and department officials need intelligent prioritization, clear task assignment and workload visibility. Supervisors require SLA monitoring, escalation mechanisms and performance insights to prevent delays. Government administrators and oversight bodies need reliable analytics to identify hotspots, allocate resources and improve overall civic service delivery.

---

## 3. How It Works Today (Step 3 of 7)

### 3.1 Current Process

A citizen identifies a civic issue and reports it through an available channel such as a website or mobile application. The complaint is recorded and reviewed, then categorized and forwarded to the concerned department. The department assigns it to an officer or field worker, who investigates and carries out the required action. The status is updated and checked by a supervisor; once the issue is considered resolved, the case is closed and the citizen may receive a notification.

### 3.2 Step-by-Step Workflow Table

| Step | Actor / Role | Action Performed | Tool / System Used | Pain Point Observed |
|---|---|---|---|---|
| 1 | Citizen | Reports a civic issue (garbage, noise, illegal parking, damaged roads, water leakage, streetlight failure) | Civic issue reporting system | Complaints may not be efficiently resolved after reporting |
| 2 | Citizen | Uploads evidence and provides complaint details | Complaint submission interface | Existing systems mainly focus on collecting complaints |
| 3 | System | Analyzes the complaint and determines priority from severity, impact, urgency and historical patterns | Data-driven prioritization / priority queue | Manual prioritization causes delays and incorrect priorities |
| 4 | System / Department Official | Routes the complaint to the appropriate department | Role-based workflow system | Incorrect or inefficient task assignment |
| 5 | Department Official | Allocates the task to a field officer based on resource availability | Department management system | Inefficient resource allocation and workload management |
| 6 | Field Officer | Receives the prioritized task and views the issue location | Officer dashboard / location system | Officers may not receive efficiently prioritized tasks |
| 7 | Field Officer | Works on the issue and updates its progress | Workflow / status tracking system | Difficulty monitoring complaint progress |
| 8 | Supervisor | Monitors SLA and identifies delayed complaints | SLA monitoring system | Delayed issues may not be identified quickly |
| 9 | Supervisor | Reassigns delayed tasks and handles escalations | Escalation / workflow system | Lack of integrated escalation management |
| 10 | Citizen | Tracks complaint status and receives updates | Complaint tracking interface | Limited transparency for citizens |
| 11 | Government / Administration | Analyzes complaint trends and identifies hotspots | Data analytics / reporting system | Limited data-driven decision making |
| 12 | Government / Administration | Uses insights for resource and operational decisions | Analytics dashboard | Difficulty making effective resource-allocation decisions |

### 3.3 Workflow Diagram

![Workflow diagram](S0_doc_media/civic_as_is_workflow.jpg)

Flow: Citizen → Report Complaint → Validate Data → ML Classification (Category, Location) → Priority Engine (Severity, SLA, Hotspot) → Priority Score → Priority Queue → Department Routing → Role-Based Assignment → Field Officer → Resolve / Escalate → Supervisor → Verify → Citizen → Close.

### 3.4 Bottlenecks & Inefficiencies Identified

1. **Manual classification & routing** — complaint → manual review → department assignment causes delays and routing errors.
2. **Inefficient assignment** — officers receive work without regard to workload, skills or proximity.
3. **Limited visibility & analytics** — citizens lack transparent tracking; authorities lack a unified view of hotspots, backlog and workload.

---

## 4. Problem & Goals (Step 4 of 7)

### 4.1 Observed Problems → Underlying Needs

| # | Observed Problem | Evidence / Source | Underlying Need | Linked Stakeholder(s) |
|---|---|---|---|---|
| 1 | Complaints are manually classified and assigned | Current civic complaint workflow | Automatic classification and department assignment | Citizens, Department Officials |
| 2 | Urgent complaints may not be handled first | Different complaints have different severity and impact | Priority-based complaint handling | Citizens, Field Officers, Supervisors |
| 3 | Duplicate/repeated complaints increase workload | Multiple complaints can refer to the same issue/location | Duplicate detection and complaint grouping | Department Officials, Field Officers |
| 4 | Delayed complaints are difficult to monitor | Lack of effective SLA tracking | SLA monitoring and automatic escalation | Supervisors, Department Officials |
| 5 | Citizens have limited visibility into progress | Status updates may not be centralized | Real-time complaint tracking and transparency | Citizens, Officers |
| 6 | Hotspots and workload are difficult to identify | Dataset shows geographic and departmental concentration | Analytics for hotspots, workload and resource planning | Government, Supervisors |

### 4.2 Prioritization

| Priority | Need | Justification |
|---|---|---|
| 1 | Intelligent prioritization | Urgent and high-impact issues should be handled first instead of treating every complaint equally. |
| 2 | SLA monitoring & escalation | Prevents complaints exceeding resolution deadlines and ensures delayed cases get attention. |
| 3 | Correct department & officer assignment | Complaints reach the appropriate team quickly, reducing response delays. |
| 4 | Workload & resource management | Distributes complaints among departments/officers and avoids overloading teams. |
| 5 | Location & hotspot analysis | Identifies recurring/high-volume areas and supports resource planning. |
| 6 | Citizen tracking & transparency | Keeps citizens informed and improves trust in the system. |
| 7 | Duplicate/repeated complaint detection | Reduces redundant work by identifying complaints on the same issue. |

### 4.3 Problem Statement

Citizens report a wide range of civic issues every day, but as complaint volume grows it becomes difficult to determine which issues need immediate attention, which department or personnel should handle them, and which complaints are approaching delayed resolution. This can lead to critical issues being overlooked, repeated complaints creating additional workload, and resources being distributed inefficiently. The computing challenge is to manage this continuous flow of diverse civic complaints in a way that reflects their urgency, impact, location, responsibility and time sensitivity.

*Formal statement:* "To develop a role-based civic issue management system that intelligently prioritizes complaints based on severity, impact and urgency, assigns them to appropriate departments/personnel, monitors SLAs and escalations, and tracks the complete complaint lifecycle for efficient and timely resolution."

### 4.4 Project Objectives

1. Prioritize complaints based on severity, public impact, complaint age, location and time sensitivity.
2. Route complaints to the appropriate department and assign them to suitable personnel based on responsibility and workload.
3. Provide role-specific dashboards and analytics that improve transparency for citizens and support data-driven decisions by officers and administrators.
4. Monitor complaint progress and resolution deadlines, with escalation of cases that remain unattended.

---

## 5. What's Included (Step 5 of 7)

### 5.1 Proposed Solution & Technical Workflow

Citizens report an issue with description, category, photo and location. The system validates the data, classifies the complaint (category and location), and a **priority engine** computes a score from severity, SLA time urgency and hotspot factors. Complaints enter a priority queue, are routed to the correct department, and assigned to a field officer. The officer accepts and resolves (or escalates if unresolved); the supervisor monitors, escalates and verifies; the citizen receives updates and the case is closed.

![Technical workflow, part 1](S0_doc_media/civic_to_be_part1.png)

![Technical workflow, part 2](S0_doc_media/civic_to_be_part2.png)

### 5.2 Applications

- Municipal Corporations — garbage, road, drainage and water-related issues.
- Public Utilities — streetlight and electricity complaints.
- Traffic Management — illegal parking and road-related traffic issues.
- Water & Sanitation Departments — water leakage, drainage and waste management.
- Public Works Departments — potholes, damaged roads and public infrastructure.
- Government Administration — hotspot analysis and resource planning.
- Smart City Operations — centralized monitoring and data-driven decisions.

### 5.3 In-Scope

| # | In-Scope Item |
|---|---|
| 1 | User registration, login and role-based authentication |
| 2 | Citizen complaint reporting with description, category, photo and location |
| 3 | Automatic complaint classification and department identification |
| 4 | Priority score calculation using severity, impact, complaint age, SLA and hotspot factors |
| 5 | Priority queue / max heap for handling high-priority complaints first |
| 6 | Complaint status tracking: Submitted → Assigned → In Progress → Resolved → Closed |
| 7 | Supervisor dashboard for monitoring complaints, workload and escalations |
| 8 | Citizen notifications and resolution verification |
| 9 | Duplicate/repeated complaint identification based on category and location |
| 10 | Analytics for workload, trends and hotspots |

### 5.4 Out-of-Scope

| # | Out-of-Scope Item | Reason for Exclusion |
|---|---|---|
| 1 | Physical execution of civic work | The system manages and tracks complaints; it does not repair roads, fix leaks, collect garbage, etc. |
| 2 | Emergency services / real-time emergency response | Focus is routine civic complaints and workflow management. |
| 3 | Financial transactions or payments | Payment processing and financial management are not part of the scope. |
| 4 | Government policy making | The system provides insights for decisions; it does not create policy. |
| 5 | Procurement and inventory management | Resource allocation is handled, but not purchasing materials or inventory. |
| 6 | External social-media complaint management | The system uses its own complaint workflow, not external platforms. |
| 7 | Automatic physical monitoring (CCTV, drones, IoT) | Reporting is complaint-based; no automatic issue detection. |
| 8 | Non-civic complaints | Intended only for civic issues (garbage, noise, illegal parking, damaged roads, water leakage, streetlight failures). |
| 9 | Direct control of municipal infrastructure; integration with external government systems; advanced predictive forecasting | Beyond the project's technical and access constraints. |

### 5.5 Assumptions

- Citizens have a smartphone or web-enabled device and an internet connection.
- Users provide reasonably accurate information, including issue description and location.
- Each civic issue can be associated with a responsible department or service category.
- Departments have predefined roles, responsibilities and resolution time targets (SLA).
- Officers update complaint status as work progresses.
- Administrators manage users, departments, roles and system configuration.
- The system has access to complaint data with category, location, status and timestamps.

### 5.6 Constraints

- Limited team size and development time.
- Limited availability of historical complaint data.
- Technology and infrastructure limitations.
- Dependence on accurate user-provided complaint information.
- Limited real-time information, system scalability and algorithm complexity.
- Dependence on user participation.

---

## 6. Can We Do This? (Step 6 of 7)

### 6.1 Technical Feasibility — Feasible

| Aspect | Assessment | Justification |
|---|---|---|
| Frontend | Feasible | React / HTML / CSS / JavaScript can build separate dashboards for citizens, officers, supervisors and administrators. |
| Backend | Feasible | Node.js with Express can provide REST APIs for complaints, users, departments, assignments and status updates. |
| Database | Feasible | MySQL/PostgreSQL can store users, complaints, departments, locations and status history. |
| Authentication & RBAC | Feasible | JWT-based authentication and role-based access control restrict features by role. |
| Complaint Classification | Feasible | Rule-based classification can be implemented initially. |
| Priority Engine | Feasible | A weighted scoring algorithm can compute priority from severity, impact, age, SLA and hotspot factors. |
| DSA Implementation | Feasible | Priority queue/max heap, hash maps, sorting and graph algorithms are implementable in standard languages. |
| Location Services | Feasible | A Maps API and browser geolocation can capture and visualize complaint locations. |
| Route Optimization | Feasible | Dijkstra/2-Opt for a limited number of complaints; large-scale optimization is future scope. |
| Real-Time Updates | Feasible | WebSockets can provide live status updates and notifications. |

### 6.2 Operational Feasibility — Feasible

- **Citizen adoption** — simple interface with description, photo and location.
- **Ease of use** — simple dashboards and clear workflows need minimal training.
- **Role-based access** — each stakeholder sees only role-relevant features.
- **Department workflow** — complaints are automatically classified and routed.
- **Officer usage** — officers see assigned complaints, priority, location and required action.
- **Supervisor monitoring** — pending complaints, workload, SLA deadlines and escalations are visible.
- **Citizen tracking** — status from submission to resolution with updates.
- **Reduced manual work and accountability** — automation plus status history shows who handled what and when.
- **Scalability** — start with one department or local area, then expand.

### 6.3 Time Feasibility — Feasible (15 weeks)

| Phase | Duration |
|---|---|
| Requirement analysis & problem definition | 1–2 weeks |
| System design & database design | 2 weeks |
| Frontend development | 3 weeks |
| Backend & database development | 3 weeks |
| Priority, assignment, duplicate detection & workflow features | 2 weeks |
| Testing & bug fixing | 2 weeks |
| Integration, documentation & final presentation | 1 week |

The four-member team can split work across analysis, design, frontend, backend, database, testing and documentation. The core complaint workflow is built first; duplicate detection, route optimization and analytics follow in the remaining time.

### 6.4 Resource Feasibility — Feasible

- **Team:** 4 members can divide frontend, backend, database, UI/UX and algorithm work.
- **Hardware:** standard laptops/desktops with internet.
- **Data:** civic complaint datasets for analysis, testing and developing prioritization/hotspot algorithms.
- **Software:** open-source React, Node.js/Express, PostgreSQL/MySQL and Python.
- **APIs:** mapping/location services for geolocation and route planning.
- **Skills:** web development, DBMS, DSA, Computer Networks and basic data analytics.

### 6.5 Economic Feasibility — Feasible

Low-cost: open-source technologies, public datasets and freely available development tools.

### 6.6 Overall Feasibility Conclusion — GO WITH MODIFICATIONS

Core features — complaint reporting, role-based access, database management, priority scoring, department assignment, SLA tracking and dashboards — are feasible with available technologies and team skills. Advanced features such as ML-based classification, large-scale route optimization and predictive analytics should be built incrementally or kept as future enhancements to avoid excessive complexity.

---

## 7. What Could Go Wrong (Step 7 of 7)

### 7.1 Project-Level Risks

| Risk ID | Risk Description | Category | Likelihood | Impact | Mitigation Strategy |
|---|---|---|---|---|---|
| R1 | Difficulty integrating multiple modules (reporting, prioritization, maps, dashboards) | Technical | M | H | Develop and test modules independently before integration |
| R2 | Inaccurate complaint classification or priority scoring | Technical | M | H | Start with rule-based logic; validate using historical complaint data; transparent scoring with supervisor override |
| R3 | Inaccurate or unavailable location data | Technical | M | M | Let users confirm or manually adjust the reported location |
| R4 | Limited or incomplete civic complaint data | Data | M | H | Use available public datasets; design for missing fields |
| R5 | Scope grows too large (AI, routing, analytics, multiple roles) | Scope | H | H | Define MVP first; add advanced features incrementally |
| R6 | Uneven technical skills across team members | Resource | M | M | Divide modules by skill; regular knowledge sharing |
| R7 | Integration or development takes longer than planned | Timeline | M | H | Follow milestones, prioritize core features, keep a testing buffer |
| R8 | Security or unauthorized access to role-specific functions | Security | M | H | Authentication, role-based access control and backend authorization |

Additional risks noted: duplicate/spam complaints (duplicate detection + verification), wrong assignment (department mapping + reassignment), officer overload (workload-aware assignment), poor internet connectivity (R9) and performance/scalability issues (R10).

### 7.2 Risk Owner Summary

| Risk ID | Risk | Risk Owner |
|---|---|---|
| R1 | Technical integration of multiple modules | Backend / Integration Lead |
| R2 | Incorrect classification or priority scoring | DSA / Algorithm Lead |
| R3 | Inaccurate or unavailable location data | Frontend / Maps Lead |
| R4 | Limited or incomplete complaint data | Data / DBMS Lead |
| R5 | Scope becoming too large | Project Lead |
| R6 | Uneven team skills / resource constraints | Project Lead |
| R7 | Development taking longer than planned | Project Lead |
| R8 | Security / unauthorized access | Backend / Security Lead |
| R9 | Poor internet connectivity | Frontend / Backend Lead |
| R10 | Performance and scalability issues | Backend / Database Lead |

---

## 8. Success Criteria

- **Fast complaint reporting** — citizens submit issues quickly with complete details and location.
- **Accurate prioritization** — high-severity, time-critical complaints rank ahead of lower-priority ones.
- **Correct assignment** — complaints reach the appropriate department and field officer.
- **Reduced response delay** — SLA monitoring flags delayed complaints and triggers escalation.
- **Effective workload management** — tasks distributed by officer availability and workload.
- **Reduced duplicate work** — repeated complaints about the same issue are detected and linked.
- **Complete transparency** — citizens track status through the whole lifecycle.
- **Successful resolution** — officers resolve issues and supervisors verify closure.

---