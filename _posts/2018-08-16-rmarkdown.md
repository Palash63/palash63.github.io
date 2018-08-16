---
title: 'RStudio and RMarkdown for Analytic Report'
date: 2018-08-16
excerpt: A easy way to write analytic report using RMarkdown
permalink: /posts/2018/08/rmarkdown/
tags:
  - posts
  - rstudio
  - rmarkdown
---
Overview of Rmarkdown
=====================

R Markdown is a way of writing reports that includes R code and output.

The goal of this document is to explain, with examples, how to use its
most essential features. (See rather <http://rmarkdown.rstudio.com>.)
for complete overview.

This document look in turn at three aspects of R Markdown:

-   basic formatting
-   include R code and its output
-   include Mathmatical and Statistical expression.

Editing andRendering with Rmarkdown
===================================

-   To write R Markdown, we will need a text editor, a program that read
    and write plain text files. We will also need R/RStudio, and the
    package `rmarkdown`.

-   click the button that says "knit".

-   See the `render` command in the package `rmarkdown` to render
    wwithout RStudio.

### Paragraph Breaks and Forced Line Breaks

-   To insert a break between paragraphs, include a single completely
    blank line.
-   To force a line break, put *two* blank  
-   spaces at the end of a line.

<!-- -->

    To insert a break between paragraphs, include a single completely blank line.

    To force a line break, put _two_ blank  
    spaces at the end of a line.

### Headers

-   The character `#` at the beginning of a line means that the rest of
    the line is interpreted as a section header.
-   The number of `#`s at the beginning of the line indicates whether it
    is treated as a section, sub-section, sub-sub-section, etc. of the
    document.

### Italics, Boldface format

Text to be *italicized* goes inside *a single set of underscores* or
*asterisks*. Text to be **boldfaced** goes inside a **double set of
underscores** or **asterisks**.

    Text to be _italicized_ goes inside _a single set of underscores_ or *asterisks*.  Text to be **boldfaced** goes inside a __double set of underscores__  or **asterisks**.

### Quotations

Set-off quoted paragraphs are indicated by an initial `>`:

> "An approximate answer to the right problem is worth a good deal more
> than an exact answer to an approximate problem." -- \[John Tukey\].

    > "An approximate answer to the right problem is worth a good deal more than an exact answer to an approximate problem." -- [John Tukey]. 

### Bullet Lists

-   This is a list marked where items are marked with bullet points.
-   Each item in the list should start with a `*` (asterisk) character,
    or a single dash (`-`).
-   Each item should also be on a new line.
    -   Indent lines and begin them with `+` for sub-bullets.
    -   Sub-sub-bullet aren't really a thing in R Markdown.

### Numbered lists

1.  Lines which begin with a numeral (0--9), followed by a period, will
    usually be interpreted as items in a numbered list.
2.  R Markdown handles the numbering in what it renders automatically.
3.  This can be handy when we lose count or don't update the numbers
    when editing.
    1.  Sub-lists of numbered lists, with letters for sub-items, are a
        thing.

Hyperlinks and Images formating
===============================

### Hyperlinks format

Hyperlinks anchored by URLs are easy: just type the URL, as, e.g.,
<http://www.stat.cmu.edu/~cshalizi/rmarkdown/rmarkdown.Rmd> to get the
source file for this document.

Hyperlinks anchored to text have the [anchor in square brackets, then
the link in
parentheses](http://www.stat.cmu.edu/~cshalizi/rmarkdown/rmarkdown.Rmd).

    [anchor in square brackets, then the link
    in parentheses](http://www.stat.cmu.edu/~cshalizi/rmarkdown/rmarkdown.Rmd)

### Images format

Images begin with an exclamation mark, then the text to use if the image
can't be displayed, then either the file address of the image (in the
same directory as your document) or a URL.

![KUMC logo.](https://github.com/Palash63/palash63.github.io/tree/master/images/logo.jpg)

<img src="https://github.com/Palash63/palash63.github.io/tree/master/images/logo.jpg" alt="A caption" width="70%" />
<p class="caption">
A caption
</p>

Including R Code
================

The real point of R Markdown is that it lets you include your code, have
the code run automatically when your document is rendered, and
seemlessly include the results of that code in your document. The code
comes in two varieties, code **chunks** and **inline** code.

### Code Chunks and Their Results

A code **chunk** is simply an off-set piece of code by itself. It is
preceded by ```` ```{r} ```` on a line by itself, and ended by a line
which just says ```` ``` ````. The code itself goes in between. Here,
for instance, is some code which loads a data set from a library, and
makes a scatter plot.

    library(MASS)
    data(cats)
    plot(Hwt ~ Bwt, data=cats, xlab="Body weight (kg)", ylab="Heart weight (g)",col=5)

![](https://github.com/Palash63/palash63.github.io/tree/master/images/unnamed-chunk-1-1.png)

First, notice how the code is included, nicely formatted, in the
document. Second, notice how the output of the code is also
automatically included in the document. If your code outputs numbers or
text, those can be included too:

    with(cats, cor(Hwt, Bwt))

    ## [1] 0.8041274

### Naming Chunks

We can give chunks names immediately after their opening, like
```` ```{r, clevername} ````. This name is then used for the images (or
other files) that are generated when the document is rendered.

### Changing Image Sizes and Alignments

There are a bunch of options for adjusting the placement of the figures
which R produces. `fig.align` controls the horizontal **alignment**
(left, right, or center).

When producing PDF, the options `out.height` and `out.width` let you
specify the desired height or width of the figure, in inches,
centimeters, or multiples of pre-defined lengths (from `LaTeX`). So for
instance ```` ```{r, out.height="3in"} ```` forces the image to be 3
inches high, while ```` ```{r, out.width="0.48\\textwidth"} ```` forces
the image's width to be a bit less than half of the total width of the
text on the page (so that two such images will fit side by side). The
next few figures illustrate.

<img src="https://github.com/Palash63/palash63.github.io/tree/master/images/unnamed-chunk-3-1.png" style="display: block; margin: auto;" /><img src="https://github.com/Palash63/palash63.github.io/tree/master/images/unnamed-chunk-3-2.png" style="display: block; margin: auto;" />

### Tables format

The default print-out of matrices, tables, etc. from R Markdown is
frankly ugly. The `knitr` package contains a very basic command,
`kable`, which will format an array or data frame more nicely for
display.

Compare:

    coefficients(summary(lm(Hwt ~ Bwt, data=cats)))

    ##               Estimate Std. Error    t value     Pr(>|t|)
    ## (Intercept) -0.3566624  0.6922770 -0.5152019 6.072131e-01
    ## Bwt          4.0340627  0.2502615 16.1193908 6.969045e-34

with

    library(knitr) # Only need this the first time!
    kable(coefficients(summary(lm(Hwt ~ Bwt, data=cats))))

<table>
<thead>
<tr class="header">
<th></th>
<th align="right">Estimate</th>
<th align="right">Std. Error</th>
<th align="right">t value</th>
<th align="right">Pr(&gt;|t|)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>(Intercept)</td>
<td align="right">-0.3566624</td>
<td align="right">0.6922770</td>
<td align="right">-0.5152019</td>
<td align="right">0.6072131</td>
</tr>
<tr class="even">
<td>Bwt</td>
<td align="right">4.0340627</td>
<td align="right">0.2502615</td>
<td align="right">16.1193908</td>
<td align="right">0.0000000</td>
</tr>
</tbody>
</table>

### Setting Defaults for All Chunks

You can tell R to set some defaults to apply to all chunks where you
don't specifically over-ride them. Here are the ones I generally use:

    # Need the knitr package to set chunk options
    library(knitr)

    # Set knitr options for knitting code into the report:
    # - Don't print out code (echo)
    # - Save results so that code blocks aren't re-run unless code changes (cache),
    # _or_ a relevant earlier code block changed (autodep), but don't re-run if the
    # only thing that changed was the comments (cache.comments)
    # - Don't clutter R output with messages or warnings (message, warning)
      # This _will_ leave error messages showing up in the knitted report
    opts_chunk$set(echo=FALSE,
                   cache=TRUE, autodep=TRUE, cache.comments=FALSE,
                   message=FALSE, warning=FALSE)

### More Options

See \[<http://yihui.name/knitr/options/>\] for a complete listing of
possible chunk options.

    library("plot3D")

    ## Warning: package 'plot3D' was built under R version 3.4.4

    data(iris)
    # x, y and z coordinates
    x <- sep.l <- iris$Sepal.Length
    y <- pet.l <- iris$Petal.Length
    z <- sep.w <- iris$Sepal.Width
    # Create a scatter plot
     scatter3D(x, y, z, phi = 0, bty = "g",
            pch = 20, cex = 2, ticktype = "detailed")

![](https://github.com/Palash63/palash63.github.io/tree/master/images/unnamed-chunk-7-1.png)

Math in R Markdown
==================

Getting started with equations
------------------------------

We can write fractions: $\\frac{2}{3}$. We can also handle things like
estimated population growth rate, e.g., $\\hat{\\lambda}=1.02$. And,
$\\sqrt{4}=2$.

*α*, *β*, *γ*, *Γ*

*a* ± *b*
*x* ≥ 15
*a*<sub>*i*</sub> ≥ 0   ∀*i*

Statistics
----------

The binomial probability:
$$f(y|N,p) = \\frac{N!}{y!(N-y)!}\\cdot p^y \\cdot (1-p)^{N-y} = {{N}\\choose{y}} \\cdot p^y \\cdot (1-p)^{N-y}$$

To calculate the **mean** of observations of variable , you can use:
$$\\bar{x} = \\frac{1}{n} \\sum\_{i=1}^{n}x\_{i}$$

Note that this equation looks quite nice above where it's in display
math mode. It is more compact but not quite as nice looking if we
present it using inline mode, e.g.,
$\\bar{x} = \\frac{1}{n} \\sum\_{i=1}^{n}x\_{i}$.

Let's do the same with the equation for **variance**. First the inline
version, which is
$\\sigma^{2} = \\frac{\\sum\\limits\_{i=1}^{n} \\left(x\_{i} - \\bar{x}\\right)^{2}} {n-1}$.
And then the display mode version:
$$\\sigma^{2} = \\frac{\\sum\_{i=1}^{n} 
  \\left(x\_{i} - \\bar{x}\\right)^{2}}
  {n-1}$$

Next, it's good to look at the equation for **covariance** to see how it
is just a generalization of variance to two variables. An inline version
of the equation is
$cov\_{x,y} = \\frac{\\sum\\limits\_{i=1}^{n}{(x\_i-\\overline{x}) \\cdot (y\_i-\\overline{y})} }{n-1}$.
And, the display mode is:
$$cov\_{x,y} = \\frac{\\sum\\limits\_{i=1}^{n}{(x\_i-\\overline{x}) \\cdot (y\_i-\\overline{y})} }{n-1}$$

And, finally, we'll end with the **standard deviation**. Here's the
inline version,
$\\sigma = \\sqrt{\\frac{\\sum\\limits\_{i=1}^{n} \\left(x\_{i} - \\bar{x}\\right)^{2}} {n-1}}$.
And here's the display version.
$$\\sigma = \\sqrt{\\frac{\\sum\\limits\_{i=1}^{n} \\left(x\_{i} - \\bar{x}\\right)^{2}} {n-1}}$$

Troubleshooting/Stuff to Avoid
==============================

-   Do not call `View` or `help` in your document; these are interactive
    commands which don't work well in scripts.
-   "It works when I source it, but it won't knit": This is basically
    the same problem as "it worked in the console".
-   Avoid `attach` in both the console and in your file; using it is a
    recipe for creating hard-to-find errors. We can still shorten
    expressions using `with` instead.
-   We need LaTeX to create PDFs. If we are having trouble doing so, try
    switching the output format to HTML.
    -   Do try to fix your LaTeX installation later, when you don't have
        such time pressure; it's really useful.
    -   LaTeX will complain if you try to print out truly enormous
        things. Errors about "out of stack", or "pandoc 43", are often
        caused by this. Don't print out enormous things. (Suppressing
        warnings and other messages may help.)
-   When we need to load data files or source someone else's code, use
    full URLs, rather than creating local copies and loading them from
    your disk.

Further Reading
===============

For more on R Markdown, see <http://rmarkdown.rstudio.com>, particularly
the more detailed help pages (rather than the first-guides).

### Acknowledgments

Thanks to Dr. Cosma Shalizi and Dr. Jay Rotella for their contribution.
