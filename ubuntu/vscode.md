# vscode sftp的No such file报错



 [Error: No such file (sftp liximomo extension)](https://stackoverflow.com/questions/67506693/error-no-such-file-sftp-liximomo-extension)

打开 ~/.vscode/extensions/liximomo.sftp-1.12.9/node_modu

les/ssh2-streams/lib/sftp.js

在每一个`options.emitClose = false;`下面增加:

```
options.autoDestroy = false;
```

