# 📋 Plans and Procedures

Each organization typically maintains its own specific set of plans and procedures. These are commonly well-documented to ensure that every employee has access to the most current information whenever it is required.

The primary purpose of creating plans and procedures is to ensure that every employee follows a **standard set of rules or guidelines**. These guidelines are used to achieve a common goal or meet a specific objective.

  * **Consistency:** If every employee used their own unique method to complete the same task, only a portion of the workforce might achieve the objective, while others might fail.
  * **Efficiency:** Without standard procedures, some employees might complete a task very quickly, while others might take a significant amount of time.

Therefore, establishing a standard set of plans and procedures that are shared with all employees helps ensure that everyone follows the same guidelines to complete tasks and achieve the same goals. These procedures are usually tested to verify that they represent the most efficient method for achieving a specific goal.

> **⚠️ Important Note:** As an organization grows and the IT team implements new technologies to support user demand, plans and procedures must be updated. This ensures employees remain aware of the most efficient methods for meeting objectives.

In this section, we will explore common plans and procedures, including **Change Management**, **Incident Response**, **Disaster Recovery**, **Business Continuity**, and the necessity of **Standard Operating Procedures (SOPs)**.


# 🔄 Change Management

**Change Management** focuses on ensuring that any change made is beneficial to the organization. It ensures the change is applied as efficiently and effectively as possible, while minimizing the impact on users during and after the implementation.

Before any technical or non-technical change is implemented, it must go through a complete life cycle. This ensures that all procedures are thoroughly followed by the staff implementing the change.

### 🛑 The Change Management Board

Crucially, the change must be approved by the **Change Management Board**. Their responsibilities include:

1.  **Reading and Determining Efficiency:** They carefully review the plan to determine if the procedures are efficient.
2.  **Verifying Skills:** They ensure that the staff performing the change have the correct set of skills and qualifications.
3.  **Assessing Impact:** They confirm that the impact of the change is minimal.
4.  **Contingency Planning:** They ensure there is a plan to **roll back** the change if the implementation does not go as planned.
5.  **Resource Availability:** They ensure standby staff are available to assist if the primary staff cannot continue or need to roll back the change.

### 📉 Evaluating User Impact

Changes must be carefully evaluated to determine exactly what is changing and how it will affect users.

**Example Scenario: The Microsoft Office Upgrade**
Imagine the IT staff upgrades the version of the Microsoft Office suite on everyone’s computer over the weekend.

  * **Tech-Savvy Users:** They will adapt to the new interface quickly and continue working.
  * **Non-Tech-Savvy Users:** They may find it difficult to adapt to the new interface and perform tasks without prior training.
  * **Result:** For affected users, productivity decreases, and tasks take longer to complete until they adapt.

**The Better Approach**
What if the IT staff created training videos and user-friendly, step-by-step documentation and distributed them *before* the change?

  * This helps employees transition smoothly from the old interface to the new one.
  * It helps users understand exactly what has changed.
  * Additionally, IT staff can **roll out the change in phases** (e.g., one department at a time). This allows them to monitor the process and gather user feedback, which can improve the implementation for future departments.

### 📝 Phases of Change Management

The following are the typical phases involved in change management:

1.  **Request:** Requesting to implement a specific change within the organization.
2.  **Evaluate:** Determining whether the change is actually needed to improve business processes.
3.  **Authorize:** Gaining official authorization from the change advisory board *before* making the change.
4.  **Implement:** The change owner (the person performing the change) executes the change within the organization.
5.  **Documentation:** Documenting every detail regarding the change for future reference.

### 🔙 Rollback and Remediation

Things may not always go according to plan. Having a **rollback or remediation plan** allows IT professionals to reverse a change if unforeseen problems occur.

**Example:**
You are upgrading the operating system on a core network switch. During the process, the switch freezes and stops responding to commands.

  * **Without a Plan:** You will spend a massive amount of time troubleshooting to restore the switch.
  * **With a Plan:** You can execute the pre-defined rollback steps to restore the switch to its previous working state quickly.

> **💡 Professional Insight:** As an aspiring IT professional, remember that not everyone sees technology the way you do. They cannot adapt as quickly. Change management helps reduce network downtime and organizational risk. Ideally, a change must be beneficial without creating new issues for the company.


# 🚨 Incident Response Plans

The field of cybersecurity is highly demanding. New vulnerabilities are discovered daily, and professionals work continuously to implement controls to mitigate risks from threat actors. Within this industry, **Incident Responders** are in high demand.

  * **Role:** Incident response professionals are responsible for containing threats and recovering from cyber-attacks.
  * **Goal:** They help the organization prevent and recover from real-world attacks.

Every organization needs an **Incident Response Plan**. This is a set of procedures and tools used by the cybersecurity team to efficiently:

