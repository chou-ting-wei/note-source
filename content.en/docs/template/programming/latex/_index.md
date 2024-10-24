---
title: LaTeX
type: docs
---

# LaTeX

## main.tex

```tex
%%
%%  main.tex
%%  LaTeX
%%
%%  Created by userwei
%%

\documentclass[a4paper, 12pt]{article}
\usepackage{fontspec, xeCJK, xunicode-addon}
    \xeCJKsetup{AutoFakeBold=true, AutoFakeSlant=true}
    \setCJKmainfont{KaiTi} % For Windows
    % \setCJKmainfont{Kaiti TC} % For MacOS
    \setmainfont{Times New Roman}
\usepackage[left=1.5cm, right=1.5cm, top=2cm, bottom=2cm]{geometry}
\linespread{1.2}
\usepackage{fancyhdr}
\usepackage{graphicx, float, subfigure, picinpar, adjustbox}
\usepackage{amsmath, amssymb, mathtools, tabularx}
\usepackage{hyperref, forest, multicol}
\newcolumntype{Y}{>{\centering\arraybackslash}X}

\usepackage{enumitem}
\setlength\parindent{0pt}
\setenumerate[1]{itemsep=0pt,partopsep=0pt,parsep=\parskip,topsep=0pt}
\setenumerate[2]{itemsep=0pt,partopsep=0pt,parsep=\parskip,topsep=0pt}
\setenumerate[3]{itemsep=0pt,partopsep=0pt,parsep=\parskip,topsep=0pt}
\setenumerate[4]{itemsep=0pt,partopsep=0pt,parsep=\parskip,topsep=0pt}
\setitemize[1]{itemsep=0pt, partopsep=0pt, parsep=\parskip, topsep=0pt}
\setitemize[2]{itemsep=0pt, partopsep=0pt, parsep=\parskip, topsep=0pt}
\setitemize[3]{itemsep=0pt, partopsep=0pt, parsep=\parskip, topsep=0pt}
\setitemize[4]{itemsep=0pt, partopsep=0pt, parsep=\parskip, topsep=0pt}

\usepackage{color}
\definecolor{codegreen}{rgb}{0,0.6,0}
\definecolor{codegray}{rgb}{0.5,0.5,0.5}
\definecolor{codepurple}{rgb}{0.58,0,0.82}
\definecolor{backcolour}{rgb}{0.95,0.95,0.92}

\usepackage{listings}
\lstset{
language=Python,
basicstyle=\footnotesize\ttfamily,
backgroundcolor=\color{backcolour},
commentstyle=\color{codegreen},
keywordstyle=\color{magenta},
numberstyle=\tiny\color{codegray},
stringstyle=\color{codepurple},
numbers=left,
numberstyle=\footnotesize,
stepnumber=1,
numbersep=5pt,
tabsize=4,
showspaces=false,
showstringspaces=false,
showtabs=false,
frame=leftline,
xleftmargin=2em,
breaklines=true
}

\begin{document}

\pagestyle{fancy}
\fancyhead{}
\lhead{}
\rhead{}

\end{document}
```
