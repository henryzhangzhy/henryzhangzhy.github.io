---
author: Henry
topic: Geek
---

A reference for markdown language.

structure

# title \#
## second level title \#\#

### list
- a '\-' followed by a space
- a '\-' another one

1. numbered list
3. actual number doesn't matter, just a number

   properly indented paragraph, with blank line and space.
   - another sublist
   - here
   * \* works for unordered lists
   + \+ works the same
   - \- as well

### format

- _emphasis_: \_emphasis\_ or \*emphasis\*
- __strong emphasis__: \_\_strong emphasis\_\_ or \*\*strong emphasis\*\*
- **combined _emphasis_**: \*\*combined \_emphasis\_\*\*
- ~~strike through~~: \~\~strike through\~\~

### code

- \`inline code\` `inline code`

- \`\`\`python

  code block

  \`\`\`

  ```python
  square = [x*2 for x in range(10)]
  ```

### links

- [Google](https://www.google.com): \[Google\]\(https://www.google.com\)

- [Google](https://www.google.com "Google Homepage"): \[Google\]\(https://www.google.com \"Google Homepage\"\)

- [reference style][reference]: \[reference style\]\[reference\]

- URLs and URLs in angle brackets will automatically get turned into links. 
http://www.example.com or <http://www.example.com> and sometimes 
example.com (but not on Github, for example).

[reference]: https://www.reddit.com
- \[reference\]: https://www.reddit.com


- Inline-style: 
![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")

- Reference-style: 
![alt text][logo]

[logo]: https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 2"


### Block Quate

- > block quate
  > continue
  
  Quote break
  
  > anther quaote that is very long long long long long long long long long long long long long long.

---

### Reference

Adapted from 
[Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) by [adam-p](https://github.com/adam-p)

Licence: [CC-BY](https://creativecommons.org/licenses/by/3.0/)