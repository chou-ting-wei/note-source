---
title: Installation
type: docs
---

# Installation

## Install BasicTeX

1. Install BasicTeX via Homebrew
   ```sh
   brew install --cask basictex
   ```
2. Add TeX binaries to your PATH

   - For Bash or Zsh
     ```sh
     export PATH="/Library/TeX/texbin:$PATH"
     ```
   - For Fish Shell
     ```sh
     set -U fish_user_paths /Library/TeX/texbin $fish_user_paths
     ```

3. Install additional LaTeX packages

   - Update `tlmgr`
     ```sh
     sudo tlmgr update --self
     ```
   - Install common packages
     ```sh
     sudo tlmgr install collection-latexrecommended
     ```
   - Install specific packages

     ```sh
     sudo tlmgr install fontspec
     sudo tlmgr install xetex
     ```

4. Verify the installation
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
