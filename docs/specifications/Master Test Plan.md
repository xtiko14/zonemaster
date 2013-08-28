New DNSCheck Master Test Plan
=============================

Document Control
----------------

*Roles*

| Made By        | Responsible for fact | Responsible for document |
|:---------------|:---------------------|:-------------------------|
|Patrik Wallström| Patrik Wallström     | Patrik Wallström         |

*Security*

| Security class | File name            |
|:---------------|:---------------------|
| External       | NewDNSCheck-MTP.md   |

*Revisions  *

| Date       | Version | Name               | Description           |
|:-----------|:--------|:-------------------|:----------------------|
| 2013-08-27 | PA1     | Patrik Wallström   | First draft           |
|            |         |                    |                       |


Table of Contents
-----------------
* auto-gen TOC:
{:toc}

Introduction
------------
This section gives a brief introduction to the New DNSCheck.

### Background
DNSCheck from .SE and Zonecheck from AFNIC are two different software packages that do DNS validation of the quality of a DNS delegation. The New DNSCheck implementation intends to be a major rewrite of these software packages, and implement the best parts of both.

### Purpose
The purpose of the New DNSCheck is to test the quality of a DNS delegation. The core of the software is all the implemented tests. There will be a command line tool to run a complete set of tests, and a web interface tailored for use by both basic and advanced users.

### Goals
The goal of this document is to give an overview of the requirements and the test levels. Each of the requirements will be broken down into a set of test procedures. The process of doing this will be done in accordance with the standard IEEE 829-2008.

### Scope
Only the current test cases derived from the current versions of DNSCheck and Zonecheck will be described as requirements. These documents will not describe the functionality of any software implementing the test cases. Some test cases derived from the current software will not be implemented as test cases in the New DNSCheck.

### References
#### External
The current implemented tests in DNSCheck are described here:  
https://github.com/dotse/dnscheck/wiki/Tests  
https://github.com/dotse/dnscheck/wiki/Detailed-list-of-all-possible-dnscheck-messages

The current implemented tests in Zonecheck are described here:
http://www.zonecheck.fr/features.shtml
#### Internal
No internal requirements.
#### Document hieararchy
* Master Test Plan  
  * Level Test Plan x  
    * Test Case 1  
    * Test Case 2  
    * Test Case 3  
  * Level Test Plan y  
    * Test Case 4  
    * Test Case 5  
    * Test Case 6  
  * Level Test Plan z  
    * Test Case 7  
    * Test Case 8  
    * Test Case 9  

### System overview and key features
A domain will be tested for the quality of the delegation in the DNS hierarchy. Some of the high level properties that will be tested include:

* Delegation properties (parent and child name servers)  
* Consistency (all name have consistend answers)
* DNSSEC properties (algorithms, secure delegation)  
* Address properties (IP addresses)  
* Name server connectivity  
* Zone properties (are data controlling the zone sane)

A domain can be given to the testing system and all DNS information will be retrieved from the public global DNS hierarchy, or a set of pre-delegation data can be given to test a domain not yet published in the global DNS hierarchy. A complete set of DNS queries and answers can also be given as the input to the system for repeat testing.

### Test overview
The test organization, test schedule, integrity level scheme, test resources, responsibilities, tools, techniques, and methods are necessary to perform the testing.
#### Organization
A test is run on any machine where the New DNSCheck software is available. The tests ordinarily needs access to the global public DNS hierarchy to be performed.
#### Master test schedule
A test is run as soon as the software is scheduled to run, often immediately upon execution.
#### Integrity level schema
An integrity level schema is used for illustrating relative importance of a software component. The effect of a failing component can range from negligible to catastrophic. A component with a high integrity level needs to be tested more thoroughly than a component with a low level. There is, however, no guidance in the requirements that indicate the relative importance of different areas. Each area is thus considered equally important. However, one of the main objectives is to ensure the stability of DNS.
#### Resources summary
TODO: Briefly describe the neessary resources to run a test.
#### Responsibilites
#### Tools, techniques, methods, and metrics
TODO: Briefly described the necesessary input and any metrics in the output.


Details of the Master Test Plan
-------------------------------
The utilization of the IEEE 829-2008 is described in this chapter. There is also a mapping between the test areas and the requirements.

### Test processes
The goal of these documents is to describe the test cases and how the DNS is tested. This is a part of a larger project where the goal is to test the quality of the Internet. Processes for Management, Acquisition, Supply, Development, Operation, and Maintenance are not part of this subproject to define.

### Definition of test levels
There can be different types of tests, e.g. unit, system, and acceptance tests. This test environment will only focus on acceptance testing, thus only one test level. Multiple areas have however been identified within the system requirements:

* Delegation
* Consistency
* DNSSEC
* Address
* Connectivity
* Zone

