SOC 2-Aligned Cloud Security Operations & Incident Response

Overview

This project presents a cloud-agnostic security operations workflow designed to support **SOC 2 control objectives** across AWS, Microsoft Azure, Google Cloud Platform (GCP), and hybrid environments.

It integrates security monitoring, incident response, identity and access management, vulnerability management, change control, evidence preservation, and continuous control improvement.

The objective is to demonstrate how operational security activities can support an organization's SOC 2 compliance program through repeatable procedures, documented evidence, accountability, and measurable outcomes.

Scope: This is a reference architecture and educational portfolio project. It is not a SOC 2 audit, attestation, or certification.

Architecture

1. SOC 2 Trust Services Criteria Alignment

The workflow supports relevant criteria from the AICPA Trust Services Criteria. Final applicability depends on the organization's system description, selected criteria, risks, and auditor assessment.

| Trust Services area | Operational implementation | Example evidence |
|---|---|---|
| Security — CC6: Logical and Physical Access Controls | IAM, MFA, least privilege, privileged access reviews, account lifecycle controls | Access reviews, IAM policies, authentication logs, access change tickets |
| Security — CC7: System Operations | Centralized logging, monitoring, alert triage, vulnerability detection, incident response | SIEM alerts, investigation timelines, incident tickets, remediation records |
| Security — CC8: Change Management | Controlled configuration changes, approvals, testing, deployment tracking, rollback procedures | Change requests, approvals, deployment logs, configuration history |
| Security — CC9: Risk Mitigation | Risk assessments, vendor considerations, threat mitigation, vulnerability remediation | Risk register, remediation plans, risk acceptance records |
| Availability — A criteria, when applicable | Backup monitoring, recovery testing, resilience, availability incident management | Backup reports, restore tests, recovery results, availability monitoring |
| Confidentiality — C criteria, when applicable | Data classification, encryption, access restrictions, secure data handling | Encryption settings, access policies, data protection configurations |
| Processing Integrity — PI criteria, when applicable | Controls over complete, valid, accurate, and timely processing where relevant | Validation logs, processing exceptions, reconciliation results |
| Privacy — P criteria, when applicable | Privacy-related controls for the collection, use, retention, disclosure, and disposal of personal information | Privacy procedures, retention records, access logs, relevant consent records |

The Security category is fundamental to a SOC 2 examination. Availability, Confidentiality, Processing Integrity, and Privacy are additional categories that may be included according to the service commitments and scope.

The exact mapping of individual controls to Trust Services Criteria must be validated against the applicable AICPA criteria and the organization's control design.

2. End-to-End Operational Workflow

Stage 1 — Monitor and Detect

Collect and analyze telemetry from cloud services, identity providers, endpoints, networks, and applications.

Activities:
- Centralize security-relevant logs.
- Monitor alerts and suspicious activity.
- Detect unauthorized access and configuration changes.
- Track vulnerabilities and exposed resources.
- Maintain appropriate logging coverage and retention.

SOC 2 relevance: Supports system monitoring and security operations under CC7.

Stage 2 — Triage and Assess Risk

Validate alerts and determine their severity, scope, and business impact.

Activities:
- Review alert context and enrichment.
- Identify affected assets, users, and data.
- Distinguish false positives from potential incidents.
- Prioritize investigation according to risk.
- Create or update an incident record.

Evidence: Alert details, timestamps, severity rationale, ticket identifiers, and analyst decisions.

Stage 3 — Investigate and Preserve Evidence

Establish what happened, when it happened, which assets were affected, and whether data or access was compromised.

Activities:
- Correlate identity, cloud, endpoint, and network events.
- Review relevant audit trails and configuration history.
- Establish an incident timeline.
- Preserve logs, relevant artifacts, and investigation notes.
- Record evidence sources and handling actions.

Evidence should be protected against unauthorized modification, retained according to policy, and accessible only to authorized personnel.

