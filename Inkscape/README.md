# Inkscape

## Inkscape and Arrows

Inkscape creates `svg` files that browsers cannot display correctly, see stack-exchange issue: [inkscape arrow tip color disappeared in browser](https://graphicdesign.stackexchange.com/questions/158452/inkscape-arrow-tip-color-disappeared-in-browser).

The problem is the `context-stroke` attribute value. Browsers do not
support this.

The offered solutions do not work for me. So, as a workaround, make all arrow tips have the same color (pick a color with a known value):

```sh
sed 's/context-stroke/#121212/g' image.svg > image-fixed.svg
```

In addition, fonts are not embedded in svg images, so they will be
replaced by browsers if they are not web-safe, so convert them to
paths at the very last step.

## README.md and svg links [no workaround found]

When GitHub renders svg images, the whole image becomes a link to the
file. Links (`<a>` elements) inside of the svg will be inaccessible.
Maybe an svg image that is inline with the md document is rendered
without being a link, and thus preserving internal links. (viewing the
svg in the _raw_ view has working links).

All methods of direct embedding have failed so far.

## Experiments with svg images

Each subsection will quote a command and then try that command right after. If no *svg* image appears, then the command failed on GitHub.

The first three methods work in [pandoc](https://pandoc.org/) (`<object>`, `<embed>`, `<iframe>`), rendered in the epiphany browser.

### object tag

```html
<object name="figure" type="text/html" data="ToolsetFlowchart-fix.svg"></object>
```

<object name="figure" type="text/html" data="ToolsetFlowchart-fix.svg"></object>

### embed tag

```html
<embed type="text/html" src="./ToolsetFlowchart-fix.svg"></embed>
```

<embed type="text/html" src="./ToolsetFlowchart-fix.svg"></embed>

### iframe

```html
<iframe src="./ToolsetFlowchart-fix.svg"></iframe>
```

<iframe src="./ToolsetFlowchart-fix.svg"></iframe>

### link

```html
<link rel="html-import" href="./ToolsetFlowchart-fix.svg"></link>
```

<link rel="html-import" href="./ToolsetFlowchart-fix.svg"></link>


### PHP style with server side substitution

```html
<!--#include file="ToolsetFlowchart-fix.svg" -->
```

<!--#include file="ToolsetFlowchart-fix.svg" -->

