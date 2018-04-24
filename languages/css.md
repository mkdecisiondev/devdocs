# CSS

You should understand how to use CSS to control a web page's presentation. If you already know CSS reasonably well, review the [MDN CSS reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference) and ensure you know how to use most of it.

If you need to learn CSS from scratch, refer to these resources:

* [MDN: Introduction to CSS](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS)
* [Learn to Code HTML & CSS](https://learn.shayhowe.com/html-css/getting-to-know-css/)
* [CSS Reference](http://cssreference.io/) with visual examples

## Advanced topics

* [`em` and `rem`](https://webdesign.tutsplus.com/tutorials/comprehensive-guide-when-to-use-em-vs-rem--cms-23984)
* [Stacking context](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)
* [Grid](https://gridbyexample.com/)

## CSS length units

CSS provides numerous ways of specifying dimensions. There is no single "right" way - each has its own purpose:

* `px`: small border dimensions (e.g. 1-2px) and image sizes
* `em`: use for specifying font size and padding relative to the element's font size
	* Use with caution: setting padding in `em` may initially seem to make sense, but on a page with sections that are aligned, either vertically or horizontally, if they have different font sizes and padding specified in `em` then they will have different padding values, causing a visual mis-alignment of content across sections.
* `rem`: use for specifying font size, margin, and padding relative to the whole page. Margin and padding should usually use `rem` to maintain consistency throughout the page.
* `%`: use for specifying width/height of an element that should adjust relative to its container
* `vh/vw`: use for specifying width/height of an element that should adjust relative to the viewport size
* `pt` (and others not listed): do not use
