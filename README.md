# 在一切之前...
## 需要使用服务器的同学请通过微信私信你们的账号和密码，默认是没有的。
## omnisky用户的账号密码我会发布在群中。

# 基本使用
-   服务器内网使用IP: 192.168.1.43      &emsp;&emsp;&emsp;端口: 22 <br>

    公网IP: 123.206.59.126             &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;端口: 6000<br>
    
    统一使用SSH协议登录，使用FRP进行地址映射，[这里是FRP的GitHub页面](https://github.com/fatedier/frp)。<br>

    所以每次开关机需要重新启动 FRP。操作如下：
    ```
    登陆omnisky账号
 
    cd /home/omnisky && screen ./startFRP.sh
    ```
-  当前目录切换：`cd 目录名`

   查看 GPU 利用情况：`nvidia-smi`

   查看所有用户对于 CPU 的使用情况：`htop`
   
   查看硬盘信息：`df -h`
   
   退出：`exit`

-  机械硬盘挂载点在`/mnt/devices` 中，为了节省本来就不多的固态硬盘资源，
   
   所有同学和老师的用户在建立完成以后家目录都默认在 `/home/用户名` 中 

   初次登陆大家的家目录下的软连接 `Datas` 就是指向机械硬盘挂载点下的文件夹的 
   
   软连接如下：`Datas -> /mnt/devices/datas/用户名`

   请大家尽量将所需要的数据集、代码拷贝至此软连接文件夹中，固态硬盘空间有限，还请大家支持！

-  如果需要安装软件可以登录 `omnisky` 用户安装，或者联系服务器维护的同学。

# Python & Anaconda 指令
-  使用GPU进行运算：
    ```
    import os
    os.environ['CUDA_VISIBLE_DEVICES'] = ‘0’
    ```

-  动态分配显存：（这个在程序之中必须加上）
    ```
    config = tensorflow.ConfigProto()
    config.gpu_options.allow_growth = True
    session = tensorflow.Session(config=config)
    ```

-  Anadonda 虚拟环境
    ```
    conda create --name 环境名 python=需要的python 版本          # 创建环境
    source activate 环境名                                      # 激活环境
    source deactivate 环境名                                    # 退出环境
    conda remove --name 环境名 --all                            # 删除环境
    ```

    请在虚拟环境中配置实验需要的组件、资源版本，具体的大家可以上网参考。

    例如我的实验环境配置（仅供参考）:
    ```
    conda create –-name myEnvironment python=3.6

    source activate myEnvironment
    # 之后可以发现终端最前方出现了括号，括号内是你设置的环境名

    pip3 install keras=1.2.0
    # 安装实验所需的 1.2.0 版本的 keras

    # 之后开始实验，实验完成后……
    source deactivate myEnvironment

    # 如果不再使用了，就删除这个虚拟环境释放硬盘空间
    conda remove --name myEnvironment –all
    ```

-  更换终端后的环境变量设置（如果看不懂或者不知道啥意思的同学们可以跳过这一步）

    同学可能会更换自己喜欢的终端（比如我就换了`zsh`），更换完后可能发现conda无法使用，因为conda的环境变量默认是添加在`bash`终端的配置文件`.bashrc`中的，所以需要将相应终端的环境变量配置好，我就以`zsh`为例子为大家演示一下
    ```
    echo 'export PATH="/opt/anaconda3/bin:$PATH"' >> ~/.zshrc && source ~/.zshrc
    ```
    复制此行代码粘贴到终端执行即可。