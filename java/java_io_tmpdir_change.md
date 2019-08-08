# Java 临时目录及目录调整

java.io.tmpdir用于获取系统的临时目录。

不同系统，临时目录地址不同：
1. Windows：C:\Users\登录用户~1\AppData\Local\Temp\
2. Solaris：/var/tmp/
3. Linux: /tmp/
4. Mac OS: /tmp/

一般系统都存在对临时目录的清理机制。

如果要修改临时目录地址，需要在调用JVM时指定路径：
`java -Djava.io.tmpdir=/path/to/tmpdir `

参考
1. https://www.cnblogs.com/zhaoyue1215/p/9178109.html
