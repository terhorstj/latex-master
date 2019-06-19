# LaTeX-master

This project is intended to provide a master template for LaTeX documents. LaTeX has a notoriously steep learning curve, and my hope is that this template can expose some of the most common features for document formatting and layout.

*Note: As a method of best-practice, I prefer to use as few packages as possible to achieve my goal. This speeds up build times, minimizes errors and conflicts, makes it easier to find warnings, and avoids unexpected behaviors. Keep this in mind when choosing your options!*

## Getting Started

At the top of ```LaTeX-master.tex``` you will find four definitions:

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

I highly recommend the ```article``` class for most documents. If chapters are needed, ```report``` is a good alternative. The article class provides several other macro-level settings:

* ```letterpaper```
* ```titlepage```
* ```twocolumn```

You can decide which of these you prefer. Without the ```titlepage``` option, document title, author, and date will be printed at the top of the first page, with body text beginning immediately below it, like you might see in a magazine or academic journal. The ```twocolumn``` option, as expected, renders text in two columns, which makes for a professional-looking presentation but introduces other obstacles, such as figure and table widths. Most, if not all, LaTeX installations use U.S. letter as the default page size, so the ```letterpaper``` class option is necessary for 8.5"-by-11" paper only if your installation has a nonstandard localization. You can find more information on page layout at https://en.wikibooks.org/wiki/LaTeX/Page_Layout.

### *Geometry* Package

Owing to its ability to specify and redefine page layout, the ```geometry``` package is one of the principal or global packages that I would recommend loading on every document. Here, I use it to define margins based on our previous ```\mymargin``` definition. As you can see (and as one would hope), margins can be set independently of each other if needed. A useful option that I like to include here for drafts is ```showframe```; simply add it to the list of options to print page-layout elements when you build your document.

*Note: if you comment out the ```geometry``` package here, our ```\mymargins``` definition will not be applied and instead default margins will be calculated from page and font size.*

## Basic Setup

At this point, we have enough information to build a bare-bones document without any further intervention. However, what follow are some useful packages and settings to help customize your document, should the default settings not be desirable.

* ```\renewcommand{\familydefault}{\sfdefault}``` - You can use this setting to change the default font family. By default, LaTeX uses a Roman font, defined as \rmdefault. For a sans serif font, use \sfdefault. For a monospace font, use \ttdefault.

* ```\usepackage[T1]{fontenc}``` - An extensive amount of work has gone on behind the scenes to improve font capability in LaTeX. Specifically, for inclusion of accented characters, the T1 font encoding produces the best results. However, overall, LaTeX T1 fonts are of a lower quality. Therefore, if special characters are not being used extensively, disabling this option will produce a higher quality font. For more information on fonts in LaTeX, see http://www.johnterhorst.com/LaTeX/cm.pdf.

* ```\usepackage{microtype}``` - The ```microtype``` package improves typesetting significantly through the use of "micro-typography," which redefine parameters for kerning, justification, hyphenation, and protrusion. If you don't know what any of this means, fine! Just know that including this package will greatly improve the look of your text. Give it a try: build a document with a few paragraphs of text, with and without microtype enabled, and look at the difference. There are many, many options that can be tweaked within this package, and you can read about them in the documentation (https://ctan.org/pkg/microtype) and other websites (http://www.khirevich.com/LaTeX/microtype/), but the default settings are good enough. This package, along with ```geometry```, are the two main packages that I consider *essentially required* in all of my documents. 

* ```\usepackage[version=4]{mhchem}``` - The ```mhchem``` package provides some very nice tools for typesetting chemistry and chemical notation, which I use a lot of in my job as a chemistry professor. It also preloads a handful of other useful packages, such as ```color```, ```amsmath```, ```amssymb```, and ```calc```, so I like to think of it as a Swiss Army-knife package for producing scientific documents.

* ```\usepackage{graphicx}``` - Provides support for including graphics as PNG, JPG, and PDF. 

* ```\usepackage{fullpage}``` - A quick and dirty way to set margins to 1 inch (or 1.5 cm with the [cm] option). This package is significantly lighter than the ```geometry``` package, so it may be sufficient or even preferred for small, simple documents; but when activated it requires manual adjustments for headers, footers, or other elements of page layout that might be affected by other packages or settings. In general, I recommend against using this package for anything other than extremely simple layouts.

