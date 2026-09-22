# IT Audit Services: What They Cover and How to Prepare

*By Junaid Khan, Lead Business Analyst, R&D and Presales Consultant, INNERLUXES. First published 22 September 2026 on [innerluxes.dev](https://innerluxes.dev/it-operations/information-technology-audit-services). That page is the canonical version of this article.*

Most requests we get for an "IT audit" turn out to be one of three different things: a compliance review ahead of a
certification, a due-diligence check before an investor or acquirer looks at the business, or an internal health
check after something went wrong. The scope is different each time, and knowing which one you need before you call a
firm saves weeks.

This article is the version of that conversation I have most often before any engagement starts.

## What an IT Audit Actually Checks

Strip away the branding and an IT audit checks four things, in this order.

- **Does the control exist?** Is there a written policy for access, change management, backups, and incident response?
- **Is it followed?** A sample of real access requests, change tickets, and backup logs is checked against the policy, not just the policy document itself.
- **Is there evidence?** Every control needs something that proves it ran — a ticket, a log entry, an approval record — not a verbal assurance.
- **Is it proportionate?** A five-person company does not need the same change-approval chain as a five-hundred-person one; auditors adjust expectations to size and risk.

The output is a findings report ranked by risk, each finding tied to a specific control gap, not a generic checklist score.

## IT Audit vs. Penetration Test vs. Security Assessment

| Service | Answers | Method |
|---|---|---|
| **IT audit** | Do our controls exist, get followed, and leave evidence? | Policy review, ticket sampling, interviews, evidence checks. |
| **Penetration test** | Can an attacker actually get in, and how far? | Active testing of systems and applications. |
| **Risk assessment** | What could go wrong, and how bad would it be? | Structured review of assets, threats and likely impact, no active testing. |

These overlap but answer different questions. A clean pentest report does not mean your change-management process is
documented, and a clean audit does not mean nobody can break in. A firm that offers both, and is honest about which
one you need first, is worth more than one that always recommends its own biggest package.

## Types of IT Audit

- **Compliance-readiness audit.** Run ahead of an ISO, SOC 2, or industry-specific certification, to find gaps before the formal certifying audit does.
- **Due-diligence audit.** Run before an investment, acquisition, or major partnership, focused on what a buyer's technical team will ask about.
- **Internal controls audit.** A periodic health check, often annual, covering access, change management, backups, and vendor risk.
- **Post-incident audit.** Run after a breach or major outage, to establish what control gap allowed it and what changed since.

Each type samples the same underlying control areas but with a different emphasis: a due-diligence audit spends more
time on licensing and vendor contracts, a post-incident audit spends more time on the specific control that failed.

## What to Prepare Before an IT Audit

- A current inventory of systems, servers, cloud accounts, and the person or team who owns each one.
- Written access control and change management policies, even short ones, rather than none.
- A sample of recent access requests, approvals, and change tickets an auditor can trace end to end.
- Backup logs and, ideally, a record of the last time a restore was actually tested.
- A list of third-party vendors with system access, and what that access is scoped to.
- An organization chart showing who is accountable for each system, not just who administers it day to day.

Firms that gather this in advance typically cut audit duration by a third, because the auditor spends less time
chasing evidence and more time evaluating it.

## Common Findings, and What They Usually Mean

- **Access review not evidenced.** A policy says access is reviewed quarterly, but there is no ticket or log showing the last review happened.
- **Shared administrator accounts.** One login used by several people, so no individual action can be traced.
- **Backups untested.** Backups run on schedule, but nobody can show a successful restore in the last twelve months.
- **Offboarding lag.** A departed employee's access is disabled days or weeks after their last day, not on it.
- **Vendor access with no expiry.** A contractor or vendor was granted system access for a project that ended months ago, and it was never revoked.

None of these findings are unusual, and none require a large rebuild to fix. Most close with a written procedure, a
scheduled review, and one clean-up pass through existing accounts.

## Questions to Put to an IT Audit Firm

- Which standard or framework does your audit map to, if any, and can I see a sample findings report?
- Do you sample evidence, or do you take our policy documents at face value?
- Will the same team that finds the gaps also be available to help close them, or is that a separate engagement?
- How long will your team need read access to our systems, and what is revoked when the audit ends?
- What is included in the fixed fee, and what would trigger extra cost partway through?
- Who signs the final report, and what is their basis for it — a named auditor or an automated scan?

## Protecting Audit Evidence and Access

An IT audit involves handing over access lists, change logs, and sometimes credentials for review. Whichever firm you
use, decide who sees this material and for how long. When our engineers work on audit preparation or remediation, our
own arrangements are the same as on any project: an NDA is signed before we see access lists, tickets, or system
credentials; we review evidence and samples rather than requesting standing production access wherever a sample will
do; engineers see only the systems and datasets their task needs; client evidence, credentials, and data stay inside
a Chromium enterprise browser we built in-house, so nothing sits on a personal laptop; and at the end of the
engagement we revoke access, wipe local copies, and confirm deletion to the client's named contact in writing.

## Q&A

**What is an IT audit?**
It is a structured review of how your organization manages its IT environment: who has access to what, how changes
are made and approved, how systems are backed up and recovered, and whether the controls you say you have actually
operate day to day. It checks process and evidence, not just whether a firewall is configured correctly.

**How is an IT audit different from a penetration test?**
A penetration test tries to break in and reports the technical weaknesses it finds. An IT audit checks whether your
controls and processes exist, are documented, are followed, and leave evidence. A mature IT function usually needs
both: the audit checks the process is real, the pentest checks the process actually holds up against an attacker.

**Do we need an IT audit if we already have ISO or SOC 2?**
A certification audit and an internal or vendor-readiness IT audit serve different purposes. A certification audit
confirms you meet a named standard on a schedule set by the certifying body. An internal audit can run at any time,
focus on the areas that worry you most, and surface gaps well before the certification audit does.

---

Full article with the IT audit preparation worksheet: [innerluxes.dev/it-operations/information-technology-audit-services](https://innerluxes.dev/it-operations/information-technology-audit-services)
