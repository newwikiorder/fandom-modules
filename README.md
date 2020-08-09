A collection of CSS rules for custom templates and components used on a variety of Fandom communities.

# Importing
In order to import stylesheets from GitHub, you have to use [jsdelivr.net](https://jsdelivr.net/). Find the file that you want to import to your wiki in the `dist/` directory of this repo, then replace `MODULE` in the following URL with its name:

```css
@import url("https://cdn.jsdelivr.net/gh/newwikiorder/fandom-modules@latest/dist/MODULE/MODULE.css");
```

Alternatively, you can import everything via the master file using this:

```css
@import url("https://cdn.jsdelivr.net/gh/newwikiorder/fandom-modules@latest/dist/master.css");
```

# How to edit the source
## Installing Sass and the Git CLI
This is a newbie section for editors who don't know what Sass is and how Git works. It is strongly recommended to research how it works for yourself, but some basic instructions are below. For intermediate web developers, skip to "Cloning and editing".

### Sass
Sass is a pre-processor for CSS that allows you to do things normal CSS can't (static variables, nesting, mixins, includes, interpolation, etc.) In order to do this, you have to install the Sass compiler, which takes Sass code and transforms it into CSS for you as you save each Sass file (`.scss`). Sass works in the terminal (Mac and Linux) or command prompt (Windows).

Install Sass here: https://sass-lang.com/install (note you may need to install Ruby first)

### Git CLI
The Git CLI allows you to pull code from Git repos (like this one) and then publish those changes back to the repo. Instructions for how to do this are below in "Cloning and editing" and "Publishing and updating".

Download Git here: https://git-scm.com/downloads

## Cloning and editing
First, download a local version to edit:
```bash
git clone https://github.com/newwikiorder/fandom-modules.git
```

All the files you'll actually edit are in the `src/` (source) directory. Sass will then compile these changes and add them as pure CSS to the `dist/` (distribution) directory. *Do not directly edit the distribution files*, as they will get overwritten by changes made to the source files.

Before you make any changes, you'll have to start the Sass compiler. Open a terminal, then navigate to whatever folder you cloned the repo to (e.g. "my-folder"):

```bash
cd my-folder
sass --watch src:dist
```

To make the compiler produce minified code, append ``--style compressed`` at the end of the ``sass`` command. By default the CSS will not be minified.

Now you are ready to make changes to the stylesheets.

## Pushing and updating
To add your changes to the repo, you will need the login credentials to the New Wiki Order Github account. All and only NWO members have these credentials.

If you have these ready, go back to the terminal and make sure you're still in the folder you cloned the repo to.

You can stage your changes (which is the first step) by typing the command ``git add .``

Next, commit your changes with an edit summary: ``git commit -m "my edit summary here"``

Now you're ready to officially publish your changes with the command: ``git push -u origin master``.

The terminal may ask for your Github credentials first, simply type them in as you're prompted to.

# Configurability
Some communities may wish to change aspects about certain modules. They can do this by simply overriding the relevant style rules in their own stylesheet.

To make this as easy as possible, certain properties should be variablized to minimize the amount of code needed. For example, if one wished to import the styles for Template:Quote and then change the color of the quotation marks, the following CSS would be applied:

```css
@import url("https://raw.githack.com/newwikiorder/fandom-modules/master/dist/templates/quote.css");

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