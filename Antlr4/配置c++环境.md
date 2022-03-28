# 配置 c++ 环境

以下是官方文档中关于构建动态库的描述：  

``` Shell
cd <antlr4-dir>/runtime/Cpp (this is where this readme is located)  # 实际上这个路径在我这应该是 /home/root/runtime-cpp
mkdir build && mkdir run && cd build
cmake .. -DANTLR_JAR_LOCATION=full/path/to/antlr4-4.5.4-SNAPSHOT.jar -DWITH_DEMO=True
# 编译生成的动态链接库文件放在 /home/root/runtime-cpp/dist
make
DESTDIR=<antlr4-dir>/runtime/Cpp/run make install  # 这一步产生的文件都被放在了 /home/root/runtime-cpp/run/usr/local/include/antlr4-runtime/ 如果我不指定路径是不是就会放在到正确的地方？ 
```

---------------------

构建镜像需要做的事：  

更新 apt-get  
安装 default-jdk(antlr4的依赖)  
安装 vim(为了能够在容器中编辑)  

建立动态库依赖：  
安装 uuid-dev  
安装 cmake  
安装 pkg-config  
安装 git :  
``` Shell
apt-get install libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev
apt-get install git
```

最后安装 g++ 或 clang++

以上部分在 dockerfile 中已经构建好  

dockerfile 源码:  
``` Dockerfile
FROM ubuntu
COPY antlr-4.9.2-complete.jar /usr/local/lib
RUN apt-get update\
  && apt-get install vim -y\
  && apt-get install default-jdk -y\
  && apt-get install uuid-dev -y\
  && apt-get install cmake -y\
  && apt-get install g++ -y\
  && apt-get install pkg-config -y\
  && apt-get install -y libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev\
  && apt-get install git -y
RUN echo "export CLASSPATH='.:/usr/local/lib/antlr-4.9.2-complete.jar:$CLASSPATH'" >> /etc/bash.bashrc\
  && echo "alias antlr4='java -jar /usr/local/lib/antlr-4.9.2-complete.jar'" >> /etc/bash.bashrc\
  && echo "alias grun='java org.antlr.v4.gui.TestRig'" >> /etc/bash.bashrc\
  && echo "export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib" >> /etc/bash.bashrc\
  && mkdir -p /home/root/runtime-cpp
COPY runtime-cpp /home/root/runtime-cpp
WORKDIR /home/root/runtime-cpp
RUN mkdir build && mkdir run && cd build\
  && cmake ..\
  && make\
  && make install
```

---------------------

antlr-4.9.2-complete.jar 文件放在了 /usr/local/lib/ 中  
容器中必须有个 runtime-cpp 源码，设置其所在路径为 `export ANTLR_RUNTIME=该绝对路径`  
~~之后运行以下代码~~已添加至 dockerfile 中，现在的环境创建容器即可用:  
``` Shell
cd $ANTLR_RUNTIME
mkdir build && mkdir run && cd build
cmake .. # 虽然在官方文档中使用了参数，但是这里我们不生成测试实例，所以不加参数
make # 可能需要多等待一会 git clone，如果长时间都不行那还是新来一遍吧，这涉及到代理问题
make install # 不要参考官方文档使用 DESRDIR 参数！使用默认路径即可，不然还得手动移动
```

之后使用老师给的例子  
``` Shell
antlr4 JSON.g4 -Dlanguage=Cpp
g++ *.cpp -o main -I/usr/local/include/antlr4-runtime -lantlr4-runtime  
```

成功编译后，可以尝试运行 `./main test.json` 如果成功则说明配置成功  

但是运行时还可能出现错误提示：无法加载共享库......  
该问题出现原因可能是因为 .so 动态库文件放在了 “/usr/local/lib” 而不是 “/usr/lib” 中有关

**~~解决方法~~(以将其添加到镜像构建环节，无需手动解决)**；
``` Shell
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib
```

若成功运行程序则说明配置成功  
