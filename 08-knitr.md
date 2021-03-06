---
layout: page
title: R for reproducible scientific analysis
subtitle: Dynamic reports with knitr
minutes: 30
---



> ## Learning Objectives {.objectives}
>
> * Understand the value of `knitr`: Generate dynamic documents that include text, code, and results.
> * Control basic formatting using markdown syntax.
> * Be able to create, edit, and compile an .Rmd document including code chunks and inline code.

### The What and Why of RMarkdown

RMarkdown is a way to keep our notes, code, and results organized in a single document. It is a great tool for "literate programming" -- the idea that your code should be readable by humans as well as computers. It keeps your writing and results together, so if you collect some new data or change how you clean the data, you just have to re-compile the document and you're up to date.

RMarkdown uses a simple syntax, which is then converted by the R package `knitr` and the utility pandoc, to html, pdf (if you have LaTeX on your machine), or Word files. You can write websites in RMarkdown, articles that conform to publishing standards, CVs, presentations... People have even written dissertations in RMarkdown. The syntax of the language is designed to be super simple, but you still get high quality output.

### Organization of an RMarkdown document

To get started, install the `knitr` package and create a new RMarkdown document.

> ## Challenge - Create and render an RMarkdown document {.challenge}
> 
> - Install `knitr` via `install.packages("knitr")`
> - Click on File -> New File, and select the "R Markdown..." option. 
> - Accept the default options in the dialog box that follows. 
> - Save the file as `firstRMarkdown.Rmd` in the `papers` directory of your project. 
> - Click on the "Knit HTML" button at the top of the script (or press ctrl-shift-k/cmd-shift-k) and compare the output to the source.
>

The top of the source (.Rmd) file has some header material in YAML format (enclosed by triple dashes). Some of this gets displayed in the output header, other of it provides formatting information to the conversion engine. This is the only required part of an RMarkdown document. 

After the header, there is a mix of plain-text, formatted with markdown syntax, and R-code chunks. 

#### Markdown syntax

This page -- <http://RMarkdown.rstudio.com/authoring_basics.html> -- covers the basics of formatting text in RMarkdown. You can create section headers and sub-headers with `#`, `##`, etc. Emphasis is achieved by surrounding text with one or two asterisks:  \*italics\* and \*\*bold\*\*. Lists via `-` and numbered lists using `1.`, `2.`, etc. Even creating a table is simple.

Markdown also supports LaTeX equation editing. We can display pretty equations by enclosing them in `$`. E.g. `$\alpha = \dfrac{1}{(1 - \beta)^2}$` renders as: $\alpha = \dfrac{1}{(1 - \beta)^2}$.

#### Code chunks

To distinguish R code from text, RMarkdown uses three back-ticks followed by `{r}` to distinguish a "code chunk". In RStudio, the keyboard shortcut to create a code chunk is command-option-i or control-alt-i. You can set options for how that code chunk renders after the `r`. For example, `echo = FALSE` will prevent the code from being displayed, but its output will still be rendered. `fig.height = 8` will make plots generated in that code chunk 8 inches in height. You can set the options for the entire document by including this in a code chunk in your document: `opts_chunk$set( ... )`. Check out the full suite of code-chunk options at [Yihui's (the author of `knitr`) website](http://yihui.name/knitr/options/).

A code chunk will set off the code and its results in the output document, but you can also print the results of code within a text block by enclosing code like so: `` `r code-here` ``. For example, this: 

``There were `r length(unique(gapminder$country))` countries in the dataset with a mean per-capita gdp of $`r round(mean(gapminder$gdpPercap), 1)`.``

Renders to:

There were 142 countries in the dataset with a mean per-capita gdp of $7215.33.

#### RMarkdown documents are self-contained

Any data or package you use in an RMarkdown document must be loaded in that document. `knitr` will not look in the Environment for data or functions. It is sometimes useful to include a code-chunk at the beginning of your document where you load data and packages and perhaps set `knitr` options for the whole document. You may or may not want to include this code in the output. If not, you can give it the option `include = FALSE`.

> ## Challenge - Use knitr to produce a report {.challenge}
>
> 1. Open an new .Rmd script and save it as life_expectancy.Rmd
> 2. Create a plot of life_expectancy versus year. Start simple, when you're finished with the rest of this challenge, return to this to improve it.
> 3. Add a few notes describing what the code does and what the main findings are. Include an in-line calculation of the global average life expectancy over the whole dataset.
> 4. `knit` the document and view the html result.
>
