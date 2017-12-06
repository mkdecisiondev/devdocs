# Common coding standards

## Naming things

> There are only two hard things in Computer Science: cache invalidation and naming things.
> -- Phil Karlton

Names should be descriptive, but do try to keep them concise. Do not use short abbreviations like `btn`, `evt`, etc.

1. Keep names concise by using context appropriately
    1. If a `person` object has a `name` property, then `name` is perfect; `personName` is redundant
    1. Application context, module context, and even common shared social/cultural knowledge can provide context.
       Use your judgment and don't be shy to discuss with team members.
1. Start names with the main identifying information, then add any necessary modifiers
    1. e.g. `personHeight` not `heightOfPerson`

## Formatting

Many of the rules of prose apply to code as well. Think of how prose is organized in paragraphs and spaced out for
legibility when you are writing code.

1. Use spacing, both horizontal and vertical, to separate words and operations
1. Group focused blocks of logic together and use vertical spacing to separate distinct concepts or operations
1. Use indentation correctly to indicate structure and heirarchy

## File names

1. Files that will be served over HTTP should be named in lower-case dasherized
    1. HTML files that will be loaded directly
    1. JS files that will be referenced in a `script` element
    1. CSS files that will be referenced in a `link` element
1. Files that are modules, partials, or templates should be named with camel-case
    1. HTML files that are templates for a JS module should match the module name
    1. JS modules that export a constructor should begin with an upper-case letter; otherwise lower-case
    1. CSS files that are for a JS module should match the module name

## Rationale (This Seems Silly, Why Do We Do It??)

Underscored names are the worst of the lot in terms of legibility and ease of typing, so should generally be avoided.
Camel-case is legible, easy to type, and compatible with pretty much every programming language's naming restrictions,
so it is the first choice. HTML is case-insensitive, so using case-sensitive names introduces the potential for errors.
Dasherized CSS class names have become kind of a de facto standard, so we follow the trend for consistency's sake.