* ```\usepackage{parskip}``` - By default, LaTeX uses indentation to start a new paragraph, with no line spacing between paragraphs. This package provides a simple way to enable block paragraphs, where no indentation is used but rather a single blank line is inserted between paragraphs. This package can induce some "funkiness" in spacing of other environments (like equations, figures, and tables), but these effects are relatively minor.

	* *Note: Paragraph spacing and paragraph indentation can be set manually (without using a package) using for example ```\setlength{\parindent}{3em}``` and ```\setlength{\parskip}{12pt}```. These definitions will be enforced regardless of context, including font size and other line/paragraph considerations. As with ```parskip```, manually adjusting these parameters can have some unexpected effects on other environments. As a general rule, using a package to automatically set parameters is a better practice than setting up those parameters manually.*


* ```\usepackage{authblk}``` - For papers with multiple authors with multiple affiliations, this package provides a nice way to generate the author block of the paper's title. I have provided a sample of code at the end of the preamble. For more usage, as always, see the documentation. 

* ```verbatim```, ```textcomp```, ```siunitx```, ```amsmath```, ```amssymb```, ```mathrsfs```, ```textgreek```, ```float```, ```ulem``` - This is just a series of other packages that I frequently like to include. The ```verbatim``` package allows for printing verbatim text and for wrapping text in comment tags to be excluded during processing. The ```textcomp```, ```amssymb```, and ```mathrsfs``` packages provide many additional symbols and glyphs, and ```amsmath``` provides better math support. The ```siunitx``` package provides macros for dealing with scientific notation, units, and context-aware column alignment in tables. The ```textgreek``` package provides upright Greek characters in text mode. The ```float``` package disables the ability of floating environments to float (giving the author more control over the positioning and location of tables and figures, if desired). The ```ulem``` package redefines ```\emph``` for underline instead of italics (use ```\usepackage[normalem]{ulem}``` to revert this), and provides enhanced underlining (with ```\uline```), strikethrough, etc.

* ```\usepackage{tikz}``` - A package that I rarely use but others might use more often, so I thought I would include it in the Basic Setup section. This package allows for drawing of diagrams and figures directly in LaTeX. There is a steep learning curve here but it is an extremely powerful tool. It's also a very large package so I would recommend keeping it disabled unless it is being used.

* ```\usepackage{mathptmx}``` - This package redefines the main serif font as Times (*not* Times New Roman), including (most importantly) math support; it redefines the sans serif font as Helvetica; and it redefines the typewriter (monospace) font as Courier. Although Times is a widely used to font, there are many reasons why it should not be used, principally among which is designed specifically for printing in narrow columns where space is limited. In broader contexts (for example, essays, reports, letters etc.), other font choices are better. However, oftentimes is expected to be used as the main font, so I'm including it here for the sake of compatibility.

* ```\usepackage{enumitem}``` - This package provides additional options for the ```enumerate``` and ```itemize``` environments. See the package documentation for more details.

* ```\usepackage{subtext}``` - A useful package for setting Roman text in subscripts in math mode.

* ```\usepackage[bottom,hang,symbol]{footmisc}``` - The ```footmisc``` package provides a few useful customizations to the default footnote behavior in LaTeX. The ```bottom``` option forces the footnote to the bottom of the page even when the body text stops mid-page. (The default behavior is to place the footnote directly beneath the body text, even if the body text stops mid-page; such behavior can place a footnote in the middle or even near the top of the page, which is contrary to how most footnotes are written.) The ```hang``` option uses a hanging indent in the footnotes, which matches the block paragraphs in which many documents are formatted. (The default behavior is indented footnotes, which matches the default paragraph formatting in LaTeX.) The ```symbol``` option uses symbol characters to reference footnotes, instead of numbers. Choose which options suit your document best.

	* *Note: this package also allows for further customization including footnote margin distance. As always, see the package documentation for details.*

	* *Another note: the command ```\interfootnotelinepenalty=10000``` will force the typesetting engine to do everything it can to avoid placing a footnote on a different page than the page on which it is referenced. It essentially redefines the penalty for doing so to be the maximum possible.*


