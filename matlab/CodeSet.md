# CodeSet of MATLAB

### calculate the distance of 2 points set( high dimension features)

$$
{\bf x} \in R^{n\times d}, {\bf y} \in R^{n\times d}\\
{\bf D}_{ij} = ||{\bf x}_i - {\bf y}_j||_2^2\\
{\bf D} = xx^T+yy^T-2xy^T
$$



```
XX = sum(X' .* X'); YY = sum(Y' .* Y'); XY = X * Y';
D = repmat(XX', [1, n2]) + repmat(YY, [n1, 1]) - 2 * XY;
```





the feature of node should use the histogram 
