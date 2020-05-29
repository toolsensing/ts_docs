# 图迅科技技术文档Tex模版

## 项目起源

LaTeX利用设置好的模板，可以编译为格式统一的pdf。

word由于其强大的功能与灵活性，在新手面对形式固定的文档时，排版、编号、参考文献等简单事务反而会带来很多困难与麻烦，对于一些需要通篇修改的问题，要想达到LaTeX的效率，对word使用者来说需要具有较高的技能水平。

为了能把主要精力放在文档撰写上，使用LaTeX撰写文档具有诸多好处，新手不需要关心格式问题，只需要按部就班的使用少数符号标签，即可得到符合要求的文档。且在需要全篇格式修改时，更换或修改模板文件，即可直接重新编译为新的样式文档，这对于word新手使用word的感受来说是不可思议的。

LaTeX 的核心思想在于内容与格式的分离。 LaTeX的意义在于让作者从格式中解脱。

LaTeX 的创始者 Leslie Lamport 曾被问道人们在使用 LaTeX 时应停止犯的错误时，其回答如下：

>"Worrying too much about formatting and not enough about content."
>
>"Worrying too much about formatting and not enough about content."
>
>"Worrying too much about formatting and not enough about content."

这个回答也同样适用于ts_tech_doc的使用者。 技术文档写作最重要的是通过规范的写作表达自己的思想和成果，而不是纠结于某些格式及样子上的差异。当花费过多的时间关注和修葺文档的格式而非内容时，往往是想逃避写作而表现出的拖延症状。在此，与大家共省。

本项目的目的是为了创建一个符合成都图迅科技有限公司技术文档撰写规范的TeX模板，解决各类技术文档撰写时格式调整的痛点。

## 主要内容

1. 封面、扉页；
2. 目录；
3. 符号说明（必要时）；
4. 缩略词释义（必要时）；
5. 正文；
6. 参考文献；
7. 附录（必要时）；

## 版本状况
此版本为通用版本，具体技术文档需要自行修改`ts_tech_doc.cls`文件。

## 文件介绍

### `ts_tech_doc.cls`

样式文件，通用版本，具体文档可能要更改此文件。

### `gbt7714-unsrt.bst`和`gbt7714.sty`两个文件

来自项目[CTeX-org/gbt7714-bibtex-style](https://github.com/CTeX-org/gbt7714-bibtex-style)，是参考文献的样式。


### `content`目录

所有文档需要编辑的内容都在这里。

`info.tex`：文档的各种信息, 封面标题，日期等。

`content.tex`：从绪论到总结的全部正文内容。`\cite`的时候可能因为tex文件与主文件分离，LaTeX环境配置不到位，会有找不到bib的提示（Texlive+sublime会这样），没关系，照常插入需要的bibkey即可。

### `ts_tech_doc_main.tex`

文档主文件，正常情况下不用修改这个文件，以这个文件编译文档即可。

在content目录提供的页面不足以保证所需内容时，可以修改主文件，引入其他自定义content文件。

### `images`目录

放图片，模板已经配置了相对路径，所以在文中插图片时，直接用images目录下的相对路径即可，比如`images/logo.jpg`，在正文中插入只需要`logo.jpg`。

## 编译

`Linux`
```bash
# 单次编译
make
# 持续集成
make pvc
```
或者
请使用`xelatex`，对`ts_tech_doc_main.tex`文件进行编译。
Windows下可以使用`TexMaker`,`TexStudio`等IDE，选中`xelatex`编译器进行编译。
使用高级文本编辑器，如sublime等，否则可能因为ANSI、UTF-8等编码格式问题编译失败。

## Texlive安装

### 1. Windows10 + Texlive2020

安装包位于 \\192.168.0.102\public\02_IT\软件安装包\texlive2020.iso  
双击打开  
以管理员身份运行install-tl-windows.bat  
所有安装选项默认就行, 等待安装完成  
安装完成后打开cmd命令窗口，输入tex -v验证安装是否成功，若出现tex版本号的信息，说明安装成功  

### 2. 编辑器配置

理论上，任何文本编辑器都可以编辑LaTex源代码，然后通过命令行编译。  
也可以用texlive自带的编辑器TeXwords editor， 提供了一些简单的GUI操作。  
或者用集成开发环境TeX Studio。  
不过，还是推荐用vscode + LaTex Workshop插件的方式。

vscode 和 LaTex Workshop插件的安装就不介绍了，下面是安装好之后LaTex Workshop的配置命令，快捷键Ctrl+Shift+P，在弹出的命令窗口输入Preferences:Open Settings (JSON),按Enter键，将下面的代码添加进打开的setting.json文件即可

```json
"latex-workshop.latex.autoBuild.run": "never",
"latex-workshop.message.error.show": false,
"latex-workshop.message.warning.show": false,

"latex-workshop.latex.tools": [
	{
		"name": "xelatex",
		"command": "xelatex",
		"args": [
			"-synctex=1",
			"-interaction=nonstopmode",
			"-file-line-error",
			"%DOCFILE%"
		]
	},
	{
		"name": "pdflatex",
		"command": "pdflatex",
		"args": [
			"-synctex=1",
			"-interaction=nonstopmode",
			"-file-line-error",
			"%DOCFILE%"
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
		],
	},
	{
		"name": "pdflatex",
		"tools": [
			"pdflatex"
		]
	},
	{
		"name": "xe->bib->xe->xe",
		"tools": [
			"xelatex",
			"bibtex",
			"xelatex",
			"xelatex"
		]
	},
	{
		"name": "pdf->bib->pdf->pdf",
		"tools": [
			"pdflatex",
			"bibtex",
			"pdflatex",
			"pdflatex"
		]
	}
],
```