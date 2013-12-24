---
layout: post
title: Proposal Submission and Management System on Atlassian JIRA
tagline: (for The Research Council, Oman) by Akber Choudhry and Dusko Knezevic
date: 2009-11-07 23:10:00+00:00
tags: [seam, jira, identity]
category: architecture
comments: false
---
**An Issue is an Issue** : Alassian JIRA is all about issues.  In fact, Atlassian sends out T-shirts saying 'Because you've got issues'!  We first started using JIRA in a purely development support role, but then we read a case study from a company that was using JIRA for their new-hire orientation process.  

We had a particularly challenging project that had a three-month implementation plan (which we took rather seriously), and which required a fairly sophisticated workflow.  The requirements called for researchers (end users) submitting research proposals under multiple disciplines which went through a combined workflow, then an approval particular for for the specific discipline that included external reiewers, and then again through a combined workflow for final granting or rejection.

<!-- more -->

##Software Stack for the Solution
The client and the project team had chosen <a rel='nofollow' href='http://seamframework.org/'>JBoss Seam</a> as the front-end, primarily due to its close integration with JBoss application server and jBPM as well as the Drools rules engine, but also due to the <i>portletbridge</i> API that allowed a Seam application to run inside JBoss Portal.  Developing with an agile methodology, we were still undecided whether we were going to use jBPM for the actual workflow or come up with something else.  As the requirements poured in, it became apparent that a number of persistence, data, security and administration interaction artefacts would have to be developed in order to support the workflow in jBPM. 
<br/>
<br/>
As you may have guessed by now, we decided to use JIRA as the workflow back-end:  end users would access the Seam application, which would use JIRA through its Web Services API for workflow and persistence.  The original user interface of JIRA would be modified using string replacements to provide the administration interface.  Persistence and file attachments were transparent.  It would work!

##Interface Customisation
Projects and sub-projects became 'research disciplines', issues became 'research proposals', and releases became 'call for papers'. The OSWorkflow engine proved to be very flexibile, and transition screens provided the approval input.


##Identity Integration
So far, so good!  Now came some tricky security issues:
* External users (researchers) were being authenticated by a distributed authentication mechanism, and their user id was provided to the front-end application.  By setting up a trusted symmetric key between the front-end application and JIRA, existing users could be looked up and new users created in JIRA.
* When new users logged in to the front-end, they would be automatically logged in to JIRA using the SOAP API client, with a custom algorithm that bypasses the regular credential check (database password), substituting it for another type of credential check.  This was implemented as another authentication Java class similar to the LDAP authentication Java class that ships with JIRA.  This type of login would only be valid when coming through the SOAP API, in order to avoid inadvertent end-user authentication on the back-end administration interface should they have physical or network access to the administration interface.
* Finally, on the back-end administration interface, a 'real' administrator login (user and password in database) would still be authenticated due to the built-in JIRA login architecture that goes through all possible authenticators one by one.


##Seam Integration and Testing
The SOAP client derived  from the JIRA WSDL was wrapped in Seam components:
* a UserClient - that held the authentication token for the logged-in user.
* an AdminClient - extending the UserClient, but holding an administration login token in order to create new users or look up existing users, and perform other administrative functions through the SOAP API.

Both of these clients were extended into 'mock' scope components in Seam in order to simulate a back-end JIRA using a couple of HashMaps embedded within the mock clients.  This allowed the front-end developers to progress rapidly with their work while not depending on back-end JIRA configuration that was proceeding at its own pace.  For example, when the front-end created a proposal (issue) and called the API to persist it, the mock client would just store the RemoteIssue object into a HashMap keyed by the issue ID.  All subsequent calls to the mock client using that key would retrieve the same RemoteIssue object.

Drop us an email (address on main page of this site) for the source code for the mock JIRA service.

This was a somewhat unorthodox use of JIRA, but this approach resulted in a robust, scalable and feature-rich platform.  The unlimited-user license for JIRA is an expense, but replicating the features of the system would be at an even greater cost.  The system was deployed in February 2009 at <a rel='nofollow' href='https://www.trc.gov.om/portal/sec/portal/default/TRESS'>https://www.trc.gov.om/portal/sec/portal/default/TRESS</a>
