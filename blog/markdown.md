**Table of Contents**

- [What’s Markdown?](#whats-markdown)

- [Basic Syntax](#basic-syntax)

- [Extended Syntax](#extended-syntax)

- [CommonMark](#commonmark)

- [GitHub Flavored Markdown Spec](#github-flavored-markdown-spec)

- [Emoji Markup](#emoji-markup)

## [What’s Markdown?](https://www.markdownguide.org/getting-started)

**Markdown** is a lightweight markup language that you can use to add formatting elements to plaintext text documents. Created by John Gruber in 2004, **Markdown** is now one of the world’s most popular markup languages.

## [Basic Syntax](https://www.markdownguide.org/basic-syntax)

- **Headings**

    To create a heading, add number signs (`#`) in front of a word or phrase. The number of number signs you use should correspond to the heading level. 

- **Paragraphs**

    To create paragraphs, use a blank line to separate one or more lines of text. You should not indent paragraphs with spaces or tabs.

- **Line Breaks**

    To create a line break (`<br>`), end a line with two or more spaces, and then type return.

- **Emphasis**

    - **Bold**
    
        To bold text, add **two** asterisks or underscores before and after a word or phrase. To bold the middle of a word for emphasis, add two asterisks without spaces around the letters.
    
    - **Italic**
    
        To italicize text, add **one** asterisk or underscore before and after a word or phrase. To italicize the middle of a word for emphasis, add one asterisk without spaces around the letters.
    
    - **Bold and Italic**
    
        To emphasize text with bold and italics at the same time, add **three** asterisks or underscores before and after a word or phrase.

- **Blockquotes**

    To create a blockquote, add a `>` in front of a paragraph.
    
    - **Blockquotes with Multiple Paragraphs**
    
        Blockquotes can contain multiple paragraphs. Add a `>` on the blank lines between the paragraphs.
    
    - **Nested Blockquotes**
    
        Blockquotes can be nested. Add a `>>` in front of the paragraph you want to nest.
    
    - **Blockquotes with Other Elements**
    
        Blockquotes can contain other Markdown formatted elements. Not all elements can be used — you’ll need to experiment to see which ones work.

- **Lists**

    - **Ordered Lists**
    
        To create an ordered list, add line items with numbers followed by periods. The numbers don’t have to be in numerical order, but the list should start with the number one.
    
    - **Unordered Lists**
    
        To create an unordered list, add dashes (`-`), asterisks (`*`), or plus signs (`+`) in front of line items. Indent one or more items to create a nested list.
    
    - **Adding Elements in Lists**
    
        To add another element in a list while preserving the continuity of the list, indent the element four spaces or one tab.
        
        > **Code blocks are normally indented four spaces or one tab. When they’re in a list, indent them eight spaces or two tabs.**

- **Code**

    To denote a word or phrase as code, enclose it in tick marks (\`).
    
    - **Escaping Tick Marks**
    
        If the word or phrase you want to denote as code includes one or more tick marks, you can escape it by enclosing the word or phrase in double tick marks (\`\`).
    
    - **Code Blocks**
    
        > **To create code blocks, indent every line of the block by at least four spaces or one tab.**

- **Horizontal Rules**

    To create a horizontal rule, use three or more asterisks (`***`), dashes (`---`), or underscores (`___`) on a line by themselves.

- **Links**

    To create a link, enclose the link text in brackets and then follow it immediately with the URL in parentheses.
    
    - **Adding Titles**
    
        You can optionally add a title for a link. This will appear as a tooltip when the user hovers over the link. To add a title, enclose it in parentheses after the URL.
        
        ```
        My favorite search engine is [Duck Duck Go](https://duckduckgo.com "The best search engine for privacy").
        ```
    
    - **URLs and Email Addresses**
    
        To quickly turn a URL or email address into a link, enclose it in angle brackets.
    
    - **Formatting Links**
    
        To emphasize links, add asterisks before and after the brackets and parentheses.
    
    - :question: **Reference-style Links**

- **Images**

    To add an image, add an exclamation mark (`!`), followed by alt text in brackets, and the path or URL to the image asset in parentheses. You can optionally add a title after the URL in the parentheses.
    
    ```
    ![Tux, the Linux mascot](/assets/images/tux.png)
    ```
    
    > - For convenience, set the alt text to be empty.
    > 
    > - In Github markdown, it's better to use the following way which can control the size of image.
    > 
    >   ```
    >   <img src="/assets/images/tux.png" width="100%">
    >   ```
    
    - **Linking Images**
    
        To add a link to an image, enclose the Markdown for the image in brackets, and then add the link in parentheses.
        
        ```
        [![An old rock](/assets/images/shiprock.jpg "New Mexico")](https://www.flickr.com/photos/in/photolist-bXMYv)
        ```

- **Escaping Characters**

    To display a literal character that would otherwise be used to format text in a Markdown document, add a backslash (`\`) in front of the character.

## [Extended Syntax](https://www.markdownguide.org/extended-syntax)

Extended syntax isn’t available in all Markdown applications. You’ll need to check whether or not the **lightweight markup language** your application is using supports extended syntax. If it doesn’t, it may still be possible to enable extensions in your **Markdown processor**.

> Many of the most popular Markdown applications use one of the following lightweight markup languages:
> 
> - CommonMark
> - GitHub Flavored Markdown (GFM)
> - Markdown Extra
> - MultiMarkdown

- **Tables**

    To add a table, use three or more hyphens (`---`) to create each column’s header, and use pipes (`|`) to separate each column. You can optionally add pipes on either end of the table.
    
    - **Alignment**
    
        You can align text in the columns to the left, right, or center by adding a colon (`:`) to the left, right, or on both side of the hyphens within the header row.
    
    - **Formatting Text in Tables**
    
        You can format the text within tables. For example, you can add links, code, and emphasis. You can’t add headings, blockquotes, lists, horizontal rules, images, or HTML tags.
    
    - **Escaping Pipe Characters in Tables**
    
        You can display a pipe (`|`) character in a table by using its HTML character code (`&#124;`).

- **Fenced Code Blocks**

    The basic Markdown syntax allows you to create code blocks by indenting lines by four spaces or one tab. If you find that inconvenient, try using fenced code blocks. Depending on your Markdown processor or editor, you’ll use three tick marks (\`\`\`) or three tildes (`~~~`) on the lines before and after the code block.
    
    - **Syntax Highlighting**
    
        Many Markdown processors support syntax highlighting for fenced code blocks. This feature allows you to add color highlighting for whatever language your code was written in. To add syntax highlighting, specify a language next to the tick marks before the fenced code block.

- **Footnotes**

    Footnotes allow you to add notes and references without cluttering the body of the document. When you create a footnote, a superscript number with a link appears where you added the footnote reference.
    
    ```
    Here's a simple footnote,[^1] and here's a longer one.[^bignote]

    [^1]: This is the first footnote.

    [^bignote]: Here's one with multiple paragraphs and code.

        Indent paragraphs to include them in the footnote.

        `{ my code }`

        Add as many paragraphs as you like.
    ```

- **Heading IDs**

    Many Markdown processors support custom IDs for headings — some Markdown processors automatically add them. Adding custom IDs allows you to link directly to headings and modify them with CSS. To add a custom heading ID, enclose the custom ID in curly braces on the same line as the heading
    
    ```
    ### My Great Heading {#custom-id}
    ```
    
    - **Linking to Heading IDs**
    
        You can link to headings with custom IDs in the file by creating a standard link with a number sign (#) followed by the custom heading ID.
    
    > **Linking to automatically added Heading IDs**
    > 
    > ```
    > ##### Table of Contents  
    > [Headers](#headers)  
    > ...
    > ## Headers
    > ```
    > 
    > If you hover over a Header in a GitHub Markdown file, you'll see a little link simple to the left of it, you can also use that link. The format for that link is `<project URL>#<header name>`. The `<header name>` must be all lower case. While creating the table of contents, you'll need to use this `<header name>` as `headers` of `[Headers](#headers)`. Then the link will be automatically created.

- **Definition Lists**

    Some Markdown processors allow you to create definition lists of terms and their corresponding definitions. To create a definition list, type the term on the first line. On the next line, type a colon followed by a space and the definition.
    
    ```
    First Term
    : This is the definition of the first term.

    Second Term
    : This is one definition of the second term.
    : This is another definition of the second term.
    ```

- **Strikethrough**

    You can “strikethrough” words by putting a horizontal line through the center of them. To strikethrough words, use two tilde symbols (`~~`) before and after the words.

- **Task Lists**

    Task lists allow you to create a list of items with checkboxes. In Markdown applications that support task lists, checkboxes will be displayed next to the content. To create a task list, add dashes (`-`) and brackets with a space (`[ ]`) in front of task list items. To select a checkbox, add an `x` in between the brackets (`[x]`).

- **Automatic URL Linking**

    Many Markdown processors automatically turn URLs into links.
    
    - **Disabling Automatic URL Linking**
    
        If you don’t want a URL to be automatically linked, you can remove the link by denoting the URL as code with tick marks.

## [CommonMark](https://commonmark.org/)

It’s a plain text format for writing structured documents, based on formatting conventions from email and usenet.

## [GitHub Flavored Markdown Spec](https://github.github.com/gfm/)

**GitHub Flavored Markdown**, often shortened as **GFM**, is the dialect of Markdown that is currently supported for user content on GitHub.com and GitHub Enterprise.

This formal specification, based on the **CommonMark Spec**, defines the syntax and semantics of this dialect.

**GFM** is a strict superset of **CommonMark**. All the features which are supported in GitHub user content and that are not specified on the original CommonMark Spec are hence known as extensions, and highlighted as such.

While **GFM** supports a wide range of inputs, it’s worth noting that GitHub.com and GitHub Enterprise perform additional post-processing and sanitization after GFM is converted to HTML to ensure security and consistency of the website.

## [Emoji Markup](https://gist.github.com/rxaviers/7360908)
