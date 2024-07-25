---
title: LaTeX
type: docs
---

# LaTeX

## Install MiKTeX

1. Download the [MiKTeX installer](https://miktex.org/download)
2. Run the installer and follow the instructions to complete the installation
3. After installation, ensure `xelatex` is in your system path
   ```sh
   xelatex --version
   ```

## Configure LaTeX Workshop

1. Install the `LaTeX Workshop` extension in Visual Studio Code
2. Add configuration in Visual Studio Code settings

   ```json
   {
     "latex-workshop.latex.tools": [
       {
         "name": "xelatex",
         "command": "xelatex",
         "args": [
           "-synctex=1",
           "-interaction=nonstopmode",
           "-file-line-error",
           "%DOC%"
         ]
       },
       {
         "name": "latexmk",
         "command": "latexmk",
         "args": [
           "-synctex=1",
           "-interaction=nonstopmode",
           "-file-line-error",
           "-pdf",
           "-outdir=%OUTDIR%",
           "%DOC%"
         ],
         "env": {}
       },
       {
         "name": "lualatexmk",
         "command": "latexmk",
         "args": [
           "-synctex=1",
           "-interaction=nonstopmode",
           "-file-line-error",
           "-lualatex",
           "-outdir=%OUTDIR%",
           "%DOC%"
         ],
         "env": {}
       },
       {
         "name": "xelatexmk",
         "command": "latexmk",
         "args": [
           "-synctex=1",
           "-interaction=nonstopmode",
           "-file-line-error",
           "-xelatex",
           "-outdir=%OUTDIR%",
           "%DOC%"
         ],
         "env": {}
       },
       {
         "name": "latexmk_rconly",
         "command": "latexmk",
         "args": ["%DOC%"],
         "env": {}
       },
       {
         "name": "pdflatex",
         "command": "pdflatex",
         "args": [
           "-synctex=1",
           "-interaction=nonstopmode",
           "-file-line-error",
           "%DOC%"
         ],
         "env": {}
       },
       {
         "name": "bibtex",
         "command": "bibtex",
         "args": ["%DOCFILE%"],
         "env": {}
       },
       {
         "name": "rnw2tex",
         "command": "Rscript",
         "args": [
           "-e",
           "knitr::opts_knit$set(concordance = TRUE); knitr::knit('%DOCFILE_EXT%')"
         ],
         "env": {}
       },
       {
         "name": "jnw2tex",
         "command": "julia",
         "args": ["-e", "using Weave; weave(\"%DOC_EXT%\", doctype=\"tex\")"],
         "env": {}
       },
       {
         "name": "jnw2texminted",
         "command": "julia",
         "args": [
           "-e",
           "using Weave; weave(\"%DOC_EXT%\", doctype=\"texminted\")"
         ],
         "env": {}
       },
       {
         "name": "pnw2tex",
         "command": "pweave",
         "args": ["-f", "tex", "%DOC_EXT%"],
         "env": {}
       },
       {
         "name": "pnw2texminted",
         "command": "pweave",
         "args": ["-f", "texminted", "%DOC_EXT%"],
         "env": {}
       },
       {
         "name": "tectonic",
         "command": "tectonic",
         "args": ["--synctex", "--keep-logs", "%DOC%.tex"],
         "env": {}
       }
     ],
     "latex-workshop.latex.recipes": [
       {
         "name": "xelatex",
         "tools": ["xelatex"]
       },
       {
         "name": "latexmk",
         "tools": ["latexmk"]
       },
       {
         "name": "latexmk (latexmkrc)",
         "tools": ["latexmk_rconly"]
       },
       {
         "name": "latexmk (lualatex)",
         "tools": ["lualatexmk"]
       },
       {
         "name": "latexmk (xelatex)",
         "tools": ["xelatexmk"]
       },
       {
         "name": "pdflatex -> bibtex -> pdflatex * 2",
         "tools": ["pdflatex", "bibtex", "pdflatex", "pdflatex"]
       },
       {
         "name": "Compile Rnw files",
         "tools": ["rnw2tex", "latexmk"]
       },
       {
         "name": "Compile Jnw files",
         "tools": ["jnw2tex", "latexmk"]
       },
       {
         "name": "Compile Pnw files",
         "tools": ["pnw2tex", "latexmk"]
       },
       {
         "name": "tectonic",
         "tools": ["tectonic"]
       }
     ]
   }
   ```

## Usage

Create a new file named `main.tex` and enter the following content. Then click the green arrow at the top right to compile the project. After that, click the magnifying glass icon on the right to view the generated PDF file.

```tex
\documentclass{article}
\usepackage{xeCJK}

\begin{document}
   Hello World, this is \LaTeX

   \LaTeX 中文文字測試
\end{document}
```
