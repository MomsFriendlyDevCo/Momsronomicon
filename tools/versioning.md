Versioning - Git
================

> And when I *do* get involved with the code, it's not because it's "cool", it's because it broke, and you'll find me cursing the people who wrote it, and questioning their parentage and that of their pets
> - [Linus Torvalds](http://meta.slashdot.org/story/12/10/11/0030249/linus-torvalds-answers-your-questions)

Git is the de-facto version control system of choice in MFDC. [GitHub](https://github.com) the preferred distribution server.

General tips:

* Pull as often as possible to prevent future merging problems - 90% of issues with Git are due to a coder not pulling enough and working on already-patched code.
	* Always pull before starting a new feature/bugfix

* Commit as often as possible. Its better to commit small chunks that fix individual errors than one large commit which will take ages to unpick if someone else only wants one feature of your commit.
	* Learn to use `git add -p` (git add patch), this allows you to selectively add bits of your code to a commit. This is extremely useful to pick out bits of code from an exceptionally large patch and label them correctly.

* Commit comments are mandatory. This is enforced by Git anyway but please try to be at least a little descriptive of your commit. Generally we go with the 'one line description' method of committing (don't go nuts) but multiple lines are advised if you use any of the below prefixes (one per line)
	* Some example prefixes we find useful:
		* `CLIENT: xxx` - The client asked for something specific even if the dev thinks its stupid
		* `BUGFIX: xxx` - This commit includes a correction to a bug
		* `REFACTOR: xxx` - This commit includes code cleanup which does not effect the operation of the code (improved comments, indentation fixes etc.)
		* `REVERT: xxx` - Revert of a previous commit (Git uses this prefix automatically anyway)
* Branching is only necessary on 'live' projects or if you are making an especially large commit that may break things. If the project is being developed and it is not mission critical or live then committing to master is good as it allows everyone to test everyone elses code.
* Do not push broken code _ever_, under any circumstances. A push should indicate that the code you are pushing has been completed and is ready at least for testing. Buggy or broken code that breaks everything will result in the WOM (Wrath of Matt).


**[Back to Table of Contents](../index.md)**
