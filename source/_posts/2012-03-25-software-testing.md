---
layout: post
title: Software Testing
tagline: overview and challenges
date: 2012-03-25 23:11:17+00:00
tags: [testing, algorithms, complexity, technique]
category: development
comments: false
---
**Algorithmic Complexity and the Theoretical Limits of Testing:** According to the undecidability theorem, most software quality properties are not provable. Therefore, what kind of testing techniques do we use to achieve software quality?  While it is theoretically impossible to deterministically test a system for flawless quality, it is possible -- through good design, communications and dynamic testing -- to prevent and detect defects, and to verify and validate the system against pre-defined expectations.
<!-- more -->
##Undecidability Theorem
The undecidability or incompleteness theorem is a statement of complexity of systems (a group of logical statements when taken together) first formulated by Godel [1](#references) -- and is the precursor to Turing's halting theorem about Turing machines -- which in turn is the precursor of modern program-based computer systems. Without going into details, a good summary that serves the current purposes is: *any piece of code that's complex enough to be interesting will always surprise its programmers* [2](#references).

This concept is generally known as **algorithmic complexity** (AC). In Claim 4 , Lewis successfully uses these theorems to prove that 
> _There is no estimator which produces a correct fixed bound on the complexity of all inputs."_  [3](#references). 
The impications of algorithmic complexity do not apply only to software programs, but extend to other areas such as encryption algorithms, computer security, etc.

##Testing techniques: origins and types
So, how do we test software for quality if we assume that we have proven that software can never be completely tested? By -- **prevention, detection, verification** and **validation**. These concepts are fairly generic and subjective, and to make them as objective as possible, a numbe of techniques have been specified by scientists and have evolved in business software development.

In the recent past, these techniques have been refined and assumed greater importance with the advent of distributed software that relies on multiple systems working correctly and as expected in order to fulfil the business goals. In other words, the "contractual" reliability of the interfaces between disparate software systems has resulted in these techniques coming to the forefront of software development as part of a continuous quality assurance process [4](#references).

Here are the three main groups of these techiques and most of them involve steps **before, during** and **after** the development of software (the foundation of TQM). Both groups involve **static** (without execution) and **dynamic** (execution) testing of programs.

###1. Functional Testing (black-box)
The developed software system is seen as a black box which is expected to satisfy a set of business requirements. Those requirements are provided to developers as specifications, and once the programs have been partially or completely developed, they are tested against these functional specifications. This testing is sometimes **manual** -- as in user clicking on a GUI and producing results or sophisticated programs can be used to design and quantify the functional tests, and then to measure the software against them.

Functional test generation and execution tools are a fairly recent addition [5](#references). Commonly employed techniques are:
* Acceptance testing: dynamic: where the software testing is tested against user specifications so that the user community "accepts" it.
* Regression tests: dynamic: when changes in a prior version of the software are tested to make sure that they have not compromised existing functionality.
* Integration testing: dynamic: when separately developed components are testing when they are executing in concert with each other.
* End-to-end testing or transaction testing: a business transaction is tested from beginning to end.
* Inspections: static :when the software is tested for completeness and interaction and functional assumptions are validated by a dialogue between the user community and the development team, usually with a meeting that involves a design of the system.

###2. Structural Testing (white-box)
These tests delve inside the code of the system and test the logic of individual pieces. It may be necessary to organize the code in a way to make structural testing possible. Almost all of these techniques are **automatic**, using a variety of tools. These tests are NOT exhaustive, i.e. if they were to check for all valid inputs, the number of tests would be astronomical. In real-life, experienced programmers check for bounds, limits, nulls, zeros and other such inputs into "units" of code. Commonly employed techniques include:
* Unit testing: dynamic: programmatically tests portions of the code against a set of conditions specified by the programmer that developed the software or another programmer. This is further augmented by *unit test coverage testing* -- testing that tests the extent of the code that is "covered" by unit testing!
* Code walk-throughs: static : the programmer walks through the logic and branching of the code by him/herself or with the development team - looking for obvious flaws that are detectable by a 'second pair of eyes'. It is also helpful for junior programmers to learn best practices in coding.
* Branch-condition testing: dynamic : using tools and pre-compilers, the execution of code is tested in conjunction with unit testing (see above) to determine if all the branch conditions in the code have been "covered".
* Thread testing: static dynamic: this tests the code for concurrent or "race conditions". Such tests are notoriously hard to design due to the unpredictability of such conditions and good design is always a must, and as such, I classify them as 'static' also.

###3. Operational Testing
These types of testing test the software under operational conditions. Examples include:
* Stress testing: dynamic : testing the software under operational loads that exceed the maximum expected loads on the system.
* Security breach testing: static and dynamic: testing the software under a combination of real-world security risks.
 
###Combination of Techniques (gray-box), and Risk Analysis
A good testing regimen is a combination of functional and structural testing as well as operational testing. This has been referred to as "gray-box"! However, the choice of the exact techniques to use depends on an experienced **risk analysis** of the business impact of software defects in terms of financial loss and prestige loss (sometimes it is the same thing). For example - what is the business impact of a bank account statement being sent to the wrong person? What is the impact of a delayed product shipment? etc.

<a name="references">&nbsp;</a>
##References
1. [R. Lucas: Minds, Machines, and Gödel. Philosophy XXXVI (1961):112-127, retrieved on 18 September, 2005.](http://users.ox.ac.uk/~jrlucas/Godel/mmg.html)
2. [Mitchell Waldrop, Complexity: The Emerging Science at the Edge of Order and Chaos, Simon and Schuster, 1992, 282. , retrieved on 18 September, 2005.](http://www.awprofessional.com/articles/article.asp?p=101654)
3. JP Lewis, Limits to Software Estimation, ACM SIGSOFT, Volume 26 Issue 4 July 2001, p. 58.
4. W Lewis, Software Testing and Continuous Quality and Improvement, 2nd Edition, pp. 29-39.
5. [Functional Testing: http://www-306.ibm.com/software/awdtools/tester/functional/index.html](http://www-306.ibm.com/software/awdtools/tester/functional/index.html)