* ```\usepackage{setspace}``` - This package allows line spacing to be adjusted. The command to set line spacing with this package is ```\setstretch{1.1}```, where ```1.1``` means 10\% additional spacing and 2.0 would be double spacing.

* ```\usepackage[all]{nowidow}``` - The ```nowidow``` package prevents widows and orphans. When only the last line of a paragraph appears at the top of the next page, that line is called a widow. When only the first line of a paragraph appears at the bottom of a page, that line is called an orphan. Using this package will instruct the typesetting engine to do everything it can to avoid placing widows and orphans. (If my understanding is correct, it does so by defining the penalty for such as being the maximum possible, similar to the footnote penalty that we set above.)

* ```\usepackage[super,comma,sort&compress]{natbib}``` - If you use references or bibliographies extensively in your writing, I highly recommend checking out the ```natbib``` package. Specifically it provides features for references and bibliographies used in the natural sciences, but its features may be valuable to a more general user base. The features that I appreciate most from this package are the ability to sort and compress numerical references (for example, 1,3-7,9,13). Stylistically, I like my references cited using superscripts and separated by commas.

* ```\usepackage{booktabs}``` - For producing tables, no package is more essential than ```booktabs```. It produces tables with much more aesthetically pleasing lines and spacing, but also provides powerful features such as multicolumn, multirow, and midrules. See the documentation for more information.

