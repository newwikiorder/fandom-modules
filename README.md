A collection of CSS rules for custom templates and components used on a variety of FANDOM communities.

# Importing
In order to import stylesheets from GitHub, you have to use [raw.githack](http://raw.githack.com/). Find the stylesheet in the `dist/` directory of this repo that you want to use, click the "Raw" button in the top right, then copy and paste that URL into raw.githack.

Import the *development* URL. The CDN services provided by raw.githack are not needed, as the contents of all imports are compiled into a single stylesheet by MediaWiki and periodically updated.

# How to contribute
First, download a local version:
```bash
git clone https://github.com/jacecotton/fandom-modules.git
```

Edit the `src/` director only. The source code uses SASS with the SCSS syntax.

Tell SASS to watch for any changes to the files and compile them to the `dist/` directory with the following command:

```bash
sass --watch src:dist --style compressed
```

After the compilation is complete, push to the repo:

```bash
git add .
git commit -m "Edit summary here"
git push -u origin master
```

# Style guide
This style guide does not include universal best practices for writing SASS and CSS (e.g. "comment frequently", "prefer classes to IDs", "don't use `!important`", etc.) However, universal best practices are still expected to be followed as much as possible, and the BEM naming convention is preferred.

## Pre-processing
The source code for these modules are written in SASS (with the SCSS syntax) and compiled to CSS. SASS watches the `src/` directory and outputs to the `dist/` directory in a minified format. Thus, a typical setup for this project looks like this:

```batch
$ sass --watch src:dist --style compressed
```

## Specificity management
FANDOM's default global stylesheet (Qualaroo.css) often uses selectors with high specificity; we can contend with this by being as specific (and only as specific) as Qualaroo is.

However, for maintainability purposes, the reason for high specificity should be logged in the source code with inline comments (using `//`, so they're stripped out when compiled).

For example:

```scss
// High specificity here to override Qualaroo defaults.
// Qualaroo selector: `.WikiaPage blockquote`
```

## Configurability
Some communities may wish to change aspects about certain modules. They can do this by simply overriding the relevant style rules in their own stylesheet.

To make this as easy as possible, certain properties should be variablized to minimize the amount of code needed. For example, if one wished to import the styles for Template:Quote and then change the color of the quotation marks, the following CSS would be applied:

```css
@import url("https://raw.githack.com/jacecotton/fandom-modules/master/dist/templates/quote.css");

:root {
  --pull-quote-mark-color: <new value here>;
}
```

And the source module would be written as:

```scss
:root {
  --pull-quote-mark-color: <default value here>;
}

.pull-quote {
  color: var(--quote-mark-color);
}
```

All custom properties should be added to a `:root` ruleset so they can easily be overriden in the community stylesheet. As such, the variable names should be prefixed with some sort of namespace; to keep it easy, try to stick to the element's actual classname, such as `--pull-quote-mark-color`.

Reminder, however, that custom properties need not be used at all in the importing stylesheet; one can simply override the actual CSS if they wish.