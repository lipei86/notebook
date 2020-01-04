# 安装 JupyterLab
JupyterLab 作为Jupyter Notebook的下一代数据科学工具。是一个类似于IDE的环境。

`pip install jupyterlab`

在python的虚拟环境下，会默认把jupyter的程序存储在venv\Scripts目录下。

执行：
`venv_py3\Scripts\jupyter-lab.exe`

# 遇到的问题
## 找不到 cl.exe
cl.exe是windowns的c++编译工具，需要安装visual studio。下载visual studio installer 后，可以选择只安装msvc build组件。

## 找不到 basetsd.h 
basetsd.h是windows 10 sdk的文件，需要使用visual studio installer安装windows 10 sdk组件。

## 找不到 rc.exe
在 program files 文件夹下搜索rc.exe, 并把文件夹路径加入PATH环境变量。

## Python38\lib\asyncio\events.py add_reader NotImplementedError


# 参考
https://blog.csdn.net/zhouzixin053/article/details/102599456
https://www.jianshu.com/p/a7963ebecbe4