1.  **Identify**
2.  **Contain**
3.  **Recover**

This plan helps organizations adapt to the changing security landscape and respond to threats using a **uniform, systematic approach**.

### 📄 Documentation and Patterns

It is critical to document and track all incidents that occur. Proper documentation helps professionals determine if similar incidents have happened in the past and what actions were taken.

**What to Record:**

  * Detailed description of the incident.
  * Time and date.
  * Location.
  * Persons involved.
  * Actions taken to resolve the issue.
  * Lessons learned.

Keeping these records helps security professionals identify patterns in past incidents.

### 👥 The Incident Response Team

When an incident occurs, the right people must be involved.

  * **Dedicated Team:** The organization may have a specific team trained to resolve security incidents.
  * **IT Management/Technical Staff:** These members may be involved in remediation.
  * **Escalation:** If a technical staff member cannot resolve the issue, it must be escalated to a senior expert.
  * **Cyber-Incident Response Team (CIRT):** Some companies maintain a CIRT responsible for monitoring, analyzing, responding to, and reporting all security incidents.

### 🧪 Testing the Plan

Designing a plan is not enough; it must be **tested regularly** (e.g., a few times per year).

  * Testing should be scheduled and conducted *before* a real incident occurs.
  * The outcome of the test must be documented.
  * Areas for improvement should be identified and re-tested.

Continuous testing ensures professionals are prepared for real cyber-attacks and makes the plan more effective.


### 🔄 The Incident Handling Process (NIST)

According to the **NIST SP 800-61 Rev. 2** (Computer Security Incident Handling Guide), there are four distinct phases of incident handling.

The following diagram illustrates the NIST incident response and handling model:

<div align="center">
  <img src="./images/01.png" width="400"/>

  Figure 12.1 – The incident handling process
</div>


**Explanation of the Figure:**

### 1\. Preparation 🛠️

This phase focuses on gathering a list of all assets within the organization. An **asset** is anything of value to the company.

  * **Tangible Assets:** Physical objects like networking devices and servers.
  * **Intangible Assets:** Digital objects like data, license keys, policies, business processes, and intellectual property.
  * **People:** Employees and staff.

During preparation, professionals must create a **baseline** of network performance under normal conditions. This helps distinguish normal traffic from abnormal traffic. A communication plan must also be developed to outline who to contact during an incident.

### 2\. Detection and Analysis 🔍

The team must be trained to identify security events efficiently.

  * **Event:** Any action on a system (e.g., a user logging in).
  * **Incident:** A security event indicating a system has been compromised by a threat.

Professionals must distinguish between harmless events and actual incidents. They collect as much information as possible to analyze the threat and determine how it entered the system. Security appliances are used to monitor systems in real-time.

### 3\. Containment, Eradication, and Recovery 🛑

  * **Containment:** Stop the threat from spreading (e.g., preventing malware from infecting other systems).
  * **Eradication:** Remove the threat completely. This involves disinfecting systems and verifying that no traces of the threat remain.
  * **Recovery:** Restore systems to an acceptable working state. This includes recovering data from backups, replacing compromised systems, and re-installing operating systems and applications.

### 4\. Post-Incident Analysis 📚

After resolution, the team analyzes the event to learn from the experience. These "lessons learned" improve the incident response plan and the team's future preparedness.


# 💼 Business Continuity Plan (BCP)

The **Business Continuity Plan (BCP)** is a set of guidelines used to restore an organization's services and functions after a disaster. It relies on a **Business Impact Analysis (BIA)** to identify critical processes and resources needed for operation.

### 📊 Availability Metrics

Organizations use metrics to measure system availability. For example, cloud providers often advertise availability as **99.999%** annually. The more "9s" included, the higher the guaranteed uptime.

### 🔑 Key Factors in BCP

  * **Tabletop Exercises:** A cost-effective method where staff discuss a simulated disaster scenario rather than physically acting it out.
  * **After-Action Reports:** A required report after any exercise detailing what worked smoothly and what did not.
  * **Failover:** Having an alternative site ready for migration. Data must be fully synchronized between the main site and the failover site.
  * **Alternative Business Practices:** Documentation of manual or secondary methods to achieve tasks if primary technology (like networks or printers) fails.


# 🌪️ Disaster Recovery Plans (DRP)

**Disaster Recovery Planning** ensures an organization is equipped to recover from risks to its resources and assets. This involves a dedicated team and up-to-date documentation of infrastructure.

> **ℹ️ Important Note**
>
> The NIST SP 800-34 Rev. 1 *Contingency Planning Guide for Federal Information Systems* is a key resource for DRP standards.

### 🗝️ Key Terms

  * **Recovery Time Objective (RTO):** The maximum time a system can be unavailable before the impact becomes unacceptable.
  * **Recovery Point Objective (RPO):** The point in time to which data must be recovered (i.e., how much data loss is acceptable) after an outage.

