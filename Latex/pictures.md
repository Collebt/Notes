# 加入图片

```latex
\begin{figure}[h]
\entering
\includegraphics[width=4cm, height=5cm]{3}
\caption{这是图片，名字为3.png}
\end{figure}
```



上面的公式缩放有点问题



```latex
\begin{figure}
    \centering
    \includegraphics[width=0.7\textwidth]{examples/pictures/graph1.png}
    \caption{解决大视差问题的图匹配示意图}
    \label{fig:graph matching}
\end{figure}
```



引用方法（包括公式也是这个用法）：

```latex
\ref{fig:graph matching}
```





引用论文是cite

```latex
\cite{paper_reference}
```



$H_2$ H~2~O

