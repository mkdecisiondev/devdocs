# Best practices: CSS

## Using variables

The goal when using variables is to create code that is reusable and configurable. Strive to find a balance between
the two. The quality of being generic tends to promote reuse, but at an extreme something too generic will get overused
and if it is modified it will have overreaching effects. The quality of being specific enables fine-grained
customization, but at an extreme having 500 highly-specific configurable options makes customization too cumbersome.

Look at the design of a UI and pick out similar elements. Rather than creating variables for every single element's
border, font, colors, etc, create groups of similar elements. Ask yourself: if the user changes this property for this
element, are they likely to make the same change for other elements (to maintain consistent visuals)? If the answer is
yes, then group all of those elements and use the same variable.
