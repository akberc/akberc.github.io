---
layout: post
title: Overview of ITIL-based Application Backup and Recovery
tagline: formalising backup for business continuity
date: 2012-03-25 13:11:36+00:00
tags: [itil, continuity, backup, recovery]
category: architecture
comments: false
---
*Derived from a subset of IT Service Continuity Management (ITIL v3 ITSCM):* ITIL v3 ITSCM considers application backup and recovery as one of the risk mitigating factors in assuring service continuity. This is a brief discussion of commonly understood IT application backup and recovery methods within the ITIL v3 ITSCM framework.
<!-- more -->
In ITIL v3, ITSCM (IT Service Continuity Management) is defined as:
>*‘The goal of ITSCM is to support the overall Business Continuity Management process by ensuring that the required IT technical and service facilities (including computer systems, networks, applications, data repositories, telecommunications, environment, technical support and Service Desk) can be resumed within required, and agreed, business timescales.’ (ITIL v3 ITSCM 4.5.1)*

Within each of the four stages of ITSCM, backup and recovery planning and the testing and invocation of its procedures, is mapped as follows:

##Stage 1 - Initiation
>*Resource allocation: Depending on the maturity of the organization, with respect to ITSCM, there may be a requirement to familiarize and/or train staff to accomplish the Stage 2 tasks. Alternatively, the use of experienced external consultants may assist in completing the analysis more quickly. However, it is important that the organization can then maintain the process going forward without the need to rely totally on external support. (ITIL v3 ITSCM 4.5.5.1)*

In other words, the ultimate ownership of the backup and recovery strategy and processes lies with the organization itself.

##Stage 2 - Requirements and Strategy
Once the Business impact Analysis and Risk Analysis has been done, backup and recovery of applications and data is usually one of many Risk Response Measures.
>*A comprehensive backup and recovery strategy, including off-site storage. (ITIL v3 ITSCM 4.5.5.2)*

The recovery procedures are defined first, and then backup procedures and their frequency are based on the needs of the recovery procedures.

Common recovery options include:
1. **Cold Standby** (Gradual Recovery): Servers need to be reconfigured and applications deployed, and this can take days or weeks.
2. **Warm Standby** (Intermediate Recovery): From minutes to a few hours, this option requires servers and applications already configured and deployed, that need to be connected to the production infrastructure (using network or other techniques. By engaging a third party to host alternate hardware, this technique can also be used for disaster recovery.
3. **Hot Standby** (Immediate or Fast Recovery): This option requires redundant hardware and applications that may or may not be at the same physical location, which automatically take over, without minimal interruption to IT services.

##Stage 3 - Implementation
In this stage, backup and recovery processes are implemented using one or more of the following types of tests:
1. Theoretical Testing: Concerned individuals meet to assess the effectiveness of the backup and recovery procedures
2. Announced and unannounced full testing: this is a full dress rehearsal.
3. Partial testing and event-based testing: this is a subset of full testing.

##Stage 4 - Ongoing Operations
>**Testing** – *following the initial testing, it is necessary to establish a programme of regular testing to ensure that the critical components of the strategy are tested, preferably at least annually, although testing of IT Service Continuity Plans should be arranged in line with business needs  . . .  All plans should also be tested after every major business change. (ITIL v3 ITSCM 4.5.5.4)*

Recovery Invocation
When disaster strikes, the organization needs to put the recovery plans into action:
* Retrieval of backup tapes, data documentation, procedures, software images etc. from on-site or off-site locations
* Mobilization of the appropriate technical personnel to commence the recovery of required systems, servers, applications and services
* Contacting and putting on alert customers, partners, service providers, application vendors, etc. who may be required to undertake actions or provide assistance in the recovery process

