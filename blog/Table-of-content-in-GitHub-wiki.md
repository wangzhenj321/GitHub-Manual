## Question
If you look here: [Stack Overflow](http://en.wikipedia.org/wiki/Stack_Overflow)

You'll notice there's a little "Content" section, if you click on one of the links, it will send you to a specific section on the page.

How do I do this in GitHub wiki? With Markdown or whatever they use?

## Answer
It is nicely demonstrated in the Table of Contents of the [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).
```
##### Table of Contents  
[Headers](#headers)  
...
## Headers
```
If you hover over a Header in a GitHub Markdown file, you'll see a little link simple to the left of it, you can also use that link. The format for that link is `<project URL>#<header name>`. The `<header name>` must be all lower case. While creating the table of contents, you'll need to use this `<header name>` as `headers` of `[Headers](#headers)`. Then the link will be automatically created. 

## References
1. [How do I create some kind of table of content in GitHub wiki?](https://stackoverflow.com/questions/18244417/how-do-i-create-some-kind-of-table-of-content-in-github-wiki)