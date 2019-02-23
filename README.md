# latex-master

This project is intended to provide a master template for LaTeX documents. LaTeX has a notoriously steep learning curve, and my hope is that this template can expose some of the most common features for document formatting and layout.

*Note: As a method of best-practice, I prefer to use as few packages as possible to achieve my goal. This speeds up build times, minimizes errors and conflicts, makes it easier to find warnings, and avoids unexpected behaviors. Keep this in mind when choosing your options!*

## Getting Started

At the top of ```latex-master.tex``` you will find four definitions:

1. ```\def\myname```
2. ```\def\myshortname```
3. ```\def\mydoctitle```
4. ```\def\myfontsize```
5. ```\def\mymargins```

These definitions will be used as options in package specifications later on in the preamble. 

### Font Size

LaTeX provides three primary choices for font size: 10, 11, and 12 points. All text in a document is set *relative* this primary size, using switches like ```\small```, ```\large```, or ```\scriptsize```. 

LaTeX's venerable default font, Computer Modern (or Latin Modern in more-recent implementations), is slightly larger and less compressed than other common serif typefaces like Times New Roman, Georgia, and Cambria. In fact, 11-point Computer Modern set with 1.1-inch margins matches nearly perfectly in terms of spacing and line/paragraph breaks with 12-point Times New Roman set with 1.0-inch margins. 

### A Comment on Margins

By default, LaTeX calculates "appropriate" margin widths based on page dimensions and font size so as to allow approximately 60 characters per line. While this may ostensibly provide "optimal" ease of reading, it usually results in margins of *at least* 1.6 inches, which is (in my opinion) simply not practical for a document of any real substance. It is wasteful of space (and of paper if you are printing!), and severely limits available width for figures, tables, and section titles (which themselves are painfully oversized by default; more of this later...). Therefore I have decided to make margin width a principal document setting that I expect users to set to their wishes.

## Class Designation 

I highly recommend the ```article``` class for most documents. If chapters are needed, ```report``` is a good alternative. The article class provides several other macro-settings:

* ```letterpaper```
* ```titlepage```
* ```twocolumn```

You can decide which of these you prefer. Without the ```titlepage``` option, document title and author will be printed at the top of the first page, with body text beginning immediately below it, like you might see in a magazine or academic journal. The ```twocolumn``` option, as expected, renders text in two columns, which makes for a professional-looking presentation but introduces other obstacles, such as figure and table widths. You can find more information on page layout at https://en.wikibooks.org/wiki/LaTeX/Page_Layout.

### *Geometry* Package

Owing to its ability to specify and redefine page layout, the ```geometry``` package is one of the principal or global packages that I would recommend loading on every document. Here, I use it to define margins based on our previous ```\mymargin``` definition. As you can see (and as one would hope), margins can be set independently of each other if needed. A useful option that I like to include here for drafts is ```showframe```; simply add it to the list of options to print page-layout elements when you build your document.

*Note: if you comment out the ```geometry``` package here, our ```\mymargins``` definition will not be applied and instead default margins will be calculated from page and font size.*

## Basic Setup

At this point, we have enough information to build a bare-bones document without any further intervention. However, what follow are some extremely useful packages settings to help customize your document, should the default settings not be desirable.

* ```\usepackage[T1]{fontenc}``` - by default, TeX uses a 7-bit font encoding called "```OT1```" that has a limit of 128 glyphs; this means that diacriticals and accented characters are built from separate entities. On the other hand, a more-modern 8-bit font encoding called "```T1```" allows for 256 glyphs, such that diacriticals and accented characters are singly contained entities. This allows for more flexibility and accuracy for hyphenation and kerning, and the text in the output PDF can be properly copied, pasted, and searched. Overall, this package is of course optional, but will produce a higher quality PDF than will result without its use. You can find more discussion on this topic here: https://tex.stackexchange.com/questions/664/why-should-i-use-usepackaget1fontenc.

	*	*Note: A standard LaTeX distribution includes both 7-bit and 8-bit versions of Computer Modern. The ```lmodern``` package enables the Latin Modern font, which is essentially 8-bit Computer Modern. Therefore ```\usepackage{lmodern}``` would generally an appropriate substitute for ```\usepackage[T1]{fontenc}```.*


