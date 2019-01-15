---
layout: post                                                    
title:  "Ubuntu下使用VScode配置latex"
categories: latex
tags: Linux Latex
author: Tree 
---  

* content                                                  
{:toc}

1. 下载texlive安装，包含了latex所需的基本环境。
2. 下载VScode安装。
3. `ctrl`+`,`打开配置，点击右上角`Open Settings(JSON)`，然后在右边的`User Settings`的花括号内添加以下内容（前一段的配置如果没有逗号`,`需要自己添加上）
```
"latex-workshop.latex.recipes": [
      {
        "name": "xelatex",
        "tools": [
          "xelatex"
        ]
      },
      {
        "name": "xelatex -> bibtex -> xelatex*2",
        "tools": [
          "xelatex",
          "bibtex",
          "xelatex",
          "xelatex"
        ]
      }
    ],
    "latex-workshop.latex.tools": [
      {
        "name": "latexmk",
        "command": "latexmk",
        "args": [
          "-synctex=1",
          "-interaction=nonstopmode",
          "-file-line-error",
          "-pdf",
          "%DOC%"
        ]
      },
      {
        "name": "pdflatex",
        "command": "pdflatex",
        "args": [
          "-synctex=1",
          "-interaction=nonstopmode",
          "-file-line-error",
          "%DOC%"
        ]
      },
      {
        "name": "bibtex",
        "command": "bibtex",
        "args": [
          "%DOCFILE%"
        ]
      },
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
    "latex-workshop.view.pdf.viewer": "tab",
```
保存