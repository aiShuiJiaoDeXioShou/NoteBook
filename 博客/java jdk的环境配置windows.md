# java环境配置（以安装java17为例）

***前言：***本图文教程使用的是win11，面向纯小白，官方安装网址：[Java Downloads | Oracle](https://www.oracle.com/java/technologies/downloads/)

***其他版本：***[JDK Builds from Oracle (java.net)](http://jdk.java.net/)

## 一. 安装jdk，跟着图走，我这里以安装jdk17为例

![image-20210919223156283](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210919223156283.png)

**虽然是全英文页面，但是微软有官方的翻译器，实在看不懂可以翻译**

![image-20210919223429077](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210919223429077.png)

​	![image-20210919223708242](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210919223708242.png)

***注意***：**官方提供的安装版本，实际上就是帮你解压**

![image-20210919223631002](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210919223631002.png)

![image-20210919224041395](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210919224041395.png)

![image-20210919224159194](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210919224159194.png)

<font color='red'>	***友情提示***：</font>**一定要记住自己的安装位置，你是解压包的话就记住解压包位置**

## 二. 配置环境变量

1. 我们来到桌面点击下面的搜索框，输入环境变量

   <img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210919224454882.png" alt="image-20210919224454882" style="zoom: 67%;" />
   <img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210919225117099.png" alt="image-20210919225117099" style="zoom: 67%;" />

   <img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210919225321279.png" alt="image-20210919225321279" style="zoom: 67%;" />
   	**用户变量跟环境变量对于新人来说没有本质的区别，以后不想麻烦的话就新建环境变量，两个变量只要建一个就够了。**

   ​	**我们点击新建之后把变量名叫做**<font color='red'>JAVA_HOME</font>**，记住一定要是这个名字，祖宗之法不可变**，**如下图我的这个是按照默认安装目录的**

   ​	![image-20210919225624881](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210919225624881.png)

   ![image-20210919225931511](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210919225931511.png)

   ​	**之后我们点击Path编辑**，**在里面点击新建**,**输入这一串值**

   > %JAVA_HOME%\bin

   ![image-20210919230050155](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210919230050155.png)

   ![image-20210919230258630](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210919230258630.png)

2. 确定是否环境变量配置成功：win（图标为windows图标的那个键）+g输入cmd，打开之后输入***java -version***，能看到版本信息就表示安装成功。

   > java version "17" 2021-09-14 LTS
   > Java(TM) SE Runtime Environment (build 17+35-LTS-2724)
   > Java HotSpot(TM) 64-Bit Server VM (build 17+35-LTS-2724, mixed mode, sharing)

![image-20210919224629776](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210919224629776.png)

**![image-20210919230626949](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210919230626949.png)**