* ```\usepackage{microtype}``` - Perhaps even more than ```fontenc```, ```microtype``` improves typesetting significantly through the use of "micro-typography," which redefines parameters for kerning, justification, hyphenation, and protrusion. If you don't know what any of this means, fine! Just know that including this package will greatly improve the look of your text. Give it a try: build a document with a few paragraphs of text, with and without microtype enabled, and look at the difference. There are many, many options that can be tweaked within this package, and you can read about them in the documentation (https://ctan.org/pkg/microtype) and other websites (http://www.khirevich.com/latex/microtype/), but the default settings are good enough. This package, along with ```fontenc``` and ```geometry```, are the three main packages that I consider *essentially required* in all of my documents. 

* ```\usepackage[version=4]{mhchem}``` - The ```mhchem``` package provides some very nice tools for typesetting chemistry and chemical notation, which I use a lot of in my job as a chemistry professor. It also preloads a handful of other useful packages, such as ```color```, ```amsmath```, ```amssymb```, and ```calc```, so I like to think of it as a Swiss Army-knife package for producing scientific documents.

* ```\usepackage{graphicx}``` - Provides support for including graphics as PNG, JPG, and PDF. 

* ```\usepackage{fullpage}``` - A quick and dirty way to set margins to 1 inch (or 1.5 cm with the [cm] option). This package is significantly lighter than the ```geometry``` package, so it may be sufficient or even preferred for small, simple documents; but when activated it requires manual adjustments for headers, footers, or other elements of page layout that might be affected by other packages or settings. In general, I recommend against using this package for anything other than extremely simple layouts.

* ```\usepackage{parskip}``` - By default, LaTeX uses indentation to start a new paragraph, with no line spacing between paragraphs. This package provides a simple way to enable block paragraphs, where no indentation is used but rather a single blank line is inserted between paragraphs. This package can induce some "funkiness" in spacing of other environments (like equations, figures, and tables), but these effects are relatively minor.

	* *Note: Paragraph spacing and paragraph indent can be set manually (without using a package) using for example ```\setlength{\parindent}{3em}``` and ```\setlength{\parskip}{12pt}```. These definitions will be enforced regardless of context, including font size and other line/paragraph considerations. As with ```parskip```, manually adjusting these parameters can have some unexpected effects on other environments. As a general rule, using a package to automatically set parameters is a better practice than setting up those parameters manually.*


* ```\usepackage{authblk}``` - for papers with multiple authors with multiple affiliations, this package provides a nice way to generate the author block of the paper's title. For usage as always, see the documentation: https://ctan.org/pkg/authblk. 

* ```verbatim```, ```textcomp```, ```siunitx```, ```amsmath```, ```amssymb```, ```mathrsfs```, ```textgreek```, ```float```, ```ulem``` - This is just a series of other packages that I frequently like to include. The ```verbatim``` package allows for printing verbatim text and for wrapping text in comment tags to be excluded during processing. The ```textcomp```, ```amssymb```, and ```mathrsfs``` packages provide many additional symbols and glyphs, and ```amsmath``` provides better math support. The ```siunitx``` package provides macros for dealing with scientific notation, units, and context-aware column alignment in tables. The ```textgreek``` package provides upright Greek characters in text mode. The ```float``` package disables the ability of floating environments to float (giving the author more control over the positioning and location of tables and figures, if desired). The ```ulem``` package redefines ```\emph``` for underline instead of italics (use ```\usepackage[normalem]{ulem}``` to revert this), and provides enhanced underlining (with ```\uline```), strikethrough, etc.

* ```\usepackage{tikz}``` - A package that I rarely use but others might use more often, so I thought I would include it in the Basic Setup section. This package allows for drawing of diagrams and figures directly in LaTeX. There is a steep learning curve here but it is an extremely powerful tool. It's also a very large package so I would recommend keeping it disabled unless it is being used.

* ```\usepackage{mathptmx}``` - This package redefines the main serif font as Times (*not* Times New Roman), including (most importantly) math support; it redefines the sans serif font as Helvetica; and it redefines the typewriter (monospace) font as Courier. 

* ```\usepackage{enumitem}``` - 