SOC 2 relevance: Supports monitoring, incident investigation, and the ability to demonstrate control operation.

Stage 4 — Contain and Respond

Limit the impact of confirmed or sufficiently credible threats.

Activities:
- Disable or restrict compromised accounts when justified.
- Revoke sessions and rotate affected credentials.
- Isolate compromised workloads.
- Restrict unauthorized network or data access.
- Escalate incidents according to severity and response procedures.

Document the decision, authorization where required, action taken, timestamp, responsible party, and outcome.

SOC 2 relevance: Supports the incident management and response activities associated with CC7.

Stage 5 — Eradicate and Remediate

Remove the threat and address the underlying weakness.

Activities:
- Remove malicious artifacts and persistence mechanisms.
- Patch exploited vulnerabilities.
- Correct excessive permissions and insecure configurations.
- Review the root cause and contributing factors.
- Implement changes through the approved change-management process.

SOC 2 relevance: Supports system operations, risk mitigation, and controlled changes under relevant CC7, CC8, and CC9 criteria.

 Stage 6 — Recover and Validate

Restore affected services safely and confirm that the environment is operating as expected.

Activities:
- Restore from trusted backups when necessary.
- Validate system integrity and security configurations.
- Confirm that required business functions operate correctly.
- Monitor for recurring malicious activity.
- Document recovery decisions and results.

Evidence: Recovery logs, restore test results, validation records, and incident closure approval.

SOC 2 relevance: Supports recovery and availability controls where those controls are within scope.

Stage 7 — Report and Improve

Close the incident with a documented outcome and strengthen the control environment.

Activities:
- Produce an incident report and root cause analysis.
- Record remediation actions and outstanding risks.
- Update detection rules and response playbooks.
- Track corrective actions to completion.
- Review recurring issues and control effectiveness.

Evidence: Incident reports, corrective action records, updated rules, management reviews, and trend metrics.

3. Cloud Security Tooling

The workflow is cloud-agnostic. Specific integrations depend on the services deployed and the organization's architecture.

AWS
- **AWS CloudTrail:** API activity and audit trails.
- **Amazon GuardDuty:** Managed threat detection.
- **AWS Config:** Resource configuration history and compliance evaluation.
- **AWS Security Hub:** Security findings and posture visibility.
- **Amazon Inspector:** Vulnerability findings for supported workloads.
- **Amazon S3:** Centralized storage for relevant logs and evidence, with appropriate access and retention controls.

 Microsoft Azure
- Azure Activity Logs and relevant resource diagnostic logs.
- Microsoft Defender for Cloud.
- Microsoft Entra ID audit and sign-in logs.
- Microsoft Sentinel for SIEM and security orchestration capabilities.
- Azure Policy and supported configuration assessment capabilities.

Google Cloud
- Cloud Audit Logs.
- Cloud Logging and Cloud Monitoring.
- Security Command Center, where available and enabled.
- IAM and organization policy controls.

 SIEM, EDR, and Automation
- Microsoft Sentinel.
- Splunk Enterprise Security.
- Microsoft Defender.
- Other supported EDR, ticketing, and SOAR platforms.

A SIEM can correlate security events and support investigation. It does not, by itself, establish SOC 2 compliance; logging coverage, access, retention, alert handling, and control operation must also be demonstrated.

4. Practical Scenarios

Scenario A — IAM Compromise

Threat:** Suspicious sign-in followed by unauthorized privilege escalation.

Investigation:
1. Review sign-in and audit events.
2. Validate the user, source IP, device, MFA results, and relevant access policies.
3. Correlate role assignments, credential changes, and subsequent API activity.
4. Determine the scope and potential business impact.

Response:
1. Restrict compromised access and revoke sessions as appropriate.
2. Remove unauthorized privileges.
3. Restore approved access configurations.
4. Record evidence, remediation, and validation.

SOC 2 relevance: Logical access controls (CC6), system operations and incident response (CC7).

 Scenario B — Public S3 Bucket Exposure