* ```\usepackage[font=normalsize,labelfont={bf}]{caption}``` - The caption package can be used to customize appearance of captions that appear with table and figure floats. For example here, I am defining my font as normal size (many people might prefer small or tiny font for captions), and the label (for example, Figure or Table) as being bold. Other parameters can be defined, such as caption margin (you can increase the margin for table and figure captions if you don't want them to span all the way to the end of the normal text with), and distance from the float to the caption.

* ```\usepackage{titlesec}``` - This is another nearly essential package for producing documents with multiple sections, subsections, and subsubsections. It exposes the ability to redefine what these sections look like and how they are formatted. In this template I include several examples of styles that I like to use in various documents. This package also exposes the ```\titlespacing``` command, which, as the name suggests, allows for adjusting spacing before and after sections and subsections.

	* *Note: as a general rule, if your document requires a more extensive hierarchy then three levels (section, subsection, subsubsection, then consider reorganizing your information! LaTeX can accommodate more levels, but doing so produces documents that are organizationally difficult to follow.* 


* ```\usepackage{fancyhdr}``` and ```\usepackage{lastpage}``` - These packages can be used to create customized headers and footers. (```lastpage``` simply provides a reference to the total number of pages in the document, which can be referenced a header or footer.) I've provided some examples in the template. LaTeX provides some limited built-in functionality, mostly by means of the ```myheadings```page style, but most people looking for headers and footers will probably prefer to use ```fancyhdr```.

# Definitions, and Commands/Macros

In this template I also provide several of my own definitions, commands, and macros.

## Definitions

LaTeX provides the basic ```\def``` command for a user to provide a custom definition. For example,

* ```\def\myname{Joe Blow}``` can be set in the preamble, and then, in the document, can be used as ```My name is \myname.``` and will produce "My name is Joe Blow." in the output.

This is useful for saving time and space for text that is used repeatedly throughout the document, especially for text with complicated notation. 

* As mentioned at the beginning of this document, I used this feature to define my name, a short name, a document title, font size, and margins. I can use these definitions later on as options for other packages, for example using ```\mymargins``` in the ```geometry``` package, or using ```\myname``` with the ```authblk``` package, or using ```\myshortname``` with the ```fancyhdr``` package.

* I can define ```\dhnotrxn``` as ```{$\Delta H_\textnormal{rxn}^\circ$}``` once in the preamble, and then use ```\dhnotrxn``` in the document rather than having to type (or copy/paste) ```$\Delta H_\textnormal{rxn}^\circ$``` each time.

This also makes it convenient to redefine styles once in the preamble, and have all uses of that definition change accordingly in the document. 

* For example, if I want to change the "rxn" subscript to "reaction", I can simply change the definition to ```{$\Delta H_\textnormal{reaction}^\circ$}```, and have all instances of ```\dhnotrxn``` reference that change.

## Commands/Macros

In a similar fashion to definitions, commands or macros can be used to take arguments. 

* For example, I created a command ```\ph``` via ```\newcommand*\ph[1]{$\textnormal{pH}=#1$}```. This command takes one argument (as ```#1```), so that ```\ph{5}``` produces $\textnormal{pH}=5$ which sets text as "pH = 5". 

Commands can take any number of arguments and can be used to generate any arbitrarily complex code. As with definitions, this can save time, guarantee consistency throughout the document, and facilitate easy modification down the road.

If you find yourself repeatedly typing the same code or very similar variations of the same code, consider turning that code into a macro! This programmability is one of many features that sets LaTeX apart from standard word processors. Make use of it!

# If/Then/Else Logic

One underappreciated feature of LaTeX is that the language is Turing-complete. This means that it inherently understands and supports logical structures. 

In many cases I find it useful to create a document with two versions - for example, a resume that I can put on the web and one that I can give to potential employers. On the web version I might want to hide personal information like my phone number or home address, but I would like to include that on other versions.

Rather than maintaining two copies of a resume or having to comment/uncomment large blocks of code, we can use an if/then/else structure. Here's how we do that:

* Define the name of the structure, for example, ```\newif\ifweb```

* Then, specify whether this condition is true or false, for example, ```\webtrue``` or ```\webfalse```

* Then, provide your definitions. For example, ```\ifweb\def\address{123 Work Ave.}\else\def\address{987 Home St.}\fi```

That may look complicated at first, but what we are saying is "If web, define ```\address``` as my work address. Otherwise, define ```\address``` as my home address. 

Then, any time ```\address``` is referenced in the text, it is substituted by the appropriate address. Changing ```\webtrue``` or ```\webfalse``` will change whether ```\ifweb``` is evaluated as true or false.

This can be used in lots of ways! For example, if I want to exclude references from the web version of my resume (in addition to using the address logic above), then I can create a new block using ```\ifweb```, where my references are excluded in the "true" section, but they are included in the "false" section. 

In this way, any number of a document's features can be programmed to be enabled or disabled, to appear or not to appear, etc., depending on whether a condition is set as true or false in the preamble.

If you really want to get fancy, you can build nested arguments as well! 

# Hyperref

Lastly, the ```hyperref``` package should always be loaded last. This package can be used to embed hyperlinks and URLs, including email addresses, and can also generate clickable links between references, footnotes, endnotes, etc. Even if you don't need hyperlinking text, this package can also be used to embed metadata into the output PDF, including author, keywords, title, subject, and even a page view mode for Adobe Acrobat Reader. It is a monstrous package that is notorious for being incompatible with other packages. (The reason why it should always be loaded last is because that tends to minimize conflicts with other packages.)

# Sample text in the document

In the template I provide the following sample text:

* An example of how to customize text within the default ```\title``` and ```\author``` commands

* How to use the ```authblk``` package

* An example of front matter, including title, table of contents, list of figures, list of tables, changing page number style, and changing/resetting page number.

* Use of ```\section``` and ```\subsection``` so you can see modifications to those styles via ```\titlesec```

* An example of a figure containing an image using ```graphicx```

* An example of a fancy table using ```booktabs```

* Use of references with ```natbib``` options and including macros for custom formatting of my references (```\mytref``` and ```\myzref```)

* Some notes, after ```\end{document}```. No text appearing after ```\end{document}``` will be processed by the typesetting engine, so sometimes I like to include notes for myself here. In this template, I included 

	* how to use footnotes with symbols (via ```footmisc``` with the ```symbol``` option enabled). For small documents where I only have one footnote, sometimes I would rather use a symbol instead of the number.

	* Some fancy chemical notation making use of ```mhchem``` and concomitantly loaded ```amsmath```.

	* How to use the ```align``` environment, which is something I rarely use but sometimes find it necessary or desirable for chemical reaction mechanisms, though I can never remember how to use it.

# Final words

There is a lot of code here! Some sections of the code contain snippets that I've found over the years, so I claim none of this as my own.

As you can see, most of this document is commented out. The point of this template is to allow the user to include or exclude as much or as little code as needed to produce the documents that he or she desires. 

As I mentioned in the introduction, my hope is that this template can expose some of the most common features for document formatting and layout.

The idea is that one should be able to open this master template, comment or an comment a handful of lines, and begin writing. 


## Have any suggestions?

Please let me know! Either contact me or contribute to this project.