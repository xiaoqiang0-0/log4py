# log4py

> python日志简单实现

主要用于pypi学习

## pypi仓库搭建
> 基于`nexus3`

1) 创建`pypi-hosted`仓库  
    hosted仓库用于存储私有模块
2) 创建`pypi-proxy`仓库  
    > 代理地址不要加`simple`
    `proxy`仓库用于代理外部仓库
3) 创建`pypi-group`仓库  
    应该包括hosted和proxy，主要用于对外统一暴露
    > 可以配置到`pip.conf`中，后边需要加`simple`
4) 本地用户目录下增加`~/.pypirc`文件  
    内容示范：
    ```
    [distutils]
    index-servers =
        pypi
     
    [pypi]
    repository:https://pypi.python.org/pypi
    username:your_username
    password:your_password
    ```
    > `pypi`为自定义上传服务器`id`类似`maven`中`setting.xml`中的`server`节点，可以在`index-servers`的值后追加，直接换行即可，无需分割符号
5) 客户端增加`~/.pip/pip.conf`文件  
    用于配置私服地址，index-url直接写group仓库地址加simple结尾即可
    ```
    [global] 
    index-url = https://pypi.tuna.tsinghua.edu.cn/simple
    [install]
    trusted-host = https://pypi.tuna.tsinghua.edu.cn 
    ```    
## 发布
> 参考[官方文档](https://docs.python.org/zh-cn/3/distributing/index.html)
1) 安装发布工具  
    ```
    python -m pip install setuptools wheel twine
    ```
2) 构建
    ```
    python setup.py sdist bdist_wheel
    ```
3) 上传
    ```
    twine upload -r pypi dist/* 
    ```
    > -r即指明服务器id，可以是`.pypirc`下的任一可用地址，即可发布到远程仓库

## 安装
1) 客户端创建`~/.pip/pip.conf`  
2) 安装
    ```pip
    pip install xxx
    ```