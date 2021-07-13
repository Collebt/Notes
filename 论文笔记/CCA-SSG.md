# CCA-SSG

ori: only loss_inv: acc:78.70



loss_inv + 1e-3*loss_dec: acc:84.4

loss_inv + 1e-2*loss_dec: acc:69.3



loss_inv + 1e-3loss_dec + 1e-10loss_tec: acc:83

loss_inv + 1e-3loss_dec + 1e-9loss_tec: acc:73.5

loss_inv + 1e-2loss_dec + 1e-10loss_tec: acc:70.90



have a better perform

```
loss_inv = ((z1 - z2)**2).sum()/N
```

0.85.2

