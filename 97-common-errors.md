---
title: Appendix A – Common Errors
layout: page
---

<!-- I like the idea of introducing common errors that they will see. When they are relevant, rather than in one lump, although we might have a chapter (appendix?) on debugging where everything is lumped together?? -->

## General Tips
* Use the line number provided with the error to find where in your code the error is occurring.
* The error may not be on the line that reports the error. Check the line directly above for errors, and check other lines that use variables being referenced by the code on these two lines.

```
SyntaxError: Unexpected identifier.
```
* Check that your strings are closed correctly with matching quotes, and no quote marks are breaking the string half-way through.
* Escape quote marks that are intended to appear within the string using `\` backslashes: `'Don\'t forget!'`
