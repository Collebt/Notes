# 进行论文引用

```
\thispagestyle{fancy}
\addcontentsline{toc}{chapter}{参考文献}
\nocite{*} %不引用但是显示文献
\thispagestyle{fancy}
\bibliography{includefile/survey}
\thispagestyle{fancy}
```



注意`\bibliography{includefile/survey}`	里面要写上相对路径，否则识别不了。对应\includefile/survey.bib文件。



`\nocite{*}`用于对文中没有引用的论文，但是最后在列表也会显示出来。