Editors
=======

> I use emacs, which might be thought of as a thermonuclear word processor. It was created by Richard Stallman; enough said. It is written in Lisp, which is the only computer language that is beautiful. It is colossal, and yet it only edits straight ASCII text files, which is to say, no fonts, no boldface, no underlining. In other words, the engineer-hours that, in the case of Microsoft Word, were devoted to features like mail merge, and the ability to embed feature-length motion pictures in corporate memoranda, were, in the case of emacs, focused with maniacal intensity on the deceptively simple-seeming problem of editing text
> - Neil Stephenson (In the beginning was the command line)


The following sections list code editors sorted from most popular to least by the Devs at MFDC:


Atom
----
Project: [The Atom Editor](https://github.com/atom/atom)

Recommended packages (all available from the `Preferences > Packages` UI:

* [Triple-Folds](https://atom.io/packages/triple-folds) package to get code folding working
* [atom-sublime-select](https://atom.io/packages/sublime-style-column-selection) package to enable vertical editing (Refer to package for OS controls)

As Atom is client-side only you may be interested in [remote mounting with SSH] to edit text on machines other than your own, like servers.

Note: Atom uses soft tabs (ie two spaces) by default, with MFDC being a tabs friendly company this raises a few problems...

To turn it off, navigate to settings:
Edit -> Preferences

1. Uncheck 'Soft Wrap At Preffered Line Length'
2. Change Tab Type to Hard
  



### VI / VIM

> Vi is a subset of evil
> - Anon.

MC's preferred editor of choice. It may not have been designed by the Devil but evil thoughts are certainly at the forefront of the mind of any who begin to use it. Needless to say that VI* is a **very** difficult editor to master, its difficulty matched by its power.

VI has the added advantage that it is part of the standard set of Unix editors and can always be found on any server without any additional tools.


### Other choices

* [Notepad++](http://www.notepad-plus-plus.org) (Win)
* [TextPad](http://www.textpad.com/) (Win)
* [Sublime Text](http://www.sublimetext.com) (Win, Mac)


**[Back to Table of Contents](../README.md)**
