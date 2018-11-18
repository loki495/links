## VIM

### macro across buffers
~~~~
You can put a buffer command (:b) in macros. For your case:

qqggD:b#^Mo^R":b#^Mq
Where "#" is the number of the buffer you want to switch to, ^M is pressing <Enter>, and ^R is pressing <C-r>.
~~~~

### [Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
