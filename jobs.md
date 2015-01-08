Job descriptions
================
This section is to define a few categories developers can fit into. Sometimes a task may require multiple of these job descriptions, sometimes they may all the same person.


Business Analysts (BAs)
-----------------------
FIXME


Developer
---------
> Beauty is more important in computing than anywhere else in technology because software is so complicated. Beauty is the ultimate defence against complexity.
> - David Gelernter

FIXME


DevOps
------
> Remember, as a developer, the cost of breaking a live system to a client is: 
>  * The sum of wages of staff who can't do their job
>  * The opportunity cost in time for the company - what they could be making if it weren't for the system being down. 
>  * The loss of user trust in the system. 
>  * Any data loss that might have occurred. 
> 
> So... Since a day's downtime could run into thousands of dollars of expenses even for a minor fault, don't break the system.

DevOps is primarily a position specializing in the deployment and maintenance of live systems in an on-going basis (i.e. not just deploy and forget like most website uploads).

For larger projects where MFDC is in some way involved with development and making sure the thing still works (aka operations) there are a number of additional considerations that need to be made. Fundamentally, developers are no longer just builders who complete a task list, but are instead actively responsible for achieving two goals: Making sure existing functionality is not interrupted, making sure new deployments are achieved and most importantly, users are happy. 


**Requisites**

All DevOps people need to:

* Know enough Linux to install, say, a LAMP server
* be able to use a test-editor via the command line
* Use SSH, cron, tar
* Use the database via the command line
* Understand makefiles
* Have strong communication skills


**Branching**

MFDC doesn't have an official position on branching, but its often helpful when making significant system changes to branch the system with Git, achieve the changes and then re-merge them back into the main branch. _However_, make sure all the developers on the project understand this, lack of familiarity with branching by a junior developer will cause merry hell. 


**Initial deployment**

Once the client is happy for the system to go live:

1. Pull to server, make database, run install script. If there's anything more complicated, rethink it. Deployment has to be simple because it's where things to badly wrong. 
2. Confirm deployment: Make sure **everything** is working. Ideally unit-tests, failing that, a manual observation. 
3. Monitor response: Check with client/operations, monitor in the immediate few days of use the feedback. 


**Communication - the art of modifying live systems**

As a developer, all changes to live systems must be made known to the operations team. _Anything_ which affects the function of a website which is already in use must be run by them, even if only cosmetic. 


**Database changes**

Any modification to the database will critically change the live system. Running the simple makefile is not possible due to their being live data in the database. Field type changes are dangerous because there is the potential to lose live data. Therefore the entire issue is one which must be carefully monitored and performed flawlessly. 

1. Database Schema changes are all critically important. Track every modification of an existing system because deployment of the software without corresponding live schema updates is critical.
2. Ensure database backups before any modifications (as well as generally)
3. Create database update SQL files with a list of updates to run on the production server and _test them_.


**Disaster Fallout and blame**

Things break, when they do its the DevOps responsibility to fix it immediately, no matter who's at fault, the time of day or who's on call. Then find out where, how, when and what the lead-up to the event was.

* Remember everything is traceable through Git, so it's easy to figure out who wrote the line of code which broke the server, however, remember that whoever was in charge of deployment is ultimately responsible for the live build.
* After fixing, discuss what went wrong with all stakeholders and discuss how to avoid this in future. Future prevention is more important than blame. 


SysAdmin
--------
> UNIX was not designed to stop its users from doing stupid things, as that would also stop them from doing clever things.
> - Doug Gwyn

FIXME


Quality Control (QA)
--------------------
> Debuggers don't remove bugs. They only show them in slow motion.

FIXME


Support
-------
> PICNIC (Problem in chair not in computer)
> - General use acronym indicating a user is at fault

IT support can broadly be separated into three tiers: 1 though 3.

| Tier   | Also called                   | Description                                       |
|--------|-------------------------------|---------------------------------------------------|
| Tier 1 | Helpdesk / Helldesk           | First point of contact for the general public. Common questions and queries |
| Tier 2 | Troubleshooting / Deployment  | Generally 'the unseen' of IT. These are either the superiors (in experience) to Tier 1s or people setting up architectures (e.g. outfitting an office with hardware).
| Tier 3 | SysAdmins                     | Someone who normally administers the most complex systems in the infrastructure.
| Tier 4 | Externals                     | Not part of the usual Tier 1 - 3 this tier can be referred to when the problem exists outside of the infrastructure e.g. external vendors.


