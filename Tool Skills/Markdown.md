# Markdown

## Basic syntax:

**Headers:** Use `#` for creating headers. Good practise is to put blank lines before and after a header.

**Line Breaks:** To continue writing text in the next line, end the current line with two blank spaces and start writing in next line.

**Bold and Italic:** To emphasize a text use `*` or `_` before and after a text, two for bold, one for italic.

**Blockquotes:** When quoting text from another source or highlighting an important excerpt from notes use `>` at the beginning of a lines. Good practise is to put lines before and after a blockquote.

**Ordered lists:** Use `1.` at the beginning of a line to start an ordered list. To indent a list use 4 spaces or a tab at the beginning of a line.

**Unordered lists:** You can use `-`, `*` or `+` at the beginning of a line to start an unordered list. To add another paragraph in a current item of a list use indentation for every paragraph line.

**Code blocks:** Normally code blocks start indented 4 spaces or 1 tab. When in a list indent them 8 spaces or 2 tabs.

**Images:** Syntax for displaying images is `![img desc](url) "optional title"`. If image is local in project directory use `./images/example.jpg` instead of url. It is possible to use raw HTML for more control.

**Code:** To denote a word or phrase as code, enclose it with backticks `` ` ``. If a phrase has backticks enclose it with two backticks.

**Horizontal rules:** To create a horizontal rule (line) use three or more `***`, `---` or `___` on a line by themselves. Best practise is to put blank lines before and after a horizontal rule.

**Links:** Syntax for adding links to a text is `[text](url "optional tile")`. You can add a title for link that will appear when link is hovered. Encode spaces in URLs with `%20`, `(` with `%28` and `)` with `%29`.

**URLs & Emails:** To quickly turn url or email to a link use `<url/email>`.

**Reference-style links:** To keep markdown text clean from ugly long URLs you can use following syntax: `[linked text][label]` and usually immediatly after the paragraph or at the end of the document add link to the label `[label]: url/<url> "title"`. You can also enclose the title with `'` or `()`.

**Linking images:** Syntax for adding link to an image is `[![img desc](image url)"title"](link url)`

**Escaping characters:** To display a literal character that would otherwise be used format a text, add a `\` before a character.

## Extended sytax

**Tables:** Syntax for tables is:

    | column header 1 | column header 2 | column header 3 |
    | --- | ----- | ---- |
    | row text 1.1 | row text 1.2 | row text 1.3 |
    | row text 2.2 | row text 2.2 | row text 2.3 |
For text alignment in columns add `:` to the hyphens (`-`), to left it `| :--- |`, to right it `| ---: |`, to center it `| :---: |`.  
For displaying pipe charachter `|` in tables use its HTML code `&#124;`.

**Fenced code blocks:** To avoid indenting for code blocks, use `` ``` `` or `~~~` before and after a code block.

**Syntax highlighting:** For adding color highlighting for whatever language the code is written in, specify a language next to the backticks before the fenced code block `` ```lang ``.

**Strikethrough:** To strikethrough words use `~~` before and after the words.

**Task list:** For creating a task list start a line with `- [ ]` for empty checkbox or `- [x]` for a checked checkbox.

**Emojis:** To write emojis use `:emoji:`.

## HTML hacks

You can use HTML for all the things Markdown doesen't support.

