# Spike

[Spike](https://www.spike.cf/) is a [static site generator](https://www.sitepoint.com/7-reasons-use-static-site-generator/) that creates HTML/JS/CSS from data and templates.

## Templating: reshape

Spike uses [reshape](https://reshape.ml/) ([GitHub](https://github.com/reshape/reshape)) for templating.

We are using the features provided by the following plugins:

1. [include](https://github.com/reshape/include)
1. [component](https://github.com/mkdecisiondev/reshape-component)
1. [layouts](https://github.com/reshape/layouts)
1. [expressions](https://github.com/reshape/expressions)

## CSS: PostCSS

Spike uses [PostCSS](http://postcss.org/) ([GitHub](https://github.com/postcss/postcss)) for CSS.

We are using the features provided by the following plugins:

1. [autoprefixer](https://github.com/postcss/autoprefixer)
1. [calc](https://github.com/postcss/postcss-calc)
1. [custom-media](https://github.com/postcss/postcss-custom-media)
1. [custom-properties](https://github.com/postcss/postcss-custom-properties)
1. [import](https://github.com/postcss/postcss-import)
1. [nesting](https://github.com/jonathantneal/postcss-nesting)
1. [responsive-type](https://github.com/seaneking/postcss-responsive-type)

### cssnano

We use [cssnano](http://cssnano.co/optimisations/) to optimise CSS for deployment. Keep in mind that production builds are different from development builds (no cssnano), so code that works during development may not work in production. One CSS issue in particular to be careful of is that each individual CSS file is handled independently. You may logically structure your application CSS so that one CSS file is dependent on another but PostCSS and cssnano have no knowledge of this. As a result cssnano may remove unused code from `fileA.css` that you intend to use in `fileB.css`. To avoid this it is recommended to create a common base CSS module, e.g. `_common.css` that imports font declarations, variables, and global styles. This common module can be imported into each page-level CSS file to ensure that all dependencies are present.

Example:
```
assets/
    css/
        _common.css
        _fonts.css
        _global.css
        _variables.css
        main.css
src/
    index.html
    index.css
```

`_common.css:`

```css
@import '_fonts.css';
@import '_variables.css';
@import '_global.css';
```

`main.css:`

```css
@import '_common.css';
```

`index.css:`

```css
@import '../assets/css/_common.css';
```

## MK Decision Spike template

Our projects are based on [mk-spike-template](https://github.com/mkdecisiondev/mk-spike-template). Read its [documentation](https://github.com/mkdecisiondev/mk-spike-template#readme) to understand the project structure.
