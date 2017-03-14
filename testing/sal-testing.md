SAL Testing
===========
> What do I look like, a guy who's not lazy?
> - Sal

The SAL Testing Process
-----------------------
The SAL Testing Process is a collection of test patterns and procedures MFDC has found to be a good balance between delivering reliable and correctly functioning software without making an ineffective use of already limited resources in any given project. In other words, **SAL Testing is intended to make the development process at MFDC a high leverage activity, helping us deliver software on time and to specification.**

The SAL Testing Process is as follows:

**LEVEL 1: DEVELOPLEMT TESTING**
* During the development of a feature/module
* Manual UI component testing (e.g. testing dropdowns, CRUD operations, app routing functionality, expected output, etc.)
* Automated testing (e.g. unit tests, e2e tests) SHOULD be implemented AT LEAST for mission critical or highly complex features/modules
* Conducted by the DEVELOPER

**LEVEL 2: COMMIT TESTING**
* Upon commiting a feature/module to the project version control system - i.e. Git
* Manual user flow testing (e.g. user login: start from app root path `/` -> go to login page -> login -> follow redirect, etc.)
* Any available automated tests MUST be run
* Dealing with defects (as detected by manual or automated testing):
	1. The assigned developer for the feature/module makes the necessary changes to address the issue (if defect detected in already committed code, new commit message addressing it MUST be prefixed with `BUGFIX: `)
	2. Level 1 testing for item being addressed
	3. Once the bugfix is commited, level 2 testing is engaged and repeated until item successfully passes level 2 testing
* Conducted by the DEVELOPER OR BA/QA team

**LEVEL 3: MILESTONE (PRE-RELEASE) TESTING**
* Upon delivery of system build milestone, e.g: System Build (Alpha) and System Build (Beta)
* Manual user flow testing of each deliverable / module
* Milestone testing MUST be conducted against an INTERNAL test plan / UAT document
* Every testable item specified in the test plan / UAT MUST be assigned a status of either: 'PASS', 'FAIL', or 'CLARIFICATION'
* There may be more than one round of level 3 testing
* Dealing with detected defects:
	1. Detected defects in the software are documented in the test plan / UAT
	2. The assigned developer must be alerted to address the issue
	3. The developer makes the necessary changes to the codebase to address the issue
	4. The developer conducts level 1 and 2 testing and, once the changes made to the relevant item pass both levels successfully the item returns to level 3 testing
	5. This process is repeated until the issue is successfully addressed and marked as 'PASS'
* Conducted by the BA/QA team

This testing process is intended to cover as much of the system build stage of a project as possible. As such, developers should be heavily repeating level 1 and 2 testing throughout the build. The BA/QA team should be invested in level 2 testing throughout the build. As a project edges toward a build milestone (e.g. Alpha or Beta) level 3 testing must be engaged and repeated until ALL testable deliverables are marked as 'PASS' by BA/QA team.

**[Back to Table of Contents](../README.md)**