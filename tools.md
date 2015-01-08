Tools
=====
> The easiest method to compute newbie programmer specific hash is to sit them in front of VI and ask them to quit.
> - MC, The author

Design tools
------------
We have generally found [Balsamiq mockups](http://balsamiq.com) to be the go-to prototyping system as it provides an excellent user interface capable of generating UI's with little overhead.

For ERD diagrams [LucidChart](http://www.lucidchart.com) is the best option we have found so far.

Everything else should be constrained to standard office tools - MS Office / LibreOffice etc.


Editors
-------
> I use emacs, which might be thought of as a thermonuclear word processor. It was created by Richard Stallman; enough said. It is written in Lisp, which is the only computer language that is beautiful. It is colossal, and yet it only edits straight ASCII text files, which is to say, no fonts, no boldface, no underlining. In other words, the engineer-hours that, in the case of Microsoft Word, were devoted to features like mail merge, and the ability to embed feature-length motion pictures in corporate memoranda, were, in the case of emacs, focused with maniacal intensity on the deceptively simple-seeming problem of editing text
> - Neil Stephenson (In the beginning was the command line)

> Vi is a subset of evil
> - Anon.

Despite any fancy pre-conceived notions there are only two text editors - [Emacs](https://www.gnu.org/software/emacs) and [Vi](http://www.vim.org). All other editors are shallow copies of one of these two - usually implementing less features. These editors pre-date the internet and as such have 

Thats not to say that other editors such as [Notepad++](http://www.notepad-plus-plus.org), [TextPad](http://www.textpad.com/), [Sublime Text](http://www.sublimetext.com) or the new hip-and-trendy [Atom](https://github.com/atom/atom) are necessarily bad, just that they more-or-less duplicate the functionality of either Emacs or Vi and in most ways not to the full degree.


Version control - Git
---------------------
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