However, the separation of test levels does not necessarily mean that the levels are separated in the New DNSCheck implementation. The actual test levels might differ from the actual test modules in the code. At this level, the separation is done to make a better overview of all the test cases specified.

### Test documentation requirements
The followin documents can be created according to the standard:

* Level Test Plan (LTP)
* Level Test Design (LTD)
* Level Test Case (LTC)
* Level Test Procedure (LTPr)

However, the LTD has been incorporated in the LTP and in the LTC. LTPr has been incorporated in the LTC.

#### Level Test Plan
The system will undergo acceptance testing against the requirements. Each area is documented in a separate test plan. The purpose is to map the requirements into test cases and also to describe the approach for testing this level.

In the title of the plan, the word “Level” is replaced by the name for the particular level being documented by the plan. E.g. Delegation Test Plan and DNSSEC Test Plan.

#### Level Test Case
The purpose of the LTC is to define the information needed as it pertains to inputs to and outputs from the software or software-based system being tested. The test cases may be documented in a single or multiple LTC depending on the extent of the area. Any procedures are included in the documentation.

In the title of the test case, the word “Level” is replaced by the name for the particular level being documented by the test case. The documents have sub-titles since there can be more than one document within one level. E.g. DNSSEC Test Cases or Connectivity Test Cases.

### Test administration requirements
These activities are needed to administer the tests during execution.

#### Anomaly Resolution
The tests are executed with the input given by the user. The input data is validated to be correct. Depending on the input data and what is available in the public DNS, some test cases might not be executed.

The output from DNSCheck should clearly indicate what test cases have been executed, and which have not.

#### Reporting Processes
The output from all the tests are collected by the system and reported back to the user depending on the choice of the user. There might be several different methods used, for example as a brief or verbose log file, or as XML or JSON output, or directly into a database.

### Test reporting requirements
The following documents can be created according to the standard:

* Level Test Log (LTL)
* Anomaly Report (AR)
* Level Interim Test Status Report (LITSR)
* Level Test Report (LTR)
* Master Test Report (MTR)

Only an MTR will be generated by the system.

#### Level Test Log
All logs from each test level are aggregated into the Master Test Report.

#### Anomaly Report
An Anomaly Report is created if the result from the test is not conclusive due to internal or external anomalies. All anomalies are in the Master Test Report. However, the software implementation will also report any anomalies with a different return code, so any calling software can determine if the test cases were executed as planned, or if any anomaly stopped the execution prematurely.

#### Master Test Report
The Master Test Report is generated continually during the execution of the test plan. It will indicate the result of all the test cases, and depending on any selected verbosity also down to the level where you can see all the DNS queries and replies in a preferred data format.

TODO: make a better description of the log files here?

### System requirements
The initial requirements are derived from the current Zonecheck and DNSCheck documentation and implementations. A basic requirement is to implement all tests that Zonecheck and DNSCheck currently implements. However, there is a large overlap between the two implementations, and also several test cases that are no longer applicable.

Currently there is no other requirements other than to implement the test cases from the current implementations.

TODO: do we need a separate requirements document?

#### DNSCheck
These are the current documented test cases from DNSCheck:
https://github.com/dotse/dnscheck/wiki/Tests
https://github.com/dotse/dnscheck/wiki/Detailed-list-of-all-possible-dnscheck-messages

#### Zonecheck
The current implemented tests in Zonecheck are described here:
http://www.zonecheck.fr/features.shtml

#### RFCs
Where it is possible, the test cases refer to any RFCs describing what the current IETF standards advise on the implementation of the DNS protocol.


General
-------
This section contains the glossary and document change procedures for all of the test plans and test cases.

### Glossary
| Word / Acronym | Explanation                              |
|:---------------|:-----------------------------------------|
| DNS            | Domain Name System                       |
| DNSSEC         | DNS Security Extensions                  |
| RFC            | Requst for Comments, IETF document       |
| MTP            | Master Test Plan                         |
| MTR            | Master Test Report                       |
| LTC            | Level Test Case                          |
| LTL            | Level Test Log                           |
| LTP            | Level Test Plan                          |
| LTR            | Level Test Report                        |

### Document change procedures
The overall change procedures are defined by the project and the change management. However, there are some steps to take into consideration when changing the test documents.

#### Identifying
A change to the documents may be initiated because of several reasons:

* New internal or external requirements
* Problems with the test cases
* Text that needs to be clarified
* Etc.

#### Implementing
The document revisioning is managed by a version control system (Git). Each change must contain a specific commit message detailing the change. The major revisions section of this document should also be updated if there is a new release of the document.

It is important that the outcome of the test cases stays the same; unless the change was based on new or updated requirements.

#### Recording changes
An overall description must be stated in the document control chapter, including a new revision number. A more detailed description of the changes is part of the specific commit in the version control system.

#### Approving
The technical review team must approve any changes made to the test cases.