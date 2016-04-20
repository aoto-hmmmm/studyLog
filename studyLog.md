# 小记
##1. [pandoc](http://www.pandoc.org/)
###- 将.md文件转换成.docx文件命令
> pandoc -f markdown -t html ./input.md | pandoc -f html -t docx -o output.docx