Effective DRP requires identifying internal and external support teams, documenting key assets/vendors, and identifying redundancy hardware. Continuous training and testing reveal gaps in the plan.


# ⏳ The System Life Cycle

The **System Life Cycle** defines the lifespan of a technology supported by a vendor. Using **End-of-Life (EOL)** systems increases security risks because vendors no longer provide updates or patches for vulnerabilities.

### 🔄 Phases of the Life Cycle

1.  **Procurement:** Planning, negotiating, and acquiring the product.
2.  **Deployment:** Installation and integration into the organization.
3.  **Management:** Monitoring performance and providing support.
4.  **Decommission and Disposal:** Replacing obsolete devices and retiring EOL systems securely.


# 📑 Standard Operating Procedures (SOPs)

**Standard Operating Procedures (SOPs)** are step-by-step instructions for performing common tasks.

  * **Efficiency:** They ensure tasks are completed efficiently and consistently.
  * **Compliance:** They are often required for regulatory standards.
  * **Reliability:** They reduce failures and miscommunication by providing a standardized method.

SOPs should cover daily operations and be clearly written so anyone can understand and follow them. Poorly defined SOPs lead to inefficiency.


# 🔒 Hardening and Security Policies

Network professionals must understand security policies designed to prevent malicious activity.

### 🔑 Password Policies

Policies ensure users create complex passwords to resist attacks.

  * **Uniqueness:** Do not reuse passwords across systems.
  * **Complexity:** Use uppercase, lowercase, numbers, and symbols.
  * **Length:** Minimum of 8 characters (or more).
  * **Rotation:** Change passwords every 30 to 60 days.
  * **Lockout:** Disable accounts after consecutive failed login attempts (e.g., 3 failed attempts in 60 seconds).
  * **Recovery:** Clear procedures for forgotten passwords.
  * **Recommendation:** Use **Password Managers** and **Two-Factor Authentication (2FA)**.

### ✅ Acceptable Use Policy (AUP)

The **AUP** outlines the rules of conduct and constraints an employee must agree to before accessing the network. It prevents employees from visiting unsafe websites or being unproductive. New hires typically sign this during onboarding.

### 📱 Bring Your Own Device (BYOD)

**BYOD** policies allow employees to use personal devices (phones, laptops) for work.

  * **Risk:** Personal devices are not managed by IT and may have outdated software or malware.
  * **Mitigation:** Networks must monitor suspicious activity and profile devices to ensure they meet minimum security requirements before granting access.

### 🌐 Remote Access Policies

This defines how employees securely connect to the network from outside.

  * **Protocols:** Common methods include **SSH**, **RDP**, **VNC**, and **VPN**.
  * **Policy Content:** Define authorized users, privileges, VPN concentrators, and client configurations to prevent unauthorized access.

### 👤 Onboarding and Off-boarding

  * **Onboarding:** Training new employees on security policies and business processes.
  * **Off-boarding:** Critical for security when an employee leaves.
      * Disable (do not delete) user accounts immediately.
      * Change system passwords known to the user.
      * Retrieve all company equipment.

### 🛡️ General Security Policies

The head of information security develops policies to protect tangible and intangible assets. This involves understanding risks, privacy needs, and protecting against both **internal** and **external** threats.

### 🚫 Data Loss Prevention (DLP)

**DLP** solutions (found in firewalls, email systems, and EDR) prevent the exfiltration of sensitive data. They monitor for data breaches in real-time, stopping employees or threat actors from stealing confidential information.


# 📂 Common Documentation

Network professionals rely on specific documentation for planning, maintenance, and troubleshooting.

  * **Physical Network Diagrams:** Floor plans showing device locations, rack diagrams (server/network racks), and termination points (IDF/MDF).
  * **Logical Network Diagrams:** Illustrates packet flow, device interconnections, IP schemes, and protocols.
  * **Wiring Diagrams:** Layout of physical cabling connections throughout the organization.
  * **Site Survey Reports:** Used for wireless implementation. Details coverage areas, interference, and optimal Access Point placement based on floor plans and signal measurement.
  * **Audit and Assessment Reports:** Detailed analysis of network performance and security status.
  * **Baseline Configurations:** A snapshot of the system operating in an acceptable state. This allows professionals to detect abnormalities later.


# 🤝 Common Agreements

Organizations use legal agreements to ensure security and service levels.

  * **Non-Disclosure Agreements (NDAs):** Legal documents preventing employees, contractors, or providers from disclosing confidential information.
  * **Service-Level Agreements (SLAs):** An agreement from a service provider to a customer guaranteeing a specific level of service (e.g., uptime).
  * **Memorandum of Understanding (MOU):** A less formal agreement, often a letter, outlining the intention between two parties. It may not always require a signature.

---