# CSS coding standards

1. Avoid unnecessary quotes, use single quotes when quotes are necessary
1. Class names should be lowercase dasherized
1. One selector per line
1. Use [`hsl()/hsla()`](http://devdocs.io/css/color_value#hsla()) for colors
1. Use `normal/bold` (instead of 100, 400, 700, etc) for `font-weight`
	1. Exception: if you are using a specific font that supports more weights and you need to use one of them

## Naming things

For CSS classes and custom properties (variables), follow these naming conventions.

* Dasherize: `main-box` (not `mainBox`)
* Use a descriptive noun as the name: `main-box`, `dialog`, `user-info`
* Adding extra information and qualifiers:
	* Adjectives should come _after_ the none: `main-box-small` (not `small-main-box`)
	* Qualifying nouns should be added as a prefix: `customer-main-box` (not `main-box-customer`)

### Examples

```css
:root {
	--font-size: 16px; /* 'default' modifier not necessary, the name is generic and can be understood to be the default */
	--font-size-small: 14px; /* 'small' is an adjective and goes after the noun it modifies */
	--button-font-size: 20px; /* 'button' is a noun that qualifies this as a specific font size; use 'button' as prefix */
}
```
