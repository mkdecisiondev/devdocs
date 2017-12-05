# Common coding standards

## Naming things

There are only two hard things in Computer Science: cache invalidation and naming things.
-- Phil Karlton

Names should be descriptive, but do try to keep them concise. Do not use short abbreviations like `btn`, `evt`, etc.

1. Keep names concise by using context appropriately
    1. If a `person` object has a `name` property, then `name` is perfect; `personName` is redundant
    1. Application context, module context, and even common shared social/cultural knowledge can provide context.
       Use your judgment and don't be shy to discuss with team members.
1. Start names with the main identifying information, then add any necessary modifiers
    1. e.g. `personHeight` not `heightOfPerson`
1. Use vertical whitespace (a single newline) to separate distinct blocks of code
