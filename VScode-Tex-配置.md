title: VScode Tex 配置
categories: 编程
tags: [编程]
date: 2019-08-18 23:27:00
---
转载
---

# 配置

```json

{
    // Latex workshop
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
          }
        ],
    "latex-workshop.latex.recipes": [
          {
            "name": "xelatex",
            "tools": [
            "xelatex"
                        ]
                  },
          {
            "name": "latexmk",
            "tools": [
            "latexmk"
                        ]
          },

          {
            "name": "pdflatex -> bibtex -> pdflatex*2",
            "tools": [
            "pdflatex",
            "bibtex",
            "pdflatex",
            "pdflatex"
                        ]
          }
        ],
    "latex-workshop.view.pdf.viewer": "tab",
    "latex-workshop.latex.clean.enabled": true,
    "latex-workshop.latex.clean.fileTypes": [
        "*.aux",
        "*.bbl",
        "*.blg",
        "*.idx",
        "*.ind",
        "*.lof",
        "*.lot",
        "*.out",
        "*.toc",
        "*.acn",
        "*.acr",
        "*.alg",
        "*.glg",
        "*.glo",
        "*.gls",
        "*.ist",
        "*.fls",
        "*.log",
        "*.fdb_latexmk"
      ],

}
```
———————————————— 
版权声明：本文为CSDN博主「超级杰哥」的原创文章，遵循CC 4.0 by-sa版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/autoliuweijie/article/details/80317313