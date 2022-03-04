

# eclipes下载与配置中文（超详细2021年最新版）

<font color='red'>注意：</font>不想看步骤想直接下的话[Eclipse downloads - Select a mirror | The Eclipse Foundation](https://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/2021-06/R/eclipse-java-2021-06-R-win32-x86_64.zip)点击这里就好了，会直接跳到下载页面。

####一：下载与安装eclipes

1. 搜索eclipes

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910175454374.png" alt="image-20210910175454374" style="zoom: 50%;" />

2. 进入官网

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910175714039.png" alt="image-20210910175714039" style="zoom:50%;" />

3. 进去官网之后点击这里<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910180147413.png" alt="image-20210910180147413" style="zoom:50%;" />

4. 选择下载的版本，我这里选的是javaee，第一个版本是纯净版没有多余的插件，第二个版本为你搭建好了企业web开发的插件，建议下载第二个。

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910180400282.png" alt="image-20210910180400282" style="zoom: 33%;" />

5. 如图

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910175402003.png" style="zoom: 33%;" />

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910181057063.png" alt="image-20210910181057063" style="zoom: 33%;" />

6. 解压，注意记住解压好的地址免得找不到eclipes的启动程序，如果在解压过程中遇到了有些文件解压不了，直接选择跳过，不用管它。

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910180548812.png" alt="image-20210910180548812" style="zoom:50%;" />

7. 双击exe文件成功运行

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910181434028.png" alt="image-20210910181434028" style="zoom: 50%;" />



####二:（创建java项目教学）：选择自己需要创建项目的文件夹，点击launch

1. 第一步创建一个项目文件夹

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910181735249.png" alt="image-20210910181735249" style="zoom:50%;" />

2. 第二步点击file创建一个java项目

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910181954246.png" alt="image-20210910181954246" style="zoom:33%;" />

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910182049865.png" alt="image-20210910182049865" style="zoom:33%;" />

![image-20210910182139867](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910182139867.png)

​																			

**点击下面的Finish**

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910182302503.png" alt="image-20210910182302503" style="zoom:50%;" />

**输入项目名称**

![image-20210910182451357](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910182451357.png)



![image-20210910182547432](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910182547432.png)

​						**把welcome关闭点击welcome右上角的叉叉，我这里用老图了**

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910182624348.png" alt="image-20210910182624348" style="zoom: 33%;" />

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910182852446.png" alt="image-20210910182852446" style="zoom:33%;" />

**输入以下代码：**

~~~java
public static void main(String[] args) {
		System.out.println("你好世界，你好java");
	}
~~~

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910183031321.png" alt="image-20210910183031321" style="zoom:33%;" />

####三：汉化eclipes

1. 下载汉化包，点击以下链接，找到Language：Chinese，如下操作，点击链接即可下载

https://download.eclipse.org/technology/babel/babel_language_packs/R0.18.1/2020-09/2020-09.php

![image-20210910184539520](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910184539520.png)

2. 解压语言包：

![image-20210910184652418](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910184652418.png)

3. 如图

![image-20210910184833952](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910184833952.png)

4. 将解压好的文件复制

5. 找到eclipes应用程序的安装目录，将复制的文件整个粘到eclipes根源目录中，并替换相关文件，重启即可汉化成功

![image-20210910185242896](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210910185242896.png)

![image-20210911084242912](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911084242912.png)
