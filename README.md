# FoilTeX with Emacs Org Mode

I have been an Emacs user since the early 2000s, and even before that, a LaTeX user. With the advent of [org mode](https://orgmode.org/), I was able to combine the efficiency of an Emacs-based markdown language with the mathematical typesetting power of LaTeX. 

In my job as a professor, I make presentations frequently. While org-mode handles this nicely with the [Beamer class](https://orgmode.org/worg/exporters/beamer/tutorial.html) in LaTeX, I longed for the simplicity of the LaTeX slides (foils) that I used to make with the [FoilTeX](https://ctan.org/pkg/foiltex?lang=en) package.  So, after some searching, I figured out an easy way to write FoilTeX presentations with org-mode.

## How it works

To make this work, there are two basic steps:

1. You need to edit your `.emacs` file to include the following code block:

```
(require 'ox-latex)
(add-to-list 'org-latex-classes
	     '("foils"
	       "\\documentclass{foils}"
	       ("\\foilhead[-1cm]{%s}" . "\\foilhead[-1cm]*(%s)"))
	     )
```

This code does two things. First, it defines a "foils" class that you can call in an org document. Second, it maps the org-mode list symbol `*` to the FoilTeX page header `\foilhead`.

2. You need to include the following header at the beginning of your org document:

```
#+TITLE: Your document title
#+AUTHOR: Your name
#+DATE: the date 
#+LaTeX_CLASS: foils
#+LaTeX_CLASS_OPTIONS: [portrait, 17pt]
#+LATEX_HEADER: \MyLogo{Your footer logo}
#+LATEX_HEADER: \setlength{\parindent}{0cm}
#+LATEX_HEADER: \usepackage{amsmath}
#+OPTIONS: toc:nil
```

Strictly speaking, not all of these lines are required. But for me, they form the core of a minimal, but nicely formatted set of foils/slides.  Note that the `LaTeX_CLASS_OPTIONS` line can include any of the standard class options available in FoilTeX (e.g., `landscape`], all of which are detailed in the [FoilTeX manual](http://ftp.math.purdue.edu/mirrors/ctan.org/macros/latex/contrib/foiltex/foiltex.pdf).

## Example document

Here is an example [org-mode file](example.org) (and the resulting [pdf](example.pdf) that demonstrates how I use the integration of org and FoilTeX when making lecture slides for my courses.
