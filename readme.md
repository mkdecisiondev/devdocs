# MK Decision Developer Documentation

In order to effectively work on programming projects with a team of developers it is important to know the relevant technologies and tools, and to follow standards and conventions that make it easier to collaborate.

## Code editor

Code editors are powerful tools, so it is important that you use a good one and learn to use it effectively. You must install [Visual Studio Code](https://code.visualstudio.com/) and use it for at least a week. If you find that you prefer another editor, it must provide similar performance and features as VS Code.

### Performance

Performance is important. Your editor should not hang when you open it. It should not hang when you open a project. It should be responsive when you are editing code and switching between tabs. If you have performance issues with VS Code you should ideally acquire a better computer. If your computer cannot run VS Code well, you should use [Sublime Text](https://www.sublimetext.com/).

### Features

Advanced code editors can make it much easier to write correct and consistent code.

* [Autocomplete](https://code.visualstudio.com/docs/editor/intellisense)
* [Advanced language features](https://code.visualstudio.com/docs/languages/javascript)
* [Code linting](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

All following instructions will be for VS Code. Any editor that does not have similar configurability should be avoided.

### Editor configuration

#### Prerequisites

1. Install [Node.js](https://nodejs.org)
1. Install [ESLint](https://eslint.org/): `npm i -g eslint`
1. Install [HTMLHint](http://htmlhint.com/): `npm i -g htmlhint`
1. Install [VS Code](https://code.visualstudio.com/Download)

#### Configuration

1. indentation: tabs
1. file encoding: utf-8
1. line endings: Unix (linefeed / '\n')
1. insert final newline: yes (ensure all files end with a blank line)
1. trim trailing newlines: yes (ensure all files end with a single blank line, no more)
1. trim trailing whitespace: yes (ensure all lines end with a non-whitespace character)

You can press `Ctrl + ,` to open User Settings and paste the following in the right pane:

```json
{
    "editor.insertSpaces": false,
    "files.eol": "\n",
    "files.encoding": "utf8",
    "files.insertFinalNewline": true,
    "files.trimFinalNewlines": true,
    "files.trimTrailingWhitespace": true,
}
```

#### Install extensions

Click the extensions icon (bottom one of the 5 icons at the top left) and install the following extensions:

1. ESLint
1. HTMLHint
3. Git Blame

## Programming languages

### HTML

You should be able to create a web page with a good understanding and use of available HTML elements. If you already know HTML reasonably well, review the [list of elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element) and ensure you know how to use most of them.

If you need to learn HTML from scratch, refer to these resources:

* [MDN: Introduction to HTML](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML)
* [Learn to Code HTML & CSS](https://learn.shayhowe.com/html-css/)

### CSS

You should be understand how to use CSS to control a web page's presentation. If you already know CSS reasonably well, review the [MDN CSS reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference) and ensure you know how to use most of it.

If you need to learn CSS from scratch, refer to these resources:

* [MDN: Introduction to CSS](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS)
* [Learn to Code HTML & CSS](https://learn.shayhowe.com/html-css/getting-to-know-css/)

### JavaScript

* [Eloquent JavaScript](http://eloquentjavascript.net/)
* [MDN JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
* [MDN JavaScript Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference)
* [MDN Browser and DOM Reference](https://developer.mozilla.org/en-US/docs/Web/API)

## Development tools

### Documentation

If you don't know something, refer to the documentation. If you still don't know how to use it, discuss with other developers or look for tutorials or blogs that explain it.

1. [DevDocs](http://devdocs.io/) is a compilation of a lot of web-related documentation
1. [Mozilla Developer Network](https://developer.mozilla.org/en-US/) is an excellent source for a lot of web-related documentation (DevDocs actually pulls much of its info from here)

### Visual Studio Code

It's important to know how to use your editor effectively and take advantage of advanced features. To get started, click 'Help' -> 'Interactive Playground'. Also learn the following:

1. [Code completetion](https://code.visualstudio.com/docs/editor/intellisense)
1. [Multiple selections](https://code.visualstudio.com/docs/editor/codebasics#_multiple-selections-multicursor)
1. [Search](https://code.visualstudio.com/docs/editor/codebasics#_search-across-files)
1. [Tips and tricks](https://code.visualstudio.com/docs/getstarted/tips-and-tricks)
1. [Emmet](https://code.visualstudio.com/docs/editor/emmet)

### Git

1. [Git book](https://git-scm.com/book/en/v2) (chapters 1-3, 5, 6-8)
1. [Feature branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow)
1. [Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
1. [Rebase workflow](http://kensheedlo.com/essays/why-you-should-use-a-rebase-workflow/)

### GitHub

### Node.js and npm

## Standards

### Common

### HTML

### CSS

### JavaScript
