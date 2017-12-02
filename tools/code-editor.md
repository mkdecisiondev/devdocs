# Code editor

Code editors are powerful tools, so it is important that you use a good one and learn to use it effectively. You must install [Visual Studio Code](https://code.visualstudio.com/) and use it for at least a week. If you find that you prefer another editor, it must provide similar performance and features as VS Code.

## Performance

Performance is important. Your editor should not hang when you open it. It should not hang when you open a project. It should be responsive when you are editing code and switching between tabs. If you have performance issues with VS Code you should ideally acquire a better computer. If your computer cannot run VS Code well, you should use [Sublime Text](https://www.sublimetext.com/).

## Features

Advanced code editors can make it much easier to write correct and consistent code.

* [Autocomplete](https://code.visualstudio.com/docs/editor/intellisense)
* [Advanced language features](https://code.visualstudio.com/docs/languages/javascript)
* [Code linting](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

All following instructions will be for VS Code. Any editor that does not have similar configurability should be avoided.

## Installation and configuration

### Prerequisites

1. Install [Node.js](https://nodejs.org) (v8 recommended)
1. Install [ESLint](https://eslint.org/): `npm i -g eslint`
1. Install [HTMLHint](http://htmlhint.com/): `npm i -g htmlhint`
1. Install [VS Code](https://code.visualstudio.com/Download)

### Configuration

1. indentation: tabs
1. line endings: Unix (linefeed, `\n`)
1. file encoding: utf-8
1. insert final newline: yes (ensure all files end with a blank line)
1. trim final newlines: yes (ensure all files end with a single blank line, no more)
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

### Install extensions

Click the extensions icon (bottom one of the 5 icons at the top left) and install the following extensions:

1. ESLint
1. HTMLHint
1. Path Intellisense
1. Git Blame
