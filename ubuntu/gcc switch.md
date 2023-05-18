# gcc版本降级

查看已安装的gcc版本： ls /usr/bin/gcc*
如果版本中没有4.8版本，则安装：sudo apt-get install gcc-4.8
将4.8版本的优先级提高： sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 100
g++版本降级：

查看已安装的g++版本： ls /usr/bin/g++*
如果版本中没有4.8版本，则安装：sudo apt-get install g+±4.8
将4.8版本的优先级提高： sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g+±4.8 100
————————————————
版权声明：本文为CSDN博主「南洲.」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/zhou4411781/article/details/100083373