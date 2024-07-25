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
       }
     ],
     "latex-workshop.latex.recipes": [
       {
         "name": "xelatex",
         "tools": ["xelatex"]
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
