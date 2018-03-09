### 路径和名字的获取方式

```
# -*- coding: utf-8 -*-
# @Time    : 2018/3/8 10:31
# @Author  : superman
# @FileName: test.py
# @Software: PyCharm
# @Blog    ：

import os,sys

if __name__ == '__main__':
    filename = __file__
    print("filename : ", filename)
    filepath = os.path.abspath(filename)
    print("filepath : ", filepath)
    dirname = os.path.dirname(__file__)
    print("dirname : ", dirname)
    dirpath = os.path.abspath(dirname)
    print("dirpath : ", dirpath)
    
输出：
filename :  C:/Users/dell/Desktop/git/SimpleStorageServer-Windows10/test.py
filepath :  C:\Users\dell\Desktop\git\SimpleStorageServer-Windows10\test.py
dirname :  C:/Users/dell/Desktop/git/SimpleStorageServer-Windows10
dirpath :  C:\Users\dell\Desktop\git\SimpleStorageServer-Windows10
```



### os.walk的用法

```
os.walk(directorypath, topdown=True, onerror=None, followlinks=False)
可以得到一个三元tupple(dirpath, dirnames, filenames)
#这里directorypath 必须是一个目录的路径，如果是一个文件的路径，则不会得到任何东西

第一个为起始路径，第二个为起始路径下的文件夹，第三个是起始路径下的文件。
dirpath 是一个string，代表目录的路径，
dirnames 是一个list，包含了dirpath下所有子目录的名字。
filenames 是一个list，包含了非目录文件的名字。
这些名字不包含路径信息，如果需要得到全路径，需要使用os.path.join(dirpath, name).

通过for循环自动完成递归枚举

import os,sys
if __name__ == '__main__':
    filename = __file__
    print("filename : ", filename)
    filepath = os.path.abspath(filename)
    print("filepath : ", filepath)
    dirname = os.path.dirname(__file__)
    print("dirname : ", dirname)
    dirpath = os.path.abspath(dirname)
    print("dirpath : ", dirpath)

    # for dirpaths, dirnames, filenames in os.walk(filepath):
    #     print(dirpaths, dirnames, filenames)

    # for dirpaths, dirnames, filenames in os.walk(dirpath, topdown=False):
    for dirpaths, dirnames, filenames in os.walk(dirpath):
        print(dirpaths, dirnames, filenames)
        # print(dirpaths, filenames)
        # for i in filenames:
        #     print(os.path.join(dirpaths,i))
        # for j in dirnames:
        #     print(os.path.join(dirpaths, j))
    # pass

输出：
filename :  C:/Users/dell/Desktop/git/SimpleStorageServer-Windows10/test.py
filepath :  C:\Users\dell\Desktop\git\SimpleStorageServer-Windows10\test.py
dirname :  C:/Users/dell/Desktop/git/SimpleStorageServer-Windows10
dirpath :  C:\Users\dell\Desktop\git\SimpleStorageServer-Windows10
C:\Users\dell\Desktop\git\SimpleStorageServer-Windows10 ['.git', '.idea', 'config', 'test'] ['.gitignore', '.gitlab-ci.yml', 'README.md', 's3-aws.py', 's3-minio.py', 'test.py']
C:\Users\dell\Desktop\git\SimpleStorageServer-Windows10\.git ['hooks', 'info', 'logs', 'objects', 'refs'] ['config', 'description', 'FETCH_HEAD', 'HEAD', 'index', 'ORIG_HEAD', 'packed-refs']
C:\Users\dell\Desktop\git\SimpleStorageServer-Windows10\.git\hooks [] ['applypatch-msg.sample', 'commit-msg.sample', 'post-update.sample', 'pre-applypatch.sample', 'pre-commit.sample', 'pre-push.sample', 'pre-rebase.sample', 'pre-receive.sample', 'prepare-commit-msg.sample', 'update.sample']
C:\Users\dell\Desktop\git\SimpleStorageServer-Windows10\.git\info [] ['exclude']
C:\Users\dell\Desktop\git\SimpleStorageServer-Windows10\.git\logs ['refs'] ['HEAD']
C:\Users\dell\Desktop\git\SimpleStorageServer-Windows10\.git\logs\refs ['heads', 'remotes'] []
C:\Users\dell\Desktop\git\SimpleStorageServer-Windows10\.git\logs\refs\heads [] ['master']
C:\Users\dell\Desktop\git\SimpleStorageServer-Windows10\.git\logs\refs\remotes ['origin'] []
C:\Users\dell\Desktop\git\SimpleStorageServer-Windows10\.git\logs\refs\remotes\origin [] ['HEAD', 'master', 'release']
...

发现了吗，如果dirpath下面的是目录，则walk还会遍历dirpath下面的文件和目录
所以功能通过下面这段代码，可以实现，递归的显示目录或者文件
        # for i in filenames:
        #     print(os.path.join(dirpaths,i))
        # for j in dirnames:
        #     print(os.path.join(dirpaths, j))
```

### 与os.listdir() 的区别

```
listdir会显示目录下的文件和目录，没有递归，不区分文件和目录
import os,sys

if __name__ == '__main__':
    filename = __file__
    print("filename : ", filename)
    filepath = os.path.abspath(filename)
    print("filepath : ", filepath)
    dirname = os.path.dirname(__file__)
    print("dirname : ", dirname)
    dirpath = os.path.abspath(dirname)
    print("dirpath : ", dirpath)

    test = os.listdir()
    print(test)
    
输出：
filename :  C:/Users/dell/Desktop/git/SimpleStorageServer-Windows10/test.py
filepath :  C:\Users\dell\Desktop\git\SimpleStorageServer-Windows10\test.py
dirname :  C:/Users/dell/Desktop/git/SimpleStorageServer-Windows10
dirpath :  C:\Users\dell\Desktop\git\SimpleStorageServer-Windows10
['.git', '.gitignore', '.gitlab-ci.yml', '.idea', 'config', 'README.md', 's3-aws.py', 's3-minio.py', 'test', 'test.py']
```

