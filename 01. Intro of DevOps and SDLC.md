<div align="center">
  <h1>DevOps Zero to Hero: Notes</h1>
  <p>Technical breakdown of DevOps Fundamentals, SDLC, and Organization Workflow</p>
  <a href="https://github.com/Abhishek-Veeramalla/DevOps-Zero-To-Hero" target="_blank">
    <img src="https://img.shields.io/badge/Course-DevOps%20Zero%20to%20Hero-green?style=for-the-badge">
  </a>
</div>

---

<h2 id="day-1">Day 1: Fundamentals & The "Why" of DevOps</h2>

### 1. The Core Definition
DevOps is a **cultural practice** aimed at improving an organization’s ability to deliver applications rapidly. 
* **The "Four Pillars" (Technical Framework):**
    * **Automation:** Replacing manual workflows with scripts/tools.
    * **Quality Assurance:** Standardizing code and application quality.
    * **Monitoring/Observability:** The real-time visibility into production performance.
    * **Continuous Testing:** Validating code incrementally rather than waiting until the end.

### 2. Historical Evolution (The "Why")
* **The "Pre-DevOps" Era (10+ years ago):** Organizations operated in silos. A typical flow involved:
    1. **System Administrator:** Created the server (on VMware/OpenStack).
    2. **Build/Release Engineer:** Deployed code from a central repo (SVN/CVS) to an App Server.
    3. **Server Administrator:** Managed the app server configuration.
* **The Inefficiency:** This manual hand-off meant a single deployment could take days or weeks. DevOps emerged to unify these roles, enabling the **automation of the entire pipeline** and reducing delivery time from weeks to hours.

### 3. Professional Interview Guidance
* **Introduction Strategy:** Don't just list tools. Structure your introduction by stating:
    * Total DevOps experience.
    * Previous technical background (e.g., System Admin, Java/Python Developer).
    * Your role as an **efficiency driver** who uses the "Four Pillars" to eliminate manual intervention.
* **Note:** DevOps itself has only been mainstream for ~8 years; avoid claiming 10+ years of exclusive "DevOps" experience.

---

<h2 id="day-2">Day 2: The SDLC Process</h2>

### 1. The SDLC Standard
SDLC is the mandatory industry standard for designing, developing, and testing. Every organization follows a circular lifecycle for every feature launch.

* **Phases:**
    1. **Planning & Requirements:** Gathering customer feedback and assessing feasibility.
    2. **Definition & Design:** 
        * **HLD (High-Level Design):** Scalability, availability, database infrastructure.
        * **LLD (Low-Level Design):** Function logic, module interfaces, and specific code structures.
    3. **Building:** Coding (e.g., Python/Java) and Git-based collaboration.
    4. **Testing:** Validation by QE engineers (Quality Assurance).
    5. **Deployment:** Pushing the build to production.

### 2. The DevOps Engineering Domain
DevOps engineers are the **automation architects** of the SDLC.
* **Focus Area:** Building, Testing, and Deployment.
* **The Goal:** Achieving **Zero Manual Intervention**. You do not perform the testing or development manually; you write the *automation scripts* (CI/CD pipelines) that make these processes automatic, efficient, and error-free.

---

<h2 id="day-3">Day 3: Roles, Requirement Flow, and Jira</h2>

### 1. The Requirement Flow
1. **Business Analyst (BA):** Translates customer feedback into a **BRD** (Business Requirement Document).
2. **Product Manager (PM):** Prioritizes features based on market competition (e.g., deciding to build a "Kids Catalog").
3. **Product Owner (PO):** Converts vision into **Epics** and manages the technical backlog.
4. **Solutions Architect:** Provides the HLD/LLD blueprints for the development team.
5. **Scrum Team (Execution):** The cross-functional team (Devs, DevOps, QE, DBAs).

### 2. Jira and Sprint Management
* **Agile Sprints:** 2–3 week cycles of focused development.
* **Backlog Refinement:** A continuous process where new stories are added, estimated, and assigned.
* **Technical DevOps Tasks:** You don't just "do DevOps"; you work on specific tickets like:
    * *Infrastructure:* "Provisioning a Kubernetes cluster using Terraform."
    * *Configuration:* "Writing Dockerfiles for service X."
    * *Storage:* "Provisioning AWS RDS instances."
* **Accountability:** Jira is the **single source of truth**. As a DevOps engineer, you must update task comments daily so management can track bottlenecks (e.g., VPC issues, budget locks) across the entire team.
