General coding style
====================
The following is the recommended style for coding. MFDC is a small company with a good deal of flexibility so we don't really want to enforce the below too much. Most of the below is really just habits we've picked up as a company over the years. The following is aimed at providing a suitable consistent environment over projects and between programmers. We promise not to get mad if you use something different from the below if it can be justified. Sometimes some projects have different styles so the below is by no means definitive.

* **Indentation** - [One-True-Brace / 1TBS style](https://en.wikipedia.org/wiki/One_true_brace#Variant:_1TBS). While other styles occasionally exist and are tolerated (albeit grudgingly) 1TBS is preferred.
* **[Goto statements](https://en.wikipedia.org/wiki/Goto)** - No. None. At all. Under any circumstances. You know the bit about us not getting mad if it can be justified - this does not apply here. Violence will ensue. There will be blood.
* **Global variables** - Contrary to what your computer science professor may have told you, global variables will not cause Satan to reclaim the earth. Sometimes they are justified. Don't be afraid to use them.
* **Inline documentation** - Please learn about [phpDoc](http://phpdoc.org/), [jsdoc](https://github.com/jsdoc3/jsdoc) or one of the other inline documentation systems. See any of our existing projects for examples. Its not necessary to document every little thing, but documentation should be atomic - i.e. its either there and complete (listing all `@param` and `@return` parameters at a minimum) or not present at all. *Do not have half-completed documentation* as this is often worse than having none at all.
* **No pointless documentation** - Adding to the above point, its not necessary to document every little function in your code. The key question is to ask yourself if you were to read the function name + arguments with no background in the project could you understand it? If the answer is no add some inline documentation otherwise its optional.
* **Globals are ok** - Despite what your CS lecturers told you: yes they are ok just dont overdo them.
* **Ternarys are ok** - Most languages support [ternarys](https://en.wikipedia.org/wiki/%3F:) and they generally make the code less verbose. If you have a simple If..then...else statement that just sets one variable you should probably look into how to use them.

See each individual project type in the next section for language specific styles.


**[Back to Table of Contents](../README.md)**