**Threat:** An S3 bucket becomes publicly accessible or is accessed without authorization.

Investigation:
1. Identify the configuration change using AWS Config and relevant CloudTrail events.
2. Determine the actor, timestamp, API call, and affected resources.
3. Review available object-level data events and access logs.
4. Assess potential data exposure and exfiltration.

Response:
1. Restrict unauthorized public access.
2. Restore approved bucket policies and access controls.
3. Review IAM permissions and credentials.
4. Preserve evidence and document remediation and validation.

SOC 2 relevance: Access controls (CC6), system operations (CC7), and change management (CC8), depending on the applicable control design.

Scenario C — Server Compromise

**Threat:** Malware, suspicious processes, or persistence on a cloud virtual machine.

Investigation:
1. Correlate EDR, operating system, authentication, and network logs.
2. Identify suspicious process execution and persistence mechanisms.
3. Establish the affected systems and potential data exposure.
4. Preserve relevant forensic evidence.

Response:
1. Isolate affected workloads when appropriate.
2. Remove malicious artifacts and remediate the initial access vector.
3. Patch vulnerabilities and validate system integrity.
4. Restore services and monitor for recurrence.

SOC 2 relevance: System operations and incident response (CC7), risk mitigation (CC9), and availability criteria where applicable.

5. Evidence and Audit Readiness

A key project objective is to make security activities traceable and reviewable.

For each incident, maintain a record containing:

- Incident ID, description, severity, and timestamps.
- Detection source and relevant event identifiers.
- Affected systems, identities, and data classifications where applicable.
- Investigation timeline and supporting evidence references.
- Containment and remediation decisions.
- Required approvals and change records.
- Recovery and validation results.
- Root cause, corrective actions, and closure details.

Evidence should be protected using appropriate access restrictions, integrity safeguards, retention schedules, and time synchronization. Retention periods must follow applicable organizational and contractual requirements.

**Important distinction:** Evidence that a policy exists is not the same as evidence that the control operated effectively. A SOC 2 examination may evaluate control design and, for a Type II examination, operating effectiveness over the defined review period.

 6. Security Metrics

Example metrics that can help management assess operational performance include:

- Mean time to detect (MTTD).
- Mean time to respond (MTTR), with the definition documented.
- Percentage of critical assets with required logging enabled.
- Percentage of high-risk findings remediated within policy targets.
- Number of overdue corrective actions.
- Incident recurrence rate.
- Successful backup restoration test rate.
- Percentage of privileged access reviews completed on time.

Metrics should have defined calculation methods, owners, reporting periods, and targets. They support management oversight but do not independently prove SOC 2 compliance.

7. Security Principles

- Least privilege and separation of duties.
- Centralized and appropriately protected audit logging.
- Risk-based monitoring and incident prioritization.
- Evidence preservation and traceability.
- Approved change management.
- Defined incident escalation and communication.
- Timely remediation and risk tracking.
- Recovery validation and continuous improvement.

8. Project Scope and Limitations

This repository provides a conceptual workflow and practical scenario design for cloud security operations aligned with selected SOC 2 Trust Services Criteria.

It does not represent a deployed production system, a complete control implementation, or an independent assessment. Actual SOC 2 readiness requires a defined system boundary, documented controls, assigned owners, operating evidence, risk assessment, and assessment by an independent CPA firm.

9. Future Improvements

Potential extensions include:

- Terraform-based AWS security lab.
- Sample CloudTrail and GuardDuty investigation.
- Sentinel or Splunk detection rules.
- Automated incident ticket creation and evidence collection.
- SOC 2 control-to-evidence matrix.
- Change-management and access-review templates.
- Incident response playbooks and tabletop exercises.
- Dashboard for security metrics and remediation tracking.



Cloud Security | SOC Operations | SIEM | Incident Response | Multi-Cloud Security | Security Controls and Compliance
