# HTML

You should be able to create a web page with a good understanding and use of available HTML elements. If you already know HTML reasonably well, review the [list of elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element) and ensure you know how to use most of them.

If you need to learn HTML from scratch, refer to these resources:

* [MDN: Introduction to HTML](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML)
* [Learn to Code HTML & CSS](https://learn.shayhowe.com/html-css/)

## Advanced topics

### HTML in strings

1. Don't do it
1. Seriously, it's a very bad idea
1. If you have a *very compelling* reason to do it:
	1. Compose the HTML in your editor, pay attention to linting messages and ensure it's valid HTML
		* Invalid HTML can break the build process in confusing ways
	1. Paste your HTML in [Code Beautify](https://codebeautify.org/htmlviewer/) or [HTML Minifier](https://kangax.github.io/html-minifier/) and click the "Minify" button
	1. Copy/paste the result into your JavaScript string
	1. [Validate](https://validator.w3.org/) the final built page
1. If you are updating HTML, you can paste it in [Code Beautify](https://codebeautify.org/htmlviewer/) and click the "Beautify" button, copy/paste the results to your editor, make changes, then bring it back and minify it
