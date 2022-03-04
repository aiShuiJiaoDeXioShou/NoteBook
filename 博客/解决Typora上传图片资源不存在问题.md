# 解决Typora上传图片资源不存在问题

##方案一：不麻烦的方案，但是适用面小

1. **前言：**使用Typora编写的博文，因为Typora为了缩小md文件的大小，默认采用的是把图片按照指定路径显示出来，这就产生了一个问题。

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911144304690.png" alt="image-20210911144304690" style="zoom:50%;" />

2. **问题：**如果我想把在Typora书写的博文上传到网络上，比如著名问答平台知乎，就会出现如下图错误。

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911144739183.png" alt="image-20210911144739183" style="zoom:50%;" />

3. **解决问题：**知乎是支持上传docx模式，而docx模式能够储存图片，思路来了，也就是说，只要我们能够把md格式的Typora文件转化为docx格式的文件，就能够把图片上传到知乎了。**若是其他网站**，比如说CSDN：可以将转化的Word文档Ctrl+A直接粘到富文本编辑器里。无论怎样，都需要改变文件格式。

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911150122201.png" alt="image-20210911150122201" style="zoom:50%;" />

我们在Typora文件栏上可以清楚看到，Typora是支持把md文件转化为docx格式的，但是一点击，你会发现，Typora本身是不具有这个能力，要下载第三方插件。

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911150453691.png" alt="image-20210911150453691" style="zoom:50%;" />

那么我们按照官方的步骤来：

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911151707621.png" alt="image-20210911151707621" style="zoom:50%;" />

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911151830913.png" alt="image-20210911151830913" style="zoom:50%;" />

**注意：**该网址是需要加速的，推荐下载steam++加速器，在steam++里面加速github便可以访问网站。

如果访问不了-百度网盘地址：

链接：https://pan.baidu.com/s/1R3UCQ8RgXtxtR-o0vT47mQ 
提取码：ecom

**解压之后：**复制文件地址，方便寻找

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911152446925.png" alt="image-20210911152446925" style="zoom:50%;" />

![image-20210911163759953](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911163759953.png)

选择exe启动程序，这时Typora可以转化md文件为word文件了。

4. 将docx文件上传知乎，这时候图片资源显示出来了。

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911153001597.png" alt="image-20210911153001597" style="zoom: 33%;" />

##方案二：非常麻烦，适用于所有网站，只需一次，永久不用担心图片问题

1. **前言：**虽然问题解决了，但是这样操作颇为不方便，有没有什么办法可以直接将md文件导入知乎后显示？

2. **原理：**既然Typora根据源码的路径就可以显示一张图片，浏览器是访问不到本地文件夹的，那么我们只要将文件路径改为web浏览路径不就行了吗？md格式的文件能够直接在互联网上取图片，我们把图片上传到互联网上，不就可以看见了吗？

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911154506027.png" alt="image-20210911154506027" style="zoom:50%;" />

3. **解决方案**：接下来我们讲怎么做到这点，我们在Typora的设定中可以看见：

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911153817681.png" style="zoom:50%;" />

+ Typora是支持图像上传到互联网的。

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911154033567.png" alt="image-20210911154033567" style="zoom:50%;" />

+ **下载PicGo**：我们按照官方指定的步骤来，下载官方指定上传图片软件：PicGo

> 网盘链接：
>
> 链接：https://pan.baidu.com/s/17WyQUM6iw0Tn61lv4B746A 
> 提取码：72js

4. **创建互联网图像仓库：**下载好之后，我们需要找到PicGo的exe文件，打开Typora的设置，点击图片栏，将PicGo与Typora关联到一起，将软件指定路径设置为PicGo压缩包解压后的exe文件，双击exe文件，如下图：

   <img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911155056585.png" alt="image-20210911155056585" style="zoom:50%;" />

这时候上传文件会发生错误，因为你并没有创建互联网仓库，我们点击图床设置，会看到下面有很多网盘我们相当熟悉，我这里用gitee作为互联网网盘，以下操作全部用图片显示：

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911155244926.png" alt="image-20210911155244926" style="zoom: 67%;" />

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911155712246.png" alt="image-20210911155712246" style="zoom: 67%;" />

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911155846148.png" alt="image-20210911155846148" style="zoom: 67%;" />

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911160020148.png" alt="image-20210911160020148" style="zoom: 50%;" />

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911160213694.png" alt="image-20210911160213694" style="zoom: 67%;" />

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911160434264.png" alt="image-20210911160434264" style="zoom: 67%;" />

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911160909959.png" alt="image-20210911160909959" style="zoom: 50%;" />

![image-20210911161116510](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911161116510.png)

最后点击确定，设为默认图床，即可。

5. **来到Typora：**我们随便将一张图片粘贴到这里，显示https：开头的文件目录，既创建成功。

![image-20210911161251061](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911161251061.png)

或者点击设置，来到图像，点击测试文件上传：Typora会提示你文件上传成功。

**注意**：这个仓库是不能重复上传文件的，否则会显示失败，它会自动帮你找到以前已经上传过的文件路径，对使用没有什么影响，如果想看自己上传的文件，打开PicGo：在相册这里就能看到，左下角有个小文件图标，点击就能复制文件web地址。

<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210911161647093.png" alt="image-20210911161647093" style="zoom:80%;" />

6. **尾声：**将md文件导入到知乎上，这时就能看到图片了。