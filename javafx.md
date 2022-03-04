# javafx

# 基本操作列表

- 官方链接地址[Overview (JavaFX 17) (openjfx.cn)](https://openjfx.cn/javadoc/17/)
- javafx第一个程序—>推荐用kotlin编写javafx,以下笔记都会有kotlin来编写代码
	```Kotlin
	/**
	 * 写一个笔记本的代码哦
	 */
	class Notebook : Application() {
	    override fun start(stage: Stage) {
	        val box = VBox()
	        //这个是javafx里面的文字链接
	        val like = Hyperlink()
	        like.text = "www.baidu.com"
	        like.setOnAction {
	            this.hostServices.showDocument(like.text)
	        }
	        box.children.setAll(like)
	        stage.scene = Scene(box)
	        stage.width = 800.0
	        stage.height = 700.0
	        stage.show()
	    }
	}
	
	//这个是java代码调用kotlin
	public class Main {
	    public static void main(String[] args) {
	        Application.launch(Notebook.class,args);
	    }
	}
	
	```
	
- 打开文字链接，跳转到浏览器：
	```Kotlin
	/**
	 * 写一个笔记本的代码哦
	 */
	class Notebook : Application() {
	    override fun start(stage: Stage) {
	        val box = VBox()
	        //这个是javafx里面的文字链接
	        val like = Hyperlink()
	        like.text = "www.baidu.com"
	        like.setOnAction {
	            this.hostServices.showDocument(like.text)
	        }
	        box.children.setAll(like)
	        stage.scene = Scene(box)
	        stage.width = 800.0
	        stage.height = 700.0
	        stage.show()
	    }
	}
	```
	
- 布局方式
	- VBox()—垂直方向的布局管理,HBox—水平方向的布局管理
		```Kotlin
		//常用方法
		//添加组件
		box.add()
		box.addAll()
		//设置组件之间的间距
		box.spacing = 10
		//设置组件之间的位置
		box.alignment = Pos.BOTTOM_RIGHT
		//所有组件设置本身的位置都一样,相对于父组件来说
		box.layoutY
		box.layoutX
		box.padding = Insets(0.0, 100.0, 0.0, 0.0)
		
		```
		
		![](image/image.png "")
		
	- AnchorPane绝对布局
		默认将组件全部放置在左上角,用于管理子组件,当用这个类去管理子组件时,默认的设置组件的位置就不有效了
		```Kotlin
		        val button = Button("这个是用于测试的按钮")
		        val pane = AnchorPane()
		        AnchorPane.setBottomAnchor(button,10.0)
		        AnchorPane.setLeftAnchor(button,10.0)
		        AnchorPane.setRightAnchor(button,10.0)
		        AnchorPane.setTopAnchor(button,10.0)
		        pane.children.add(button)
		```
		
		![](image/image_1.png "")
		~~最后的效果~~
	- Group 这个是捆绑的容器,就是用来放置组件的,没有什么用处
	- **BorderPane**(这个是方位布局)
		![](image/image_2.png "")
- 设置组件的背景
	- 这个是设置背景图片
	```Kotlin
	        //这下面是box的操作
	        box.children.setAll(button1,button2,button3,button4)
	        box.background = Background(BackgroundImage(Image(FileToolYt.获取_根源目录()+"img/hutao.jpg"),null,null,null,null))
	
	```
	
	- 设置背景图片大小自适应并且不重复
	```Kotlin
	 //这个是拿来用的,要理解请自己看源代码去
	 //设置背景不重复,BackgroundRepeat.NO_REPEAT
	 //设置背景自适应,Image(FileToolYt.获取_根源目录()+"img/hutao.jpg",stage.width,stage.height,true,true),可以去看一下Image的官方文档,文档里面说得很详细
	 box.background = Background(BackgroundImage(Image(FileToolYt.获取_根源目录()+"img/hutao.jpg",stage.width,stage.height,true,true),BackgroundRepeat.NO_REPEAT,BackgroundRepeat.NO_REPEAT,null,null))
	
	```
	
	- 下面这个是设置颜色背景`Color.valueOf("#ff7875") ` 颜色的话一般用这个吧,看源码我是吐了
	```Kotlin
	        box.children.setAll(button1,button2,button3,button4)
	        box.background = Background(BackgroundFill(Color.rgb(255, 120, 117),null,null))
	```
	
- 树状图组件TreeView
	- 官方文档位置:
		[TreeView (JavaFX 17) (openjfx.cn)](https://openjfx.cn/javadoc/17/javafx.controls/javafx/scene/control/TreeView.html)
		[TreeItem (JavaFX 17) (openjfx.cn)](https://openjfx.cn/javadoc/17/javafx.controls/javafx/scene/control/TreeItem.html)
		[JavaFX视频教程第101课，TreeView的基本使用_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1pb41127k7/?spm_id_from=pageDriver)
	- 基本方法
		```Kotlin
		//TreeItem方法:
		//设置默认展开
		treeImage.isExpanded = true
		treeImage.value = "是色图哦"
		treeImage.isLeaf //返回false表示下面有子节点,反之相反
		//TreeView方法:
		//如果面积不够,则滚动到多少
		treeView.scrollTo(13)
		//设置单元格的尺寸
		treeView.fixedCellSize = 20.0
		//这里表示是否显示根节点,我这里设置不显示根节点
		treeView.isShowRoot = false
		
		```
		
	- 下面是一个小项目(一个简单的相册)
		```Kotlin
		        //定义头部公共部分
		        val rootPane = BorderPane()
		        val treeItem = TreeItem<String>()
		        val label = VBox()
		
		        //这个是左界面的编写
		        val file = File("${FileToolYt.获取_根源目录()}img")
		        val fileList = file.listFiles()//获取这个目录里面的图片
		        for (file in fileList) {
		            val item = TreeItem(file.name)
		            item.addEventHandler(MouseEvent.MOUSE_CLICKED) {
		                println(file.path)
		            }
		            treeItem.children.add(item)
		        }
		
		        val treeView = TreeView(treeItem)
		        rootPane.left = treeView
		
		        //这个是右界面的编写
		        rootPane.center = label
		        stage.scene = Scene(rootPane)
		        stage.width = 1000.0
		        stage.height = 800.0
		        stage.icons.add(Image("${FileToolYt.获取_根源目录()}img/icon.png"))
		        stage.show()
		```
		
		![](image/image_3.png "")
	
- 打包
	复制这段代码进去，点击package就可以打包成功了，嘻嘻
	```XML
	<build>
	        <finalName>untitled.0.1</finalName><!-- 导出jar的名字 -->
	        <plugins>
	            <plugin>
	                <groupId>org.apache.maven.plugins</groupId>
	                <artifactId>maven-shade-plugin</artifactId>
	                <version>3.2.0</version>
	                <executions>
	                    <execution>
	                        <phase>package</phase>
	                        <goals>
	                            <goal>shade</goal>
	                        </goals>
	                        <configuration>
	                            <transformers>
	                                <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
	                                    <mainClass>com.yangteng.Run</mainClass>
	                                    <!-- 主类的位置，例如上图文件，主类配置应为： -->
	                                    <!-- <mainClass>{top.nihilwater.App}</mainClass> -->
	                                </transformer>
	                            </transformers>
	                        </configuration>
	                    </execution>
	                </executions>
	            </plugin>
	        </plugins>
	    </build>
	```
	
	![](image/image_4.png "")
- 项目实现(这都是一些小项目)
	- 计算器项目
		```Kotlin
		//计算器
		class AppComputer() : Stage() {
		    private var x = 0
		    private var y = 0
		    private var moshi = true
		    private val  text = Text()
		    private val  jisuan = Text()
		    private val  text2 = Text()
		    private var result = Text()
		    private var  sum = 0.0
		    init {
		        println("这个是构造函数")
		        val gridPane = GridPane()
		        val box = VBox()
		        text.text = x.toString()
		        text2.text = ""
		        gridPane.vgap = 5.0
		        gridPane.hgap = 5.0
		
		        //设置计算机的按钮
		        val button1 = Button("1")
		        val button2 = Button("2")
		        val button3 = Button("3")
		        val button4 = Button("4")
		        val button5 = Button("5")
		        val button6 = Button("6")
		        val button7 = Button("7")
		        val button8 = Button("8")
		        val button9 = Button("9")
		        val button0 = Button("0")
		
		        val butJia = Button("+")
		        butJia.setOnMouseClicked {
		            moshi = false
		            jisuan.text = "+"
		        }
		        val butJian = Button("-")
		        butJian.setOnMouseClicked {
		            moshi = false
		            jisuan.text = "-"
		        }
		        val butChen = Button("*")
		        butChen.setOnMouseClicked {
		            moshi = false
		            jisuan.text = "*"
		        }
		        val butChu = Button("/")
		        butChu.setOnMouseClicked {
		            moshi = false
		            jisuan.text = "/"
		        }
		        val butGui = Button("归零")
		        butGui.setOnMouseClicked {
		            x = 0
		            y = 0
		            moshi = true
		            jisuan.text = ""
		            text2.text = ""
		            text.text = ""
		            sum = 0.0
		            result.text = ""
		        }
		        val butX = Button("<-")
		        butX.setOnMouseClicked {
		            if(moshi){
		                if(text.text.length>0){
		                    text.text = jianText(text.text).trim()
		                    x = if (text.text.isNotEmpty()) text.text.toInt() else 0
		                }else{
		                    moshi = false
		                }
		            }else{
		                if(text2.text.length>0){
		                    text2.text = jianText(text2.text).trim()
		                    y = if (text2.text.isNotEmpty()) text2.text.toInt() else 0
		                }else{
		                    jisuan.text = jianText(jisuan.text)
		                    moshi = true
		                }
		            }
		            jisuanResult()
		        }
		        val butDenyu = Button("=")
		        butDenyu.setOnMouseClicked {
		            jisuanResult()
		        }
		        gridPane.addColumn(0,button1,button2,button3,button4,button5)
		        gridPane.addColumn(1,button6,button7,button8,button9,button0)
		        for (child in gridPane.children) {
		            child.setOnMouseClicked {
		                inputText(child as Button,text,text2)
		            }
		        }
		        gridPane.addColumn(2,butJia,butJian,butChen,butChu,butGui)
		        gridPane.addColumn(3,butX,butDenyu)
		        //设置背景图片
		        try {
		            box.background = Background(BackgroundImage(Image("${FileToolYt.获取_根源目录()}img/img.png"),null,null,null,null))
		        }catch (e:IllegalArgumentException){
		            println("没有找到资源！")
		        }
		        val hBox = HBox()
		        hBox.children.addAll(text,jisuan,text2,result)
		        hBox.alignment = Pos.CENTER
		        box.children.addAll(hBox,gridPane)
		        //设置组件居中显示
		        box.alignment = Pos.CENTER
		        box.spacing = 10.0
		        gridPane.alignment = Pos.CENTER
		        val scene = Scene(box)
		        this.scene = scene
		        width = 400.0
		        height = 600.0
		    }
		    private fun inputText(button:Button,text1:Text,text2:Text){
		        if(moshi){
		            x = (x.toString() + button.text).toInt()
		            text.text = x.toString()
		        }else{
		            y = (y.toString() + button.text).toInt()
		            text2.text = y.toString()
		        }
		    }
		    private fun jianText(s:String):String{
		        var newS = ""
		        val split = s.split("")
		        var mou = 0
		        if(split.size - 1>0){
		            mou = split.size - 2
		            val subList = split.subList(0,mou)
		            for (ss in subList) {
		                newS += ss
		            }
		            return newS
		        }else{
		            return newS
		        }
		    }
		    private fun jisuanResult(){
		        when(jisuan.text){
		            "+"->sum = (x+y).toDouble();
		            "*"->sum = (x*y).toDouble();
		            "/"->sum = (x/y).toDouble();
		            "-"->sum = (x-y).toDouble();
		            else->sum = (x+y).toDouble()
		        }
		        result.text = "= ${sum}"
		    }
		}
		```
		
	- 图片显示器
		```Kotlin
		//这个是图片查看器
		class totalPage : Application() {
		    //定义头部公共部分
		    private val rootPane = BorderPane()
		    private val treeRoot = TreeItem<String>()
		    private val label = VBox()
		    private val treeImage = TreeItem<String>("图片")
		    private val file = File("${FileToolYt.获取_根源目录()}img")
		    private val fileList = file.listFiles()
		
		    override fun start(stage: Stage) {
		        val computer = AppComputer()
		        treeRoot.value = "工作区"//这个用于设定和更改所在节点的名称
		        treeRoot.isExpanded = true //设置默认展开
		        //这个是左界面的编写
		        navigation()
		        val treeView = TreeView(treeRoot)
		        //设置左侧选择事件
		        treeView.selectionModel.selectedItemProperty().addListener(
		            ChangeListener<TreeItem<String>>(
		                fun(
		                    observable: ObservableValue<out TreeItem<String>>?,
		                    oldValue: TreeItem<String>?,
		                    newValue: TreeItem<String>?
		                ) {
		                    when(newValue?.value){
		                        "计算机"-> computer.show()
		                    }
		                    for (file in fileList) {
		                        if(file.name == newValue?.value){
		                            bgImage(label,file.path,stage)
		                        }
		                    }
		                })
		        )
		
		        //最下面是一些基本设置
		        treeView.isShowRoot = false //这里表示是否显示根节点,我这里设置不显示根节点
		        treeView.scrollTo(13)//如果面积不够,则滚动到多少
		
		        //这个是右界面的编写
		        rootPane.center = label
		        rootPane.left = treeView
		        stage.scene = Scene(rootPane)
		        stage.width = 1000.0
		        stage.height = 800.0
		        stage.icons.add(Image("${FileToolYt.获取_根源目录()}img/icon.png"))
		        stage.show()
		    }
		
		    fun bgImage(label: Pane, src: String, stage: Stage) {
		        label.background =
		            Background(
		                BackgroundImage(
		                    Image(src, stage.width * 0.7, stage.height, true, true),
		                    BackgroundRepeat.NO_REPEAT,
		                    BackgroundRepeat.NO_REPEAT,
		                    null,
		                    null
		                )
		            )
		    }
		    fun navigation(){
		        for (file in fileList) {
		            val item = TreeItem(file.name)
		            treeImage.children.add(item)
		        }
		        val itemJ = TreeItem("计算机")
		        val itemT = TreeItem("坦克")
		        treeRoot.children.addAll(treeImage,itemJ,itemT)
		    }
		}
		```
		
- javafx组件的一些基本操作
	```Kotlin
	isMouseTransparent //设置鼠标无法操作该组件
	textFill//设置组件字体颜色
	-fx-opacity: 0.4;//设置组件透明,最好不要用style属性,这个会覆盖之前设置的属性
	 children.opacity = 0.6 //设置透明度
	
	```
	



