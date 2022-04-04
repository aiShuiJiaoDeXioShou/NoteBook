# HTML+CSS基础

## 基础前端样式

### 边框

1. 边框的基本样式

### 高级定位

```css
position: relative;//这个是保持原地位不变
position: absolute;//这个是作用于子类定位的相对定位
position: fixed;//这个是固定定位
```

## 高级前端样式

### 1.盒子阴影

`box-shadow` :

1. 基本用法 `box-shadow: h-shadow v-shadow blur spread color inset;`
2. ![image-20211117160319638](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211117160319638.png)

# JS

## 前言:(学习JavaScript我们需要准备什么?)

### 1.一个浏览器:

+ 在这里我推荐用windows自带的浏览器edge~，因为edge浏览器基于谷歌内核可以做到和谷歌一样的开发环境，支持中文，上网方便，谷歌太麻烦了:
+ 打开浏览器界面,我们可以看到这样:

  > <img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210930151536153.png" alt="image-20210930151536153" style="zoom: 50%;" />
  >
+ 按住F12键位

  > 注意笔记本电脑要点击右下角的 `<font color='red'>`fn `</font>`键位
  >
  > <img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210930151750549.png" alt="image-20210930151750549" style="zoom: 50%;" />
  >

### 2.代码编辑器:

1. 前端的代码开发工具比后端多多了:

   + 知名的有-"宇宙第一编辑器","超级IDE"--***VSCode***:
2. 我个人推荐用idea来开发前端 :

因为idea很酷，他能真正都懂你的代码

### 3.综合开发工具:

### 4.文档编辑器:

## 1.JavaScript基本语法

1. 第一个程序helloword
2. 在一般的项目开发中，我们都不这样用js，我们会给一个特定的文件夹，然后使用script标签将其引入

   在同一个标签下直接用文件名,不在同一个目录需要使用***../***

   ```JavaScript
   <script src="Untitled-1.js"></script>
   ```
3. 变量的使用方式:全局变量用var,局部变量用let

关于function函数等等问题

1. 函数如果在页面调用的话，后面是不能带src值的，不然JavaScript会出现语法错误，从而导致不能调出函数
2. 在js文件中定义的函数，或者对象，是不能由其他的js文件调用的，说白了js就是函数式语言，没事就写在一个地方别老想着调用函数。
3. 通过script标签引入js文件，相当于直接把两个js文件放在了一起

   ```JavaScript
   	<script src="js/jquery-1.12.4.js"></script>
       <script src="js/杨腾.js"></script>
   ```
4. HelloWord(经典写法)

   ```JavaScript
   document.write("Hello 杨腾!")
   //还可以这样:
   alert("Hello 杨腾!)
   //甚至输出到控制台:
   console.log("Hello 杨腾!")
   ```

+ 输出语句

```JavaScript
//弹窗var str = prompt("","");返回值为str
		console.log('杨腾是猪');
		document.write('杨腾是猪');
		alert('杨腾是猪');
```

+ 基本数据类型的转换

```JavaScript
		var sum=Number(a)+Number(b);
		sum.toString();
```

+ 获取div的宽高

```javaS
		var w = box.offsetWidth;
		var h = box.offsetHeight;
```

+ 获取页面对象

```javaS
		var button1 = document.getElementById('button-id1');
		var button2 = document.getElementById('button-id2');
```

+ 改变页面对象的值

```JavaScript
		box.style.width = x+"px";
		box.style.height = y+"px";
```

+ 去掉多余汉字

```JavaScript
document.write(parseInt('123汉字'));
```

+ 对数组进行升序和降序

```JavaScript
var arr = [5,3,6,8,1];
        function up(a,b){
            return a-b;
        }
        function dom(a,b){
            return b-a;
        }
        arr.sort(up);
        document.write(arr.join('')+'</br>');
        document.write(arr.sort(dom).join(''));
```

+ 对数组进行删除

```JavaScript
var ary = [1,2,3,4]; 
ary.splice(0,1);
或 ary.splice($.inArray(2, ary), 1); 其中$.inArray(2, ary)用来查找某元素在数组中的索引位置。

var ary = [1,2,3,4]; 
ary.splice(0,ary.length);//清空数组 
console.log(ary); // 输出 []，空数组，即被清空了

```

+ 在数组开头添加元素

![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/0a0b2e02ebe4fb6214a2c4d2f046c489.png)

+ 在数组结尾添加元素：push()

![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/8eeb8f86625c83625dc02268a9593794.png)

+ **删除数组最后一个元素：pop()**

![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/237b01aabf4cce37c236c18da260b943.png)

+ 数组颠倒顺序

![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/cfd95554840fcfc264655647633a8a1d.png)

+ 数组连接，这里指的是打印的连接

![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/32c5be3daf19cdbd68bb04e1a0f2e853.png)

+ 数组和字符串的统计

```JavaScript
        var str = 'apple,orange,peach,banana';
        var  strArray =str.split(',');
        document.write("</br>"+strArray.join('-'));
        var str2 ='America,Greece,Britain,Canada,China,Egypt';
		//操作字符串的限定符号
        var strArray2 = str2.split(',');
        var x=0;
        for (var i = 0; i < strArray2.length; i++){
            if(strArray2[i].indexOf('a')!=-1||strArray2[i].indexOf('A')!=-1){
                x++;
            }
        }
        document.write
        ('</br>在以下字符中：'+'</br>'+strArray2.join('-')+'</br>'+'共有包含a或A：'+x);
```

+ 在网页中直接调用JavaScript代码，只需要加一个JavaScript就行了

```JavaScript
<a href="javascript:location.href='flower.html'">查看鲜花详情</a>  
<a href="javascript:location.reload()">刷新本页</a>
```

+ 工厂模式创造对象

```JavaScript
function User(name, age, describe, education) {
	this.name = name;
	this.age = age;
	this.describe = describe;
	this.education = education;
	this.say = function() {
		alert("我及时天")
	}
}
var user = new User('yangteng', 16, '大专', '很穷');
user.say();
alert(user.age);
```

### 1.字符串操作

```JavaScript
var arr = [5,3,6,8,1];
        function up(a,b){
            return a-b;
        }
        function dom(a,b){
            return b-a;
        }
        arr.sort(up);
        document.write(arr.join(' ')+'</br>');
        document.write(arr.sort(dom).join(' '));
        var str = 'apple,orange,peach,banana';
        var  strArray =str.split(',');
        document.write("</br>"+strArray.join('-'));
        var str2 ='America,Greece,Britain,Canada,China,Egypt';
        var strArray2 = str2.split(',');
        var x=0;
        for (var i = 0; i < strArray2.length; i++){
            if(strArray2[i].indexOf('a')!=-1||strArray2[i].indexOf('A')!=-1){
                x++;
            }
        }
        document.write('</br>在以下字符中：'+'</br>'+strArray2.join('-')+'</br>'+'共有包含a或A：'+x);
        //求一到一百的和
        function getSum(){
            var sum=0;
            for (var i = 1; i <= 100; i++){
                sum=i+sum;
            }
            return sum;
        }
        alert(getSum());
        var array = [1,"杨腾","19岁","皇家达机电","带专"]
        array[1]
        array[5]="奥特曼"
  
        alert(array[5])
```

### 2. 数组

**参考w3school文档**：[JavaScript 数组参考手册 (w3school.com.cn)](https://www.w3school.com.cn/jsref/jsref_obj_array.asp)

| 方法名称                                   | 约定参数                        | 具体使用                                           |
| ------------------------------------------ | ------------------------------- | -------------------------------------------------- |
| array.copyWithin(target, start, end)       | target start  end               | target指复制到的指定位置，start指开始位置，end结尾 |
| array1.concat(array2, array3, ..., arrayX) | *array2, array3, ..., arrayX* | 必需。要连接的数组。                               |
|                                            |                                 |                                                    |

#### 2.1.过滤器filter

**语法**：

对指定元素进行过滤，返回过滤之后的数组：

```js
array.filter(function(currentValue,index,arr), thisValue)
```

| 参数          | 描述                                                                                                             |
| ------------- | ---------------------------------------------------------------------------------------------------------------- |
| currentValue  | 必须填的参数，当前选项的值                                                                                       |
| index         | 可选。当前元素的索引值                                                                                           |
| *arr*       | 可选。当前元素属于的数组对象                                                                                     |
| *thisValue* | 可选。对象作为该执行回调时使用，传递给函数，用作 "this" 的值。``如果省略了 thisValue ，"this" 的值为 "undefined" |

案例：

```js
this.showList = this.showList.filter(res=>{
   return res.checked //返回的是布尔值,数组每一个选项执行一次过滤,通过返回bool值来进行排除
})
```

#### 2.2.splice工具函数

这个函数极为强大,能对元素进行增删改查,**但是有一个很大的坑,似乎在循环里,它不能正常使用**

语法:

```js
array.splice(index, howmany, item1, ....., itemX)
```

参数列表:

| 参数                  | 描述                                                                        |
| --------------------- | --------------------------------------------------------------------------- |
| *index*             | 必需。整数，指定在什么位置添加/删除项目，使用负值指定从数组末尾开始的位置。 |
| *howmany*           | 可选。要删除的项目数。如果设置为 0，则不会删除任何项目。                    |
| *item1, ..., itemX* | 可选。要添加到数组中的新项目。                                              |

例子：

```js
//删除两个项目:
var fruits = ["Banana", "Orange", "Apple", "Mango", "Kiwi"];
fruits.splice(2, 2);
```

```js
//添加一个新项目,并且删除1 个项目：
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.splice(2, 1, "Lemon", "Kiwi");
```

#### findIndex判断是否存在函数

语法:

```js
let tagIndex( = 数组.findIndex(res=>{
    return res == 值
})
```

## 2.BOM对象

![image-20210902103401613](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210902103401613.png)

+ 设置网页刷新

![image-20210902103545991](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210902103545991.png)

+ 用于用户访问过的url

![image-20210902103628862](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210902103628862.png)

+ 对窗口事件操作

![image-20210902103901623](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210902103901623.png)

![image-20210902103924217](C:\Users\有天道\AppData\Roaming\Typora\typora-user-images\image-20210902103924217.png)

## 3.DOM对象

![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/d4a8f42e8d3d6bcf761f1b5272445f80.png)

1. 给一个HTML元素设置一个整体样式

   ![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/b67b16d84d10d6efe76cc1048685f21a.png)

## 4.js里面的正则表达式

### 1.常用方法，js内置了正则对象

**表述:**在js里面 `/\w{10}/`两个 `/正则表达式/`,这样就等于一个正则对象,比如:`<font color='red'>let patt = /\w{10}/``</font>`,

下面是一些范例:

```JavaScript
        //这个表示匹配任意数字或者字符串，必须要十个
        let patt = /\w{10}/;
        //这个表示匹配任意数字或者字符串，十个或者十个以上
        let patt2 = /\w{10}/;
        let a = patt.test("2002111111");
        console.log(a);
        //首个输入必须为字母，大写或者小写都无所谓
        let patt3 = /[a-z A-Z]\w{1}/
        console.log(patt3.test("Qq"))
```

2.基本操作

+ 获取样式

```javascript
//元素节点.style.元素名
```

+ 为HTML赋值
+ 增删改查

```javascript
<!--
 * @Author: 杨腾
 * @Date: 2021-09-08 08:12:30
 * @LastEditTime: 2021-09-08 08:52:37
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \JavaScript学习\No3_HTML\9_8对节点进行增删操作.html
-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>对节点的增删练习</title>
</head>
<body>
    <div class="node">
        <button id='we'>wergg</button>
    </div>
    <button id="bt1">删除</button>
    <script>
         var node = document.getElementsByClassName('node')[0];
        //一次性添加一组节点
        var strs = ['北京','上海','天津','兰州','长沙','西安'];
        for (const key in strs) {
            if (Object.hasOwnProperty.call(strs, key)) {
                const element = strs[key];
                //创造对应节点进行添加
                var sonNode = document.createElement('button');
                var str = document.createTextNode(element);
                sonNode.appendChild(str);
                node.appendChild(sonNode);
            }
        }

        //删除元素
        var bt1 = document.getElementById('bt1');
        var we = document.getElementById('we');
        bt1.onclick = function(){
            node.removeChild(we);
        }
  
        //用按钮的方式添加一个元素
        var bt2 = document.getElementById('bt2');
        //需要添加的元素
        var index = 0;
        var names = ['杨腾','蔡雨豪','奥特曼','迪迦']
        bt2.onclick = function(){
            var butx = document.createElement('button');
            var name = document.createTextNode(names[index]);
            butx.appendChild(name);
            node.appendChild(butx);
            index++;
            if(index >= names.length){
                index = 0;
            }
        }
        //获取节点parent是父的意思,这是个属性，注意不是方法
        var weParent = we.parentNode;
        var fistNode = weParent.firstChild;//最后一个元素
        var listNode = weParent.lastChild;//第一个元素
        var nextNode = listNode.nextSibling;//下一个节点
        var shanNode = listNode.previousSibling;//上一个节点 node.removeChild(we);
        }
    </script>
</body>
</html>
```

![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/231947e3760414eb92cf50a493bf8802.png)

![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/6cbf1494babade79ee2d9863155ad31b.png)

插入指定HTML内容：

![img](https://p.ananas.chaoxing.com/star3/origin/baa91307952a9bf84f6750e7ccbd28c7.png)

![img](https://p.ananas.chaoxing.com/star3/origin/14aef20800521f76a9154b70f442b9e5.png)

![img](https://p.ananas.chaoxing.com/star3/origin/143204e114906ad978d29a4f8b707158.png)

`<font color='red'>`千万不要用nextSibing和previousSibling方法，我人傻了，用Element那个 `</font>`

![img](https://p.ananas.chaoxing.com/star3/origin/ba44d7d1bc0feb05a3cbcff8ec5b174d.png)

![img](https://p.ananas.chaoxing.com/star3/origin/01feba49c4f6b11afd8d8c3174affcf2.png)

**3. querySelector()和querySelectorAll()**

![img](https://p.ananas.chaoxing.com/star3/origin/7ad5ebff87a499d3a5216749813ea8ef.png)

+ querySelector()表示选取满足选择条件的第1个元素，querySelectorAll()表示选取满足条件的所有元素。这两个方法都是非常简单的，它们的写法跟CSS选择器的写法是完全一样的。

![img](https://p.ananas.chaoxing.com/star3/origin/94e17df8f2e01f0ab1964d32f341b690.png)

![img](https://p.ananas.chaoxing.com/star3/origin/f37f3530931bc1298238c77f9e9914a1.png)

+ ⭐querySelectorAll()方法得到的是一个类数组，即使你获取的只有一个元素，也必须使用下标[0]才可以正确获取。
+ `<font color='red'>`通过这些属性nodeName：节点名称  nodeValue：节点值 nodeType：节点类型，能对节点属性进行一系列的操作。`</font>`

# JQ

## 1.获取对象注意的地方：

+ 我们获取单个JQ元素使用(`<font color='red'>`这是JQ元素，我们不能使用HTML方法 `</font>`)：

  ```javascript
          $(function () {
              alert("杨腾吃屎");
              $('p').click(function () {
                  $(this).hide();
              });
              $('button').eq(0).click(function (){
                  $('p').hide();
              });
              $('button').eq(1).click(function (){
                  $('p').show();
              });
               $('button').get(2).onclick=function (){
                  $('p').show();
              };
          })
  ```
+ 我们获取单个HTML元素：

  ```javascript
   $('button').get(2).onclick=function (){
                  $('p').show();
              };
  ```

## 2.选择器的语法：

**前言：**（这里是指$符号里面的选择器语法，如果需要实际方法--详见6）

+ 参见表格与代码:

```javascript
//同辈元素选折器,选择第一个元素之后同辈的
$('h1~p').css('color','red');
//父类选择器，父类容器所有的后代
$('.price>*').css('color','red');
//并集选择器,选择所有div和p的元素
$('div,p').css('color','red');

```

![img](https://raw.githubusercontent.com/aiShuiJiaoDeXioShou/ynagtengpjo/main/imge4a31e5a1d3c03d14b9ad9e76b52334a.png)

![img](https://raw.githubusercontent.com/aiShuiJiaoDeXioShou/ynagtengpjo/main/img7f9f3c3debee56ca1a9f48075ecd2b13.png)

```JavaScript
//创建了新的元素 
var  p=$("<p> <b>List  Item0</b> </p>")
 
//增加子元素   ---现有元素之后 
$("#div1").append(p); 

//把p元素增加到  div里面  
p.appendTo("#div1"); 

//添加内部的子元素  ---现有元素之前 
$("#div1").prepend(p); 
p.prependTo("#div1"); 

//平级的添加元素---现有元素之前 
p.insertBefore("#div1"); 
$("#div1").before(p); 

//平级的添加元素---现有元素之后 
p.insertAfter("#div1"); 
$("#div1").after(p)
```

![img](https://raw.githubusercontent.com/aiShuiJiaoDeXioShou/ynagtengpjo/main/img4f2f66d175a213992d1c93490ffbc2a6.png)

+ ***JQuery基本过滤器***

  ```javascript
      <script type="text/javascript">
          //.contain类下选取标题
          $(".contain :header").css();
          //.contain类下选取最后一个元素
          $(".contain :last").css();
          //.contain类下选取第一个元素
          $(".contain :first").css();
          // .contain类下选择从零开始的所有偶数
          $(".contain :even").css();
          // .contain类下选择从零开始的所有奇数
          $(".contain :odd").css();
      </script>
  ```

![img](https://raw.githubusercontent.com/aiShuiJiaoDeXioShou/ynagtengpjo/main/img61a8b13493a500c4916b021d5901ff50.png)	![img](https://raw.githubusercontent.com/aiShuiJiaoDeXioShou/ynagtengpjo/main/img4793d76ef812e46070b062e4258b45b0.png)

## 3.操控元素，对元素的增删改查

+ 使用JQ获取一个JQ数组里面的当个单个对象

```javascript
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
"http://www.w3.org/TR/html4/loose.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>获得集合的某一项</title>
        <script type="text/javascript" src="jquery-core/jquery-1.8.0.js"></script>
         <script type="text/javascript">
   
           $(document).ready(function(){
           alert("jquery使用eq函数获得集合中的某一项："+$("p").eq(0).html()+
           "\njs使用索引获得集合中的某一项："+document.getElementsByTagName("p")[1].innerHTML+
           "\njquery对象转换成DOM对象使用get函数获得集合中的某一项："+$("p").get(2).innerHTML
           );
           });
         </script>
    </head>
    <body>
   
     <p>这是p1</p>
     <p>这是p2</p>
     <p>这是p3</p>
   
    </body>
</html>
```

+ 隐藏选定的某一个内容，其中this代表当前对象*hide()* 方法表示隐藏元素

```javascript
$('p').click(function (){
                $(this).hide();
            })
```

+ 使用JQ直接给对象添加css元素

```javascript
 $('.fulei').css({"background":"#000"});
// 方式二添加class属性
$('#yt2').addClass('class-1')
//移除class属性
$('#yt2').removeClass('class-1')
```

+ 增加:添加的方法有: ``<font color='#c9d8cd'>`append()```</font>`*在后面添加一个元素,*````<font color='#c9d8cd'>``prepend()``</font>``*在前面添加一个元素

```javascript
			//添加一个元素
            $('.div1').eq(0).append("<p>杨腾吃屎</p>");//添加到末尾
            $('.div1').prepend("<p>杨腾不吃屎了</p>");//添加到开头
            //在指定元素后面或者前面添加一个元素
            $('p').eq(0).before("<p>我是前面的元素</p>");
            //jQuery after() 和 before() 方法
            $('p').eq(0).after('<p>我是后面的元素</p>');
```

+ 添加一个代码块

  ```javascript
   //添加多个元素
              function appendText()
              {
                  var txt1="<p>Text.</p>";               // 以 HTML 创建新元素
                  var txt2=$("<p></p>").text("Text.");   // 以 jQuery 创建新元素
                  var txt3=document.createElement("p");  // 以 DOM 创建新元素
                  txt3.innerHTML="Text.";
                  $("p").append(txt1,txt2,txt3);         // 追加新元素
              }
  ```
+ 在指定位置添加一个元素

```javascript
            //在指定元素后面或者前面添加一个元素
$('p').eq(0).before("<p>我是前面的元素</p>");
//jQuery after() 和 before() 方法
$('p').eq(0).after('<p>我是后面的元素</p>');
```

+ 替换一个节点

  ```javascript
  		//替换
  		$("#button3").click(()=>{
  			$(".gameList li:eq(0)").replaceWith("<li>神明已经将临！</li>")
  		})
  ```
+ 删除一个元素, **detach():** 不会彻底删除元素,还保留事件

```javascript
            //删除一个元素
$('#shanchu').click(function () {
    $('p').eq(0).remove();
});

```

+ 复制一个元素,在末尾添加它

  ```javascript
  	//复制节点,clone(false)这里面是一个布尔值，true表示复制一切，false只复制文本
  		$(".gameList li:eq(3)").click(()=>{
  			$(this).clone(false).appendTo(".gameList")
  		})
  		$(".gameList li:eq(3)").click(()=>{
  			$(this).clone(true).appendTo(".gameList")
  		})
  ```
+ 添加css属性
  添加class属性有两种方式，一种是利用attr属性为元素添加一个class属性，第二种是利用 `addClass `属性添加元素，删除元素用 `removeClass`属性

  ```JavaScript
  $('#yt2').attr("class","class-1")//添加一个class
  ```

  `<img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/b4f06e23ff44a8023cffdbcfa8aa28f3.png" alt="img" style="zoom:50%;" />`

  ![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/7d6dd53eadca25273dab0e2c6482c958.png)

```javascript
$(function () {
    $('.imgLeft,dl>dt').click(function () {
        $('dd').toggle();
    })
    $('h1').css('font-weight', 'bold');
    $('.intro').css('color', 'red');
    $('dl>*').css('color', 'red');
    $('dd>span').addClass('x');
    $('#ticket>span').addClass('x');
    //添加几种属性
    $("#jdPrice>span").css({'color': 'red', 'font-size': '30px'});
    $("#author").css('font-weight', 'bold');
    $('#jdPrice>p').css('color', '#d4d4d4');
    $('#jdPrice>p>span').addClass('x2');
    $('#jdPrice').css('font-weight', 'bold');
    $('#mobilePrice').css('font-weight', 'bold');
})
```

## 4.鼠标的事件

**w3cschool地址：**[jQuery 参考手册 - 事件 (w3school.com.cn)](https://www.w3school.com.cn/jquery/jquery_ref_events.asp)

![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/0cd0582efd049e474f6114cfbc1510fb.png)

![image-20210926233243825](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210926233243825.png)

#### （1）添加鼠标事件

```JavaScript
 			//添加单条鼠标事件
			$(".red").click(function () {
                $(".red").animate({"background-color": "#7b8c7c", "width": "100px", "height": "100px"})
            })
			//添加多条鼠标事件
			$("div").on({
                "click":function(){
                    alert("杨腾不是人")
                },"mouseover":function(){
                    alert("杨腾是猪")
                }
            })
```

#### （2）删除鼠标事件：

```JavaScript
$(".comment").unbind()
```

```

```

[undelegate()](https://www.w3school.com.cn/jquery/event_undelegate.asp)：这个方法使得元素无法添加事件

## 5.JQ的创建元素对象与获取网页当中的文本元素

1. 创建元素对象：

   ```JavaScript
    var a = $("<a></a>")
   ```

   这一行代码相当于创建了a元素对象，在JQ中创建元素对象，只需要直接将文本输入进去就行了。
2. 三个方法：

   ```text
   内容操作，指的是使用jQuery来操作一个元素的文本内容、值内容等。在jQuery中，对于内容操作，我们有以下3种方法。

   （1）html()

   （2）text()

   （3）val()

   其中，html()和text()这两个方法用于操作一般元素，而val()方法用于操作表单元素
   ```
3. 具体用法

   ![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/32039572402804f82211f498f009dac7.png)

   + 使用元素**.html()**获取所有内部元素以及文本
   + 使用元素**.text()**获取文本元素
   + 使用元素**.val()**获取表单中的值

## 6. JQ里面的集合（选择器的方法版本）

### 一.遍历子元素

在jQuery中，如果想要查找当前元素的后代元素（子元素、孙元素等），我们有以下3种方法：

- **children()**:在jQuery中，我们可以使用children()方法来查找当前元素的“子元素”。注意，children()方法只能查找子元素，不能查找其他后代元素。

  **selector**是一个可选参数，它是一个选择器，用来查找符合条件的子元素。当参数省略，表示选择所有子元素；当参数不省略时，表示选择符合条件的子元素。

  ![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/f2761041db62cffb94bd9d7985dffe3f.png)
- **（2）find()**

  在jQuery中，我们可以使用find()方法来查找当前元素的“后代元素”。注意，find()方法不仅能查找子元素，还能查找其他后代元素。

  ![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/e001efa490410451ce2b304fbcd1773b.png)
- **contents()**:

  在jQuery中，我们可以使用contents()方法来获取子元素及其内部文本。contents()方法和children()方法相似，不同的是，contents()
  返回的jQuery对象中不仅包含子元素，还包含文本内容。而children()方法返回的jQuery对象中只会包含子元素，不包含文本内容。

  在实际开发中，我们极少会用到contents()方法，因此小伙伴们不需要深入了解，这里简单认识一下即可。

  ![img](https://p.ananas.chaoxing.com/star3/origin/0ca114eeb53efe0ce9731c10adbfc629.png)
- ![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/0ca114eeb53efe0ce9731c10adbfc629.png)

### 二、遍历同辈元素

**（1）向后查找兄弟元素：****next()、nextAll()、nextUntil()**

next()方法：$().next()  来查找某个元素的后一个“相邻”的兄弟元素。大多数情况下，next()方法是不需要参数的。

nextAll()方法：$().nextAll(selector)来查找某个元素后面“所有”兄弟元素。注意，next()只会查找后面相邻的兄弟元素，而nextAll()则会查找后面所有的兄弟元素。

nextUntil()方法：$().nextUntil(selector) 是nextAll()方法的一个补充，它可以查找元素后面“指定范围”的所有兄弟元素，相当于在nextAll()方法返回的集合中截取一部分。

**（2）向前查找兄弟元素：prev()、prevAll()、prevUntil()**

**prev()**方法：$().prev()来查找某个元素的前一个“相邻”的兄弟元素。大多数情况下，prev()方法是不需要参数的。

**prevAll()**方法：$().prevAll(selector)来查找某个元素前面“所有”兄弟元素。注意，prev()只会查找前面相邻的兄弟元素，而prevAll()则会查找前面所有的兄弟元素。

**prevUntil()**方法：$().prevUntil(selector)是prevAll()方法的一个补充，它可以查找元素前面“指定范围”的所有兄弟元素，相当于在prevAll()方法返回的集合中截取一部分。

![img](https://p.ananas.chaoxing.com/star3/origin/546f50eee232a2a6478ec2c78c94f2cc.png)

**（3）前后查找兄弟元素：siblings()**

jQuery提供另外一种不分前后的siblings()方法：$().siblings(selector)
是一个可选参数，它是一个选择器，用来查找符合条件的兄弟元素。当参数省略，表示选择所有兄弟元素；当参数不省略时，表示选择满足条件的兄弟元素。

### 三、遍历前辈元素

在jQuery中，如果想要查找当前元素的祖先元素（父元素、爷元素等），我们有以下3种方法。

- **（1）parent()**
- **（2）parents()**
- **（3）parentsUntil()**

#### 一、parent()

使用parent()方法来查找当前元素的“父元素”。注意，元素只有一个父元素。

![img](https://p.ananas.chaoxing.com/star3/origin/8fac9df45e63ce121f58dd4e871abf5c.png)

selector是一个可选参数，它是一个选择器，用来查找符合条件的父元素。当参数省略，表示父元素不需要满足任何条件；当参数不省略时，表示父元素需要满足条件。

#### 二、parents()

在jQuery中，我们可以使用parents()方法来查找当前元素的“祖先元素”。注意，元素可以有多个祖先元素

parent()和parents()这两个方法很好区分。其中，parent()是单数，因此查找的元素只有一个，那就是父元素。parents()是复数，因此查找的元素有多个，那就是所有的祖先元素（包括父元素、爷元素等）。

![img](https://p.ananas.chaoxing.com/star3/origin/f2387f87892b406933f3f6a20b3c0bff.png)

selector是一个可选参数，它是一个选择器，用来查找符合条件的祖先元素。当参数省略，表示祖先元素不需要满足任何条件；当参数不省略时，表示祖先元素需要满足条件。

#### 三、parentsUntil()

在jQuery中，parentsUntil()方法是parents()方法的一个补充，它可以查找“指定范围”的所有祖先元素，相当于在parents()方法返回的集合中截取一部分。

![img](https://p.ananas.chaoxing.com/star3/origin/bc2baaca292ecafd816f58afecd6d582.png)

在实际开发中，我们一般只会用到parent()方法和parents()这两个，极少用到parentsUntil()。因此对于parentsUntil()方法，我们了解一下就行。

![img](https://p.ananas.chaoxing.com/star3/origin/c39996ac4e26b5198efd8b3296441982.png)

### 四、遍历元素

在操作DOM时，很多时候我们需要对“同一类型”的所有元素进行相同的操作。如果使用JavaScript来实现，我们往往都是先获取元素的长度，然后使用循环来访问每一个元素，代码量比较大。

在jQuery中，我们可以使用each()方法轻松实现元素的遍历操作。

![img](https://p.ananas.chaoxing.com/star3/origin/77e7c33c0c2b3f9a01f869e5a3bb6b03.png)

each()方法接收一个匿名函数作为参数，该函数有两个参数：index，element。

index是一个可选参数，它表示元素的索引号（即下标）。通过形参index以及配合this关键字，我们就可以轻松操作每一个元素。此外注意一点，形参index是从0开始的。

element是一个可选参数，它表示当前元素，可以使用(this)代替。也就是说，(element)等价于$(this)。

如果需要退出each循环，可以在回调函数中返回false，也就是return false即可。

![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/e69c77790ba529b85f790bd8ea50a02d.png)

![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/e7ac24c4d0fbe9bb70c1013dd0a10f27.png)

each()方法的参数是一个匿名函数：function(index, element)
{}。没错，函数实际上也可以当做参数。对于这种形式，一开始很多新手没法理解，不过等我们慢慢深入原生JavaScript就会熟悉了，这里暂时只需要“套用”就行。

![img](https://p.ananas.chaoxing.com/star3/origin/c0b95e140f8372b6355d0f432d0fd54e.png)

⭐也就是说，对于each()方法中的回调函数，如果你想省略第二个参数，可以在内部使用$(this)代替。对于这两种等价代码，我们在实际开发中经常会碰到，大家一定要记住。

![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/a5e5d41cf8cf339c78c07a493f6ae274.png)

### JQ事件

#### 1.基本事件：

##### 1.鼠标事件

```javascript
//鼠标事件
$(()=>{
	$(".nav-ul li a").mouseover(function(){
		$(this).css("background-color","blue")
	})
	$(".nav-ul li a").mouseout(function(){
		$(this).css("background-color","red")
	})
})
```

##### 2.跟方便的合成事件，hover()方法：$().hover(fn1, fn2)

参数fn1表示鼠标移入事件触发的处理函数，参数fn2表示鼠标移出事件触发的处理函数。

在hover()方法中，说白了就是插入两个function(){}，很简单。每次在使用hover()方法时，我们先把形式写出来，如下：![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/40755956808431bdca2caca9c039d7d1.png)

再去编写两个function(){}中的内容，这样就不会导致书写错误了：

![img](https://p.ananas.chaoxing.com/star3/origin/74735e66ec0923fb709a9122d511e3c5.png)

⭐hover()方法，准确来说是替代了mouseenter()和mouseleave()，而不是替代mouseover()和mouseout()。

![img](https://p.ananas.chaoxing.com/star3/origin/0985c92865bbe5e6d49382c870c3ff11.png)

#### 2.添加多个事件，与解绑事件

```JavaScript
	$(".menu-btn").on({
		mouseover:()=>{

		$(".topDown").show();
		},
		mouseout:()=>{
			$(".topDown").hide();
		}

	})
```

使用off解绑事件

```JavaScript
	$(".menu-btn").on({
		"mouseover",()=>{
			$(".menu-btn").off("mouseover")
		}
	})
```

## 7. JQ动漫

### JQuery动画效果

平常在浏览网页时，我们经常可以看到各种炫丽的动画效果，例如下拉菜单、图片轮播、浮动广告等。使用动画效果可以让页面更加酷炫，也可以优化页面的用户体验。

![img](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg-blog.csdnimg.cn%2F20190121100852119.gif&refer=http%3A%2F%2Fimg-blog.csdnimg.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1631764437&t=2f69887de8de5f2e432d0d840ed6cca6)

![img](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fhiphotos.baidu.com%2Ffeed%2Fpic%2Fitem%2Fa71ea8d3fd1f413467da89d12e1f95cad0c85eb4.jpg&refer=http%3A%2F%2Fhiphotos.baidu.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1631764531&t=6c35654488c1e131de8f81553d072123)

![img](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg01.haolizi.net%2F2019%2F04%2F03%2F9b%2F4%2F0%2F9b40125375e4d477692e09e34a328930.gif&refer=http%3A%2F%2Fimg01.haolizi.net&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1631764558&t=8292a02dc7eae86c292c02df9de848dd)![img](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg-blog.csdnimg.cn%2F20210219141258799.gif&refer=http%3A%2F%2Fimg-blog.csdnimg.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1631764677&t=8bc6ade04199150e442903739f489e7c)

JQuery提供了多种动画效果：

**（1）显示与隐藏**

**（2）淡入与淡出**

**（3）滑上与滑下**

**（4）自定义动画**

### **显示与隐藏**

在jQuery中，如果想要实现元素的显示与隐藏，有以下2种方式。

- **（1）show()和hide()**
- **（2）toggle()**

### 一、show()和hide()

在jQuery中，我们可以使用show()方法来显示元素，也可以使用hide()方法来隐藏元素。一般情况下，show()和hide()这两个方法都是配合一起使用的。

![img](https://p.ananas.chaoxing.com/star3/origin/e2f60ff511bd12f1405caa6ef164e3a8.png)

show()方法会把元素由display: none;还原为原来的状态（display:block、display:inline-block等）。

hide()方法会为元素定义display:none;。

speed是一个可选参数，表示动画的速度，单位为毫秒。如果省略，则表示没有动画效果。speed有两种取值：一种是“字符串”；另外一种是“数值”，如下表所示。

![img](https://p.ananas.chaoxing.com/star3/origin/5a1a81de6d21f3dba777e4338abdf414.png)

fn也是一个可选参数，表示动画执行完成后的回调函数。在这里，所谓的回调函数，说白了就是在动画执行完成后执行的一个函数。

**show()和hide()不带参数就是无动画的。**

### 二、toggle()

见【复合事件】知识选项卡末尾处

**
**

### **淡入与淡出**

在jQuery中，如果想要实现元素的淡入与淡出的渐变效果，有以下3种方式。

- **（1）fadeIn()和fadeOut()**
- **（2）fadeToggle()**
- **（3）fadeTo()**

### 一、fadeIn()和fadeOut()

在jQuery中，我们可以使用fadeIn()方法来实现元素的淡入效果，可以使用fadeOut()方法来实现元素的淡出效果。一般情况下，fadeIn()和fadeOut()这两个方法都是配合一起使用的。

![img](https://p.ananas.chaoxing.com/star3/origin/9913f152e0f9f97ecf3c983f8db14b83.png)

**![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/6acdec9a499008878140cae2f711360c.png)
**

**演示：**

**淡入淡出效果跟带动画的显示隐藏效果的区别：**

show()与hide()：通过改变height、width、opacity、display来实现元素的显示与隐藏。

fadeIn()与fadeOut()：通过改变opacity、display来实现元素的显示与隐藏。

hide()方法是慢慢缩小来隐藏元素，而fadeOut()是整体淡化直至消失。

### 二、fadeToggle()

在jQuery中，我们还可以使用fadeToggle()方法来“切换”元素的显示状态。也就是说，如果元素是显示状态，则会淡出；如果元素是隐藏状态，则会淡入。

**语法：$().fadeToggle(speed, fn)**

**![img](https://p.ananas.chaoxing.com/star3/origin/5a3a1a63e32c93c480a3de36330f3a23.png)
**

使用fadeToggle()方法来切换元素的显示状态，比fadeIn()和fadeOut()这两个方法更加简单方便。

### 三、fadeTo()

在淡入效果中，透明度（opacity属性）是从0变化到1。在淡出效果中，透明度是从1变化到0的。在jQuery中，如果想要将元素透明度指定到0~1之间的某个值，可以使用fadeTo()方法。

**语法：$().fadeTo(speed, opacity, fn)**

speed是一个可选参数，表示动画的速度，单位为毫秒，默认为400毫秒。如果省略，则表示采用默认速度。speed有两种取值：一种是“字符串”；另外一种是“数值”

opacity是一个必选参数，表示元素指定的透明度，取值范围为0.0~1.0。

fn也是一个可选参数，表示动画执行完成后的回调函数。

![img](https://p.ananas.chaoxing.com/star3/origin/751bdca713dc761caf51267f160e7833.png)

⭐fadeTo()方法只会把元素的透明度改变为某个值，并不会隐藏元素。

### 滑上与滑下

在浏览器网页时，我们经常可以看到各种带有滑动效果的下拉菜单。

![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/ed5c39b317c4af43a850a839b491af25.png)

在jQuery中，如果想要实现元素的滑动效果，我们有以下2种方式。

- **（1）slideUp()和slideDown()**
- **（2）slideToggle()**
- 

### 一、slideUp()和slideDown()

在jQuery中，我们可以使用slideUp()方法来实现元素的滑上效果，可以使用slideDown()方法来实现元素的滑下效果。一般情况下，slideUp()和slideDown()这两个方法都是配合一起使用的。

![img](https://p.ananas.chaoxing.com/star3/origin/5613f3da93b5db7dd6ddb66cdbe95a15.png)

![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/921b40785a2ae8d86c5828cb5ac8a18b.png)

### 二、slideToggle()

在jQuery中，我们还可以使用slideToggle()方法来“切换”元素的滑动状态。也就是说，如果元素是滑下状态，则会滑上；如果元素是滑上状态，则会滑下。

**语法：$().slideToggle(speed, fn)**

对于滑动效果，如果使用slideUp()和slideDown()来实现，我们需要定义一个变量来标识滑动状态。如果使用slideToggle()，则不需要多此一举。

### 自定义动画

我们接触了3种动画类型：显示与隐藏、淡入与淡出、滑上和滑下。实际上，我们经常还可以看到其他动画形式，例如一个元素不断移动、一个元素不断扩大等。像这些动画，单纯使用之前那3种动画类型就无法实现了。

**一、简单动画**

对于自定义动画，我们都是使用animate()方法来实现的。

**语法：$().animate(params, speed, fn)**

params是一个必选参数，表示属性值列表，也就是元素在动画中变化的属性列表。

speed是一个可选参数，表示动画的速度，单位为毫秒，默认为400毫秒。如果省略，则表示采用默认速度。

fn也是一个可选参数，表示动画执行完成后的回调函数。

![img](https://p.ananas.chaoxing.com/star3/origin/b0f207136d184a0fcf50b4318a90cc8a.png)

animate()方法的参数params采用的是“键值对”形式，语法如下：

![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/a599c3eeaf457aa187cec6ab5e5f340d.png)

实际上，jQuery本身有一个缺陷，就是使用animate()方法时会无法识别background-color、border-color等颜色属性。因此，我们还需要引入第三方插件jquery.color.js来修复这个bug。

jquery.color.js是依赖jQuery库存在的，因此jquery.color.js文件必须在jquery库文件后面引入，不然就无法生效。实际上，你可以把jquery.color.js看成是一个jQuery插件，这样更好理解。

### 二、累积动画animate

在jQuery中，对于元素的宽度和高度，我们可以结合+=和-=这两个运算符来实现累积动画。

举个例子，{“width”: “+=100px”}表示以元素本身的width为基点加上100px，而{“width”: “-=100px”}表示以元素本身的width为基点减去100px。

`animate({ "width": "+=100px", "height": "+=100px" }, 1000)`使用的是累积动画形式，因此元素最终的width为150px，height为150px。

**
**

**总结**

![img](https://p.ananas.chaoxing.com/star3/origin/21ad43422d868ba80ccb48bb6074be99.png)

## 8. AJAX

### 1.预编译写法``（这样写比字符串拼接方便）

```JavaScript
					var text = `<li>
                                    <div><img src=${random(tuPian,3)}/></div>
                                    <h1>${title}</h1>
                                    <p>
                                       <span>${option}</span>
                                       <span>${ShiJian()}</span>
                                     </p>
                                 </li>`
```

1. 原生ajax请求，读取txt文件

   ```JavaScript
    window.onload = function (){
         //创建阿贾克斯请求对象
         var xmlajax = new XMLHttpRequest()
         //调用请求的方法
         xmlajax.open("GET","http://localhost:8080/demo_war_exploded/AjaxFuwu",true)
         //发送请求
         xmlajax.send();
         //监听状态变化,得判断服务器是否拿到了数据
         xmlajax.onreadystatechange = function (){
           if (xmlajax.readyState == 4 && xmlajax.status == 200){
             alert(xmlajax.responseText)
           }
         }
       }
   ```
2. JQ->AJAX获取后端的数据,get请求和post请求都差不多

   ```javascript
    $(function (){
               $.ajax({
                   type:"get",
                   // url:"http://localhost:8080/demo_war_exploded/AjaxFuwu",
                   url:"读取.txt",
                   data:{"port":"9222"},
                   dateTyle:"json",
                   success:function (obj){
                       alert(obj)
                       $("#hellojava").html(obj)
                   },
                   error:function (msg){
                       alert(msg)
                   }
               })
               return false;
           })  

    $(function (){
         $.get("http://localhost:8080/javaEEWeb_war_exploded/ajaxServlet",function (data){
             alert(data)
         },"text")
       })
   ```

   java代码:

   ```java
   package com.example.javaEEWeb;

   import javax.servlet.*;
   import javax.servlet.http.*;
   import javax.servlet.annotation.*;
   import java.io.IOException;

   @WebServlet(name = "ajaxServlet", value = "/ajaxServlet")
   public class ajaxServlet extends HttpServlet {
       @Override
       protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
           response.getWriter().write("hello java");
       }

       @Override
       protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

       }
   }
   ```
3. 从JSON里面获取一个对象,采用文件的方式:

   ```JavaScript
   function del(danqian){
   				$(danqian).parent().parent().remove()
   			}
   			function dels(danqian){
   				$(danqian).parent().parent().nextAll().remove();
   			}
   			$(function (){
   				$.get("json/goods.json",function (goods){
   					goods.forEach(function (good){
   						var tr = `<tr>
   								<td>${good.proname}</td>
   								<td>${good.price}</td>
   								<td><img style="width:50px;height:50px" src="${good.img}"/></td>
   								<td>${good.type}</td>
   								<td><button id = "del" class="btn btn-danger del" 														onclick="del(this)">删除</button></td>
   							  </tr>`
   							  $("#tb").append(tr)
   					})
   				},"json")
   			})
   ```
4. AJAX的一些方法:

### 2. JQ中AJAX解析JSON数据的方式

#### 1.get（），post（）方法解析数据

+ java代码

```java
        try {
            Map<String, Object> dataMap = new HashMap<>();
            List<String> list = new ArrayList<>();
            list.add("他将君临天下");
            list.add("但是他终于还是失败");
            dataMap.put("title","龙族");
            dataMap.put("list",list);
            String json = gson.toJson(dataMap);
            PrintWriter writer = response.getWriter();
            writer.write(json);
            System.out.println(json);
        } catch (Exception e) {
            e.printStackTrace();
        }
```

+ js代码

```javascript
//热度栏
function heatBarDisplay(){
    const title = $(".heat-introduction h2");//这个是标题
    const p = $(".heat-introduction p");//这个是内容
    //使用ajax请求获取数据
    $.post("http://localhost:8080/caiyuhao2/ShoppingServlet?action=heatBarDisplay",function (datas){
        for (let data in datas){
            alert(datas[data])
        }
    },"json")
}
$(function (){
    //热度栏显示
    heatBarDisplay();
})
```

# vue

## Vue2

### 1. 你好世界

1. vue作为响应式编程，简单来说，就是把原本要你自己写的方法全部封装了，你要采用MVC模式进行调用

   ![image-20210916090641688](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210916090641688.png)
2. 图中记载了两种方式：

   + 一种创建了vue的对象，获取HTML页面中的属性，代码如下：

     ```javascript
     //HTML页面
     <div id="app">
       {{ message }}
     </div>
     //JS页面
     var app = new Vue({
       el: '#app',
       data: {
         message: 'Hello Vue!'
       }
     })
     ```
   + 另一种通过在页面增加vue选择器，直接在data里面操作属性值

     ```javascript
     <div id="app-2">
       <span v-bind:title="message">
         鼠标悬停几秒钟查看此处动态绑定的提示信息！
       </span>
     </div>

     var app2 = new Vue({
       el: '#app-2',
       data: {
         message: '页面加载于 ' + new Date().toLocaleString()
       }
     })

     ```

### 2. 常用api

#### 1. 条件与判断：

```javascript
            // 条件与判断
            var b = new Vue({
                el:'#yt2',
                data: {
                    seen : true,
                    condition : false,
                }
            })
```

```html
    <!-- 条件与判断 -->
    <div id='yt2'>
        <p v-if='seen'>现在你看到我了</p>
        <p v-if="condition">你应该看不到我</p>
    </div>
```

#### 2. 循环

```JavaScript
				// vue的循环语句
				var xunhuan = new Vue({
				  el: '#xunhuan',
				  data: {
					  // 这就相当于一个数组
				    todos: [
				      { text: '学习 JavaScript' },
				      { text: '学习 Vue' },
				      { text: '整个牛项目' }
				    ]
				  }
				})
```

```html
		<!-- vue循环语句-->
		<div id="xunhuan">
			<ol>
				<li v-for="todo in todos">{{todo.text}}</li>
			</ol>
		</div>
```

#### 3.vue当中的响应函数

+ 显示用户输出的响应函数

  ```javascript
                  //使用v-on可以添加事件响应方法
                  var app5 = new Vue({
                      el:"#app-5",
                      data:{
                          text:"fjslfjsl",
                      },
                      methods:{
                          dianji: function () {
                          this.text = this.text.split('').reverse().join('')
                              }
                      }
                  })
                  //显示用户输出
                  var app6 = new Vue({
                      el:"#app-6",
                      data:{
                          text:"sdhfskhfsk"
                      }
                  })
  ```

  ```html
          <div id="app-6">
              <p>{{text}}</p>
              <input v-model="text"/>
          </div>
  ```

5. 创建一个自定义组件

   ```JavaScript
   				// 定义名为 todo-item 的新组件
   				Vue.component('todo-item', {
   				  props: ['todo'],
   				  template: '<li>{{ todo.text }}</li>'
   				})
   				var app7 = new Vue({
   				  el: '#app-7',
   				  data: {
   				    groceryList: [
   				      { id: 0, text: '蔬菜' },
   				      { id: 1, text: '奶酪' },
   				      { id: 2, text: '随便其它什么人吃的东西' }
   				    ]
   				  }
   				})

   ```

   ```html
   		<!-- 自定义组件 -->
   		<div id="app-7">
   		  <ol>
   		    <!--
   		      现在我们为每个 todo-item 提供 todo 对象
   		      todo 对象是变量，即其内容可以是动态的。
   		      我们也需要为每个组件提供一个“key”，稍后再
   		      作详细解释。
   		    -->
   		    <todo-item
   		      v-for="item in groceryList"
   		      v-bind:todo="item"
   		      v-bind:key="item.id"
   		    ></todo-item>
   		  </ol>
   ```

   ```java

   ```

#### 4.单向数据绑定

```js
//指定页面所需值
v-bind:title="name"
```

#### 5.双向数据绑定

```js
//常用于表单输入
v-model:value="xxx"
```

除此之外,v-model还可以操作input-checkbox的数据

```html
<!-- 选中的就要加checked这个东东 -->
<input class="toggle" type="checkbox" :value="item.id" @click="selectOne(index)"
v-model="!item.checked">
```

当 `v-model=true`的时候,checkbox显示为选中状态,反之则为不选中状态

#### 6.几种灵活使用Vue的方法

```js
         //可以先写数据后
		var h1 = new Vue({
            //  el: '#h1',
             data:{
                 shuju:"你是小垃圾",
                 name:"其实你不是小垃圾，你是大垃圾，嘻嘻"
             }
         })
         h1.$mount = "#h1"
```

### 3.vue里面的事件和事件修饰符

下面是常用的修饰符

**注意**：vue事件是能够链式写法的，也就是说想同时绑定两个事件在后面写就行了

#### 事件代码:

```javascript
const vw = new Vue({
            el:"#nv",
            methods: {
                // 里面的element表示发生事件的目标
                //element.target拿到事件发生的对象，innerText表示输出对象的值
                show(event){
                    console.log(element.target.innerText);
                },
                //改变指定事件位置的值
                show2(event){
                    event.target.innerText="无敌"
                    console.log(event.target.innerText);
                },
                //vue传参
                show3(event,number){
                    event.target.innerText="无敌"
                    console.log(event.target.innerText);
                    console.log(number)
                }
            }
        })
```

```html
    <div id="nv">
        <h1 v-on:click="show">你是傻逼就点击我</h1>
        <h1 @click="show2">二号机无敌于世间</h1>
        <h1 @click="show3($event,6666)">二号机无敌于世间</h1>
    </div>
```

#### 绑定多个事件：

```html
<input type="text" placeholder="按下回车提示你" @keyup.enter.prevent="show($event)">
```

#### 按键事件:

#### 查看按键本身的名字：

```JavaScript
console.log(event.key)，将真名绑定在vue事件后面就行了
```

> <img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211113102215256.png" alt="image-20211113102215256" style="zoom:50%;" />

#### 同时绑定两个键位比如Ctrl+y

```HTml
<input type="text" placeholder="按下回车提示你" @keyup.ctrl.y="show($event)">
```

代码:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>vue按键事件</title>
    <script src="../vue.js"></script>
</head>
<body>
    <!-- 获取按下键的值 -->
    <div id="keyCode">
        <h1>输出按键的值</h1>
        <input type="text" placeholder="按下回车提示你" @keyup="show($event)">
    </div>
    <!-- 绑定事件只有按下对应键才能反应 -->
    <div id="keyCode2">
        <h1>输出按键的值</h1>
        <input type="text" placeholder="按下回车提示你" @keyup.enter.prevent="show($event)">
    </div>
    <script>
        const vw = new Vue({
            el:"#keyCode",
            methods: {
                show(event) {
                    //这个可以打印按下键的值,注意event.keyCode就是键盘键值对应的数值
                    console.log(event.key)
                }
            }
        });
        const vw2 = new Vue({
            el:"#keyCode2",
            methods: {
                show(event) {
                    //这个可以打印按下键的值
                    console.log(event.key)
        
                }
            }
        });
    </script>
</body>
</html>
```

### vue自定义指令

使用这个选项可以自定义指令，其中包含了两种方式，一种是函数式直接绑定，一种是对象式选择绑定时机

```js
directives: {
    red(el, data) {
        if (data.value) {
            el.style.color = 'red';
        }
    },
        focux: {
            update(el, item) {
                if (item.value) {
                    el.focus();
                }
            },
                //初始化就执行这个方法
                inserted(el) {
                    // 聚焦元素
                    el.focus()
                }
            //
        },
},
```

### 路由:

#### 路由守卫:

调用 `beforeEach`方法,to表示即将进入的,from表示当前的,next是一个路由方法操控路由,下面是判断是否登入

```js
const router = new VueRouter({
  routes
})
// 设置路由守卫
router.beforeEach((to,from,next) => {
  //当用户进入购物车时做判定,如果登入了,则进入购物车,没有登入则跳转到登入页面
  if(to.name=='Cart'){
    console.log('进入了Cart',storge.fetch())
    if(storge.fetch().name){
      next()
    }else{
      next('/')
    }
  }else{  
    next()
  }
})
```

storge将数据储存在浏览器缓存方法:

```js
//将数据保存到浏览器中
const key = "key"
let itemLocalStorage = {
    fetch() {
        let jsonStr = localStorage.getItem(key)
        let obj = JSON.parse(jsonStr) || {}
        return obj
    },
    save(item) {
        localStorage.setItem(key, JSON.stringify(item))
    }
}
export default itemLocalStorage
```

### 常用组件库

#### vant.js

引入--`npm install vant -S`

全部引入与按需引入

```js
//全部引入
import vant from 'vant'
Vue.use(vant)
//按需引入
import {Button} from 'vant'
Vue.use(Button)
```

#### mockjs

mockjs可以不通过后端直接进行test测试

`npm install mockjs -D  `

安装mockjs -D 表示在生产环境下不打包

##### 案例：

新建文件mockjs：

```js
import Mock from 'mockjs'
//模拟请求与响应第一个参数是url,第二个是模拟结果
Mock.mock('http://localhost:8081/aoteman',{
    code:0,
    msg:'请求成功!'
})
```

在main中引用：

```js
import './tool/api/mock.js'
```

它能自动拦截所有请求

```js
qingqiu() {
    Axios({
        method: 'get',
        url: 'http://localhost:8081/aoteman',
    }).then((res)=>{
        console.log(res)
    })
}
```

#### 动漫组件库：

安装动漫效果animate.css

安装--`npm install animate.css`，只想要有一个组件有动漫效果，请把元素加在指定Vue的根元素上面

```html
<transition enter-active-class="animate__bounceInRight" mode="out-in">
    <router-view/>
</transition>
<div class="animate__animated">
    <van-search v-model="value" shape="round" placeholder="请输入搜索关键词"/>
</div>
```

main文件:

```js
import 'animate.css'
```

#### 图表库

引入v-charts图标库：

```shell
npm install v-charts echarts -S
```

引入全部图表

```js
// main.js
import Vue from 'vue'
import VCharts from 'v-charts'
import App from './App.vue'

Vue.use(VCharts)

new Vue({
  el: '#app',
  render: h => h(App)
})
```

#### 文本编辑器

引入文本编辑器

```shell
npm install tinymce@4.7.5 -S
npm install @tinymce/tinymce-vue@3.0.1 -S
npm install tinymce --savex
```

引入需要的插件

```js
import tinymce from 'tinymce/tinymce'
import 'tinymce/themes/modern/theme'
import Editor from '@tinymce/tinymce-vue'
import 'tinymce/plugins/image'
import 'tinymce/plugins/link'
import 'tinymce/plugins/code'
import 'tinymce/plugins/table'
import 'tinymce/plugins/lists'
import 'tinymce/plugins/contextmenu'
import 'tinymce/plugins/wordcount'
import 'tinymce/plugins/colorpicker'
import 'tinymce/plugins/textcolor'
```

但是这写是英文的，还需要引入中文语言包，找到tinymce在node_mode里面的位置，将中文语言包放入即可

初始化编辑对象

```js
init: {
    skin_url: "/tinymce/skins/lightgray",
    height: 300,
    plugins:"link lists image code table colorpicker textcolor wordcount contextmenu",
    toolbar:"bold italic underline strikethrough | fontsizeselect | forecolor backcolor | alignleft aligncenter alignright alignjustify | bullist numlist | outdent indent blockquote | undo redo | link unlink image code | removeformat",
    branding: false,
},
```

html代码

```html
<el-form-item label="商品详情">
    <editor :init="init"></editor>
</el-form-item>
```

vue代码

```js
components: {
    Editor,
},
mounted() {
    tinymce.init({})
},
```

### 拦截器

![image-20220114165342792](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20220114165342792.png)

### 打包部署

```shell
npm run-script build
```

## [钩子函数](https://cn.vuejs.org/v2/guide/custom-directive.html#钩子函数)

一个指令定义对象可以提供如下几个钩子函数 (均为可选)：

- `bind`：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。
- `inserted`：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)。
- `update`：所在组件的 VNode 更新时调用，**但是可能发生在其子 VNode 更新之前**。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新 (详细的钩子函数参数见下)。

我们会在[稍后](https://cn.vuejs.org/v2/guide/render-function.html#虚拟-DOM)讨论[渲染函数](https://cn.vuejs.org/v2/guide/render-function.html)时介绍更多 VNodes 的细节。

- `componentUpdated`：指令所在组件的 VNode **及其子 VNode** 全部更新后调用。
- `unbind`：只调用一次，指令与元素解绑时调用。

接下来我们来看一下钩子函数的参数 (即 `el`、`binding`、`vnode` 和 `oldVnode`)。

### 4.计算属性

**注意**：在vue对象中，this始终表示这vue对象本身

**代码**:在vue里面调用一个关键字**computed**,在里面加上一个**fullName**,vue会直接调用这里面创造的get()方法里面的返回值,也就是说你在**computed**创建了一个对象,vue会在本身对象创造一个同名属性**fullName**,调用对象的get()方法,将fullName=get()返回值,当调用fullName对象的set()方法时,vue会刷新本身

```JavaScript
computed:{
         fullName:{
             //当调用时执行下面方法
                 get(){
                     return this.xing+this.ming
                    }
                }
    			//当修改时执行下面方法
   				set(value){
        
                }
           }
```

### 5.监视属性watch

** 使用方式：** 在vue中创建watch属性，当监视对象发生变化的时候，调用与属性同名函数

** 监视范围: ** vue对象的属性在data中和计算属性都能监视

#### 代码：

```html
<div id="notKaiXin">
        <h1>今天的天气一点都不凉爽{{massge?"你是猪":"你不是猪"}}</h1>
        <button class="el-button" @click="dianji">点击切换天气</button>
</div>
  
    <script>
        new Vue({
            el:"#notKaiXin",
            data: {
               massge:true
            },
            methods:{
                dianji(){
                    this.massge=!this.massge
                }
            },
            watch:{
                massge(newVal,oldVal){
                    console.log("massge值发生了变化",newVal,oldVal)
                }
            }
        })
    </script>
```

```javascript
            watch:{
                massge(newVal,oldVal){
                    console.log("massge值发生了变化",newVal,oldVal)
                }
            }
```

#### **第二种写法**:对象式调用->

> <img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211113165811314.png" alt="image-20211113165811314" style="zoom:50%;" />

#### **第三种写法:外部调用**

**代码:**

```JavaScript
        //外部写法
        vw.$watch("massge",function(newVal,oldVal){
            console.log("外部写法：massge值发生了变化",newVal,oldVal)
        })
```

### 6.改变class样式

#### 添加一个class值:

```html
<button :class="{but:true,pad:banduan}" @click="butQue">店家获取数据</button>
```

直接使用字符串就好了

#### 添加多个class值:

添加一个数组就好了

#### **添加多个class的对象不确定式写法(推荐使用)**:

```html
 <button :class="{but:true,pad:banduan}" @click="butQue">店家获取数据</button>
```

```javascript
data(){
       return{
           data: "音乐",
           list:[],
		    banduan:false
                }
    },
```

在data里面定义一个判断层,对需要显示的css元素进行显示

### 7.条件渲染

### 8.for列表渲染

**注意点**:for渲染有一个特别需要注意的地方,就是key唯一标识必须要是唯一的,不能用index数组的一个顺序进行,否则在一些特殊的情况下会造成资源的浪费,比如说在第一个前面添加一个数值。

1. 基本的列表渲染:

```js
<!-- 下面这两个就是视窗样本罗,{completed:false,view:true}判断是否被选中 -->
				<li :class="{completed:!item.checked,view:item.checked}" v-if="showList.length>0"
					v-for="(item, index) in showList" :key="index">
					<div class="view">
						<!-- 选中的就要加checked这个东东 -->
						<input class="toggle" type="checkbox" :value="item.id" @click="selectOne(index)"
							v-model="!item.checked">
						<label>{{item.text}}</label>
						<button class="destroy" @click="destroy(index)"></button>
					</div>
					<input class="edit" value="Create a TodoMVC template">
				</li>
```

**注意:**`key`处最好不要用 `index`,因为会出现不是唯一值的问题,因为坐标会是改变的,vue函数无法确定改对象

**代码:**

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>基本列表</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 
				v-for指令:
						1.用于展示列表数据
						2.语法：v-for="(item, index) in xxx" :key="yyy"
						3.可遍历：数组、对象、字符串（用的很少）、指定次数（用的很少）
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<!-- 遍历数组 -->
			<h2>人员列表（遍历数组）</h2>
			<ul>
				<li v-for="(p,index) of persons" :key="index">
					{{p.name}}-{{p.age}}
				</li>
			</ul>

			<!-- 遍历对象 -->
			<h2>汽车信息（遍历对象）</h2>
			<ul>
				<li v-for="(value,k) of car" :key="k">
					{{k}}-{{value}}
				</li>
			</ul>

			<!-- 遍历字符串 -->
			<h2>测试遍历字符串（用得少）</h2>
			<ul>
				<li v-for="(char,index) of str" :key="index">
					{{char}}-{{index}}
				</li>
			</ul>

			<!-- 遍历指定次数 -->
			<h2>测试遍历指定次数（用得少）</h2>
			<ul>
				<li v-for="(number,index) of 5" :key="index">
					{{index}}-{{number}}
				</li>
			</ul>
		</div>

		<script type="text/javascript">
			Vue.config.productionTip = false

			new Vue({
				el:'#root',
				data:{
					persons:[
						{id:'001',name:'张三',age:18},
						{id:'002',name:'李四',age:19},
						{id:'003',name:'王五',age:20}
					],
					car:{
						name:'奥迪A8',
						price:'70万',
						color:'黑色'
					},
					str:'hello'
				}
			})
		</script>
</html>
```

2. **key的原理:**

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>key的原理</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 
				面试题：react、vue中的key有什么作用？（key的内部原理）

						1. 虚拟DOM中key的作用：
						key是虚拟DOM对象的标识，当数据发生变化时，Vue会根据【新数据】生成【新的虚拟DOM】, 
						 随后Vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较，比较规则如下：
				
						2.对比规则：
						(1).旧虚拟DOM中找到了与新虚拟DOM相同的key：
						①.若虚拟DOM中内容没变, 直接使用之前的真实DOM！
						②.若虚拟DOM中内容变了, 则生成新的真实DOM，随后替换掉页面中之前的真实DOM。

									(2).旧虚拟DOM中未找到与新虚拟DOM相同的key
												创建新的真实DOM，随后渲染到到页面。
						
						3. 用index作为key可能会引发的问题：
							1. 若对数据进行：逆序添加、逆序删除等破坏顺序操作:
									产生没有必要的真实DOM更新 ==> 界面效果没问题, 但效率低。

							2. 如果结构中还包含输入类的DOM：
															会产生错误DOM更新 ==> 界面有问题。

						4. 开发中如何选择key?:
							1.最好使用每条数据的唯一标识作为key, 比如id、手机号、身份证号、学号等唯一值。
							2.如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示，
												使用index作为key是没有问题的。
		-->
		<!-- 准备好一个容器-->
		<div id="root">
			<!-- 遍历数组 -->
			<h2>人员列表（遍历数组）</h2>
			<button @click.once="add">添加一个老刘</button>
			<ul>
				<li v-for="(p,index) of persons" :key="index">
					{{p.name}}-{{p.age}}
					<input type="text">
				</li>
			</ul>
		</div>

		<script type="text/javascript">
			Vue.config.productionTip = false

			new Vue({
				el:'#root',
				data:{
					persons:[
						{id:'001',name:'张三',age:18},
						{id:'002',name:'李四',age:19},
						{id:'003',name:'王五',age:20}
					]
				},
				methods: {
					add(){
						const p = {id:'004',name:'老刘',age:40}
						this.persons.unshift(p)
					}
				},
			})
		</script>
</html>
```

### 9.vue操作数据的原理（监视数据改变，并且在页面上调用DAO层）

**原理：**

> vue在对象中监视数据改变->通过监视对象中数据频繁调用get,set方法实现
>
> vue监视数组中数据改变->通过判断是否调用了操作数组的原生api实现,
>
> 所以想要修改数组中的数据,还得在页面的显示,就必须得调用数组的api才能实现

代码:

实例:

```JavaScript
        var vw = new Vue({
            el:"#root",
            data:{
                prson:{
                    name:"zhanxuexi",
                    age:18,
                }
            }
        })
        //动态的往对象里面添加属性
        vw.$set(vw.prson,"sex","男")
        console.log(vw.prson.sex)
```

> <img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211114173842319.png" alt="image-20211114173842319" style="zoom:50%;" />

### 10. axios

```
易用、简洁且高效的http库,安装方式:
```

`npm install axios`,Axios 是一个基于 promise 的 HTTP 库，可以用在浏览器和 node.js 中使用。

```
官网api地址:
```

`[axios中文文档|axios中文网 | axios (axios-js.com)](http://www.axios-js.com/zh-cn/docs/)`

```
get请求与post请求的简单使用:
```

```JavaScript
// 为给定 ID 的 user 创建请求
axios.get('/user?ID=12345')
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });

// 上面的请求也可以这样做
axios.get('/user', {
    params: {
      ID: 12345
    }
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
//执行post请求
axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

```
执行多个请求:
```

```JavaScript
function getUserAccount() {
  return axios.get('/user/12345');
}

function getUserPermissions() {
  return axios.get('/user/12345/permissions');
}

axios.all([getUserAccount(), getUserPermissions()])
  .then(axios.spread(function (acct, perms) {
    // 两个请求现在都执行完成
  }));
```

```
请求配置:
```

`<font color='red'>`url是必须的 `</font>`(config对象)

| 参数名称              | 参数作用                                                                                                                                                                                                                                                                     |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| url                   | `url` 是用于请求的服务器 URL                                                                                                                                                                                                                                               |
| method                | `method` 是创建请求时使用的方法                                                                                                                                                                                                                                            |
| baseURL               | `baseURL` 将自动加在 `url` 前面，除非 `url` 是一个绝对 URL, 它可以通过设置一个 `baseURL` 便于为 axios 实例的方法传递相对 URL                                                                                                                                         |
| transformRequest      | `transformRequest` 允许在向服务器发送前，修改请求数据 ,只能用在 'PUT', 'POST' 和 'PATCH' 这几个请求方法 ,后面数组中的函数必须返回一个字符串，或 ArrayBuffer，或 Stream                                                                                                     |
| transformResponse     | `transformResponse` 在传递给 then/catch 前，允许修改响应数据                                                                                                                                                                                                               |
| headers               | `headers` 是即将被发送的自定义请求头                                                                                                                                                                                                                                       |
| params                | `params` 是即将与请求一起发送的 URL 参数 , 必须是一个无格式对象(plain object)或 URLSearchParams 对象                                                                                                                                                                       |
| paramsSerializer      | `paramsSerializer` 是一个负责 `params` 序列化的函数 ,(e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)                                                                                                                                        |
| data                  | `data` 是作为请求主体被发送的数据 ,只适用于这些请求方法 'PUT', 'POST', 和 'PATCH' ,在没有设置 `transformRequest` 时，必须是以下类型之一: - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams ,- 浏览器专属：FormData, File, Blob ,- Node 专属： Stream |
| timeout               | `timeout` 指定请求超时的毫秒数(0 表示无超时时间),如果请求话费了超过 `timeout` 的时间，请求将被中断                                                                                                                                                                       |
| withCredentials       | `withCredentials` 表示跨域请求时是否需要使用凭证                                                                                                                                                                                                                           |
| proxy                 | 'proxy' 定义代理服务器的主机名称和端口  ,`auth` 表示 HTTP 基础验证应当用于连接代理，并提供凭据  ,这将会设置一个 `Proxy-Authorization` 头，覆写掉已有的通过使用 `header` 设置的自定义 `Proxy-Authorization` 头。                                                      |
| httpAgent和httpsAgent | `httpAgent` 和 `httpsAgent` 分别在 node.js 中用于定义在执行 http 和 https 时使用的自定义代理。允许像这样配置选项:`keepAlive` 默认没有启用                                                                                                                              |
| socketPath            | ' socketPath '定义了一个在node.js中使用的UNIX Socket。                                                                                                                                                                                                                       |
| maxRedirects          | `maxRedirects` 定义在 node.js 中 follow 的最大重定向数目   // 如果设置为0，将不会 follow 任何重定向                                                                                                                                                                        |
| validateStatus        | `validateStatus` 定义对于给定的HTTP 响应状态码是 resolve 或 reject  promise 。如果 `validateStatus` 返回 `true` (或者设置为 `null` 或 `undefined`)，promise 将被 resolve; 否则，promise 将被 rejecte                                                               |
| maxContentLength      | `maxContentLength` 定义允许的响应内容的最大尺寸                                                                                                                                                                                                                            |
| onDownloadProgress:   | `onUploadProgress` 允许为上传处理进度事件                                                                                                                                                                                                                                  |

```
算了不写了，自己有需求的请参考下面的官方文档：
```

```javascript
{
   // `url` 是用于请求的服务器 URL
  url: '/user',

  // `method` 是创建请求时使用的方法
  method: 'get', // default

  // `baseURL` 将自动加在 `url` 前面，除非 `url` 是一个绝对 URL。
  // 它可以通过设置一个 `baseURL` 便于为 axios 实例的方法传递相对 URL
  baseURL: 'https://some-domain.com/api/',

  // `transformRequest` 允许在向服务器发送前，修改请求数据
  // 只能用在 'PUT', 'POST' 和 'PATCH' 这几个请求方法
  // 后面数组中的函数必须返回一个字符串，或 ArrayBuffer，或 Stream
  transformRequest: [function (data, headers) {
    // 对 data 进行任意转换处理
    return data;
  }],

  // `transformResponse` 在传递给 then/catch 前，允许修改响应数据
  transformResponse: [function (data) {
    // 对 data 进行任意转换处理
    return data;
  }],

  // `headers` 是即将被发送的自定义请求头
  headers: {'X-Requested-With': 'XMLHttpRequest'},

  // `params` 是即将与请求一起发送的 URL 参数
  // 必须是一个无格式对象(plain object)或 URLSearchParams 对象
  params: {
    ID: 12345
  },

   // `paramsSerializer` 是一个负责 `params` 序列化的函数
  // (e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
  paramsSerializer: function(params) {
    return Qs.stringify(params, {arrayFormat: 'brackets'})
  },

  // `data` 是作为请求主体被发送的数据
  // 只适用于这些请求方法 'PUT', 'POST', 和 'PATCH'
  // 在没有设置 `transformRequest` 时，必须是以下类型之一：
  // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
  // - 浏览器专属：FormData, File, Blob
  // - Node 专属： Stream
  data: {
    firstName: 'Fred'
  },

  // `timeout` 指定请求超时的毫秒数(0 表示无超时时间)
  // 如果请求话费了超过 `timeout` 的时间，请求将被中断
  timeout: 1000,

   // `withCredentials` 表示跨域请求时是否需要使用凭证
  withCredentials: false, // default

  // `adapter` 允许自定义处理请求，以使测试更轻松
  // 返回一个 promise 并应用一个有效的响应 (查阅 [response docs](#response-api)).
  adapter: function (config) {
    /* ... */
  },

 // `auth` 表示应该使用 HTTP 基础验证，并提供凭据
  // 这将设置一个 `Authorization` 头，覆写掉现有的任意使用 `headers` 设置的自定义 `Authorization`头
  auth: {
    username: 'janedoe',
    password: 's00pers3cret'
  },

   // `responseType` 表示服务器响应的数据类型，可以是 'arraybuffer', 'blob', 'document', 'json', 'text', 'stream'
  responseType: 'json', // default

  // `responseEncoding` indicates encoding to use for decoding responses
  // Note: Ignored for `responseType` of 'stream' or client-side requests
  responseEncoding: 'utf8', // default

   // `xsrfCookieName` 是用作 xsrf token 的值的cookie的名称
  xsrfCookieName: 'XSRF-TOKEN', // default

  // `xsrfHeaderName` is the name of the http header that carries the xsrf token value
  xsrfHeaderName: 'X-XSRF-TOKEN', // default

   // `onUploadProgress` 允许为上传处理进度事件
  onUploadProgress: function (progressEvent) {
    // Do whatever you want with the native progress event
  },

  // `onDownloadProgress` 允许为下载处理进度事件
  onDownloadProgress: function (progressEvent) {
    // 对原生进度事件的处理
  },

   // `maxContentLength` 定义允许的响应内容的最大尺寸
  maxContentLength: 2000,

  // `validateStatus` 定义对于给定的HTTP 响应状态码是 resolve 或 reject  promise 。如果 `validateStatus` 返回 `true` (或者设置为 `null` 或 `undefined`)，promise 将被 resolve; 否则，promise 将被 rejecte
  validateStatus: function (status) {
    return status >= 200 && status < 300; // default
  },

  // `maxRedirects` 定义在 node.js 中 follow 的最大重定向数目
  // 如果设置为0，将不会 follow 任何重定向
  maxRedirects: 5, // default

  // `socketPath` defines a UNIX Socket to be used in node.js.
  // e.g. '/var/run/docker.sock' to send requests to the docker daemon.
  // Only either `socketPath` or `proxy` can be specified.
  // If both are specified, `socketPath` is used.
  socketPath: null, // default

  // `httpAgent` 和 `httpsAgent` 分别在 node.js 中用于定义在执行 http 和 https 时使用的自定义代理。允许像这样配置选项：
  // `keepAlive` 默认没有启用
  httpAgent: new http.Agent({ keepAlive: true }),
  httpsAgent: new https.Agent({ keepAlive: true }),

  // 'proxy' 定义代理服务器的主机名称和端口
  // `auth` 表示 HTTP 基础验证应当用于连接代理，并提供凭据
  // 这将会设置一个 `Proxy-Authorization` 头，覆写掉已有的通过使用 `header` 设置的自定义 `Proxy-Authorization` 头。
  proxy: {
    host: '127.0.0.1',
    port: 9000,
    auth: {
      username: 'mikeymike',
      password: 'rapunz3l'
    }
  },

  // `cancelToken` 指定用于取消请求的 cancel token
  // （查看后面的 Cancellation 这节了解更多）
  cancelToken: new CancelToken(function (cancel) {
  })
}
```

### 11. Vuex

#### 1. 使用步骤

```
创建一个叫做store的文件夹,新建index.js编写如下代码:
```

```javascript
//该文件用于创建Vuex中最为核心的store
import Vue from 'vue'
//引入Vuex
import Vuex from 'vuex'
//应用Vuex插件
Vue.use(Vuex)

//准备actions——用于响应组件中的动作
const actions = {
	/* jia(context,value){
		console.log('actions中的jia被调用了')
		context.commit('JIA',value)
	},
	jian(context,value){
		console.log('actions中的jian被调用了')
		context.commit('JIAN',value)
	}, */
	jiaOdd(context,value){
		console.log('actions中的jiaOdd被调用了')
		if(context.state.sum % 2){
			context.commit('JIA',value)
		}
	},
	jiaWait(context,value){
		console.log('actions中的jiaWait被调用了')
		setTimeout(()=>{
			context.commit('JIA',value)
		},500)
	}
}
//准备mutations——用于操作数据（state）
const mutations = {
	JIA(state,value){
		console.log('mutations中的JIA被调用了')
		state.sum += value
	},
	JIAN(state,value){
		console.log('mutations中的JIAN被调用了')
		state.sum -= value
	}
}
//准备state——用于存储数据
const state = {
	sum:0 //当前的和
}

//创建并暴露store
export default new Vuex.Store({
	actions,
	mutations,
	state,
})
```

```
在vue单组件中引用:调用对应状态的方法
```

```JavaScript
//这个是中间层dispatch（派遣）-> commit 提交修改状态 -> state（状态，仓库）->生成虚拟dom
this.$store.dispatch('jia',this.n)
```

```
一般来说都是在
```

`actions`里面提交的,不过简单情况可以直接引用:

```javascript
jiaOdd(context,value){
		console.log('actions中的jiaOdd被调用了')
		if(context.state.sum % 2){
			context.commit('JIA',value)
		}
	},
this.$store.commit('JIA',this.n)
```

### 2. 它的生命周期:

下面是vuex全套的生命周期->

![vuex](D:\AjavaWebCompetition\vue\资料（含课件）\02_原理图\vuex.png)

### 12. Vue 的跨域获取数据,使用数据代理

1. 使用步骤:在主目录下新建一个配置文件

```
配置文件里面有一个参数叫做
```

`devServer`，

```
这个参数用于配置数据代理,它有二种配置方法：
```

```javascript
//开启代理服务器（方式一）
    devServer: {
        proxy: 'http://localhost:8080'
    },
//开启代理服务器方式二，第二种可以同时配置很多个:
    devServer: {
    proxy: {
      '/atguigu': {
        target: 'http://localhost:5000',
				pathRewrite:{'^/atguigu':''},
        // ws: true, //用于支持websocket
        // changeOrigin: true //用于控制请求头中的host值
      },
```

### 13.脚手架配置文件

#### 1.通用的配置代码

```JavaScript
module.exports = {
    publicPath: "./", // 公共路径 默认为"/"，建议使用"./"相对路径
    devServer: {   // 本地服务器配置(npm run serve)
      port: 8081, // 端口
      host: "localhost", // 域名
      https: false, // 是否开启https
      open: true,	// 是否在开启服务器后自动打开浏览器访问该服务器
      proxy: 'http://localhost:8080' //开启代理服务器,服务地址为8080
    },
    lintOnSave: false,  // 取消lint语法检测，此处可不配置
    outputDir:"dist", // build打包输出目录
    assetsDir:"assets", // 静态文件输出目录，基于dist
    indexPath: "index.html",  // 输出html文件名
    productionSourceMap: false, // 取消.map文件的打包，加快打包速度
    configureWebpack: (config) => {
      // process.env为环境变量，分别对应.env.development文件和.env.production文件 此处表示加快开发环境打包速度
      if (process.env.NODE_ENV !== 'production') return;
      config.optimization.minimizer[0].options.terserOptions.compress.drop_console = true;	//生产环境去掉console.log
      return {  // 此处配置webpack.config.js的相关配置
        plugins: [],
        performance: {}
      };
    }
};

```

## Vue3

### 1.简介

1. vue3在官网的定义是海贼王

```

```

`<img src="https://user-images.githubusercontent.com/499550/93624428-53932780-f9ae-11ea-8d16-af949e16a09f.png" style="width:200px" />`

2. 特点:全面支持ts,放弃对象式写法,采用函数式编程
3. + 2020年9月18日，Vue.js发布3.0版本，代号：One Piece（海贼王）
   + 耗时2年多、[2600+次提交](https://github.com/vuejs/vue-next/graphs/commit-activity)、[30+个RFC](https://github.com/vuejs/rfcs/tree/master/active-rfcs)、[600+次PR](https://github.com/vuejs/vue-next/pulls?q=is%3Apr+is%3Amerged+-author%3Aapp%2Fdependabot-preview+)、[99位贡献者](https://github.com/vuejs/vue-next/graphs/contributors)
   + github上的tags地址：https://github.com/vuejs/vue-next/releases/tag/v3.0.0
4. + 性能的提升

   - 打包大小减少41%
   - 初次渲染快55%, 更新渲染快133%
   - 内存减少54%
   - 使用Proxy代替defineProperty实现响应式
   - 重写虚拟DOM的实现和Tree-Shaking
   - Vue3可以更好的支持TypeScrip
5. 使用vite对项目进行构建:`npm init @vitejs/app`

```shell
npm init @vitejs/app
```

### 2. 新特征

1. Composition API（组合API）

   + setup配置

   - ref与reactive
   - watch与watchEffect
   - provide与inject
   - ......
2. 新的内置组件

   - Fragment
   - Teleport
   - Suspense
3. 其他改变

   - 新的生命周期钩子
   - data 选项应始终被声明为一个函数
   - 移除keyCode支持作为 v-on 的修饰符
   - ......

### 3. 常用 Composition API

#### 1.拉开序幕的setup

1. 理解：Vue3.0中一个新的配置项，值为一个函数。
2. setup是所有 `<strong style="color:#DD5145">`Composition API（组合API）`</strong><i style="color:gray;font-weight:bold">`“ 表演的舞台 ”`</i>`。
3. 组件中所用到的：数据、方法等等，均要配置在setup中。
4. setup函数的两种返回值：
   1. 若返回一个对象，则对象中的属性、方法, 在模板中均可以直接使用。（重点关注！）
   2. `<span style="color:#aad">`若返回一个渲染函数：则可以自定义渲染内容。（了解）
5. 注意点：
   1. 尽量不要与Vue2.x配置混用
      - Vue2.x配置（data、methos、computed...）中 `<strong style="color:#DD5145">`可以访问到 `</strong>`setup中的属性、方法。
      - 但在setup中 `<strong style="color:#DD5145">`不能访问到 `</strong>`Vue2.x配置（data、methos、computed...）。
      - 如果有重名, setup优先。
   2. setup不能是一个async函数，因为返回值不再是return的对象, 而是promise, 模板看不到return对象中的属性。（后期也可以返回一个Promise实例，但需要Suspense和异步组件的配合）

#### 2.ref函数

- 作用: 定义一个响应式的数据
- 语法: ``const xxx = ref(initValue)``
  - 创建一个包含响应式数据的 `<strong style="color:#DD5145">`引用对象（reference对象，简称ref对象）`</strong>`。
  - JS中操作数据： ``xxx.value``
  - 模板中读取数据: 不需要.value，直接：``<div>{{xxx}}</div>``
- 备注：
  - 接收的数据可以是：基本类型、也可以是对象类型。
  - 基本类型的数据：响应式依然是靠 ``Object.defineProperty()``的 ``get``与 ``set``完成的。
  - 对象类型的数据：内部 `<i style="color:gray;font-weight:bold">`“ 求助 ”`</i>` 了Vue3.0中的一个新函数—— ``reactive``函数。

#### 3.reactive函数

- 作用: 定义一个 `<strong style="color:#DD5145">`对象类型 `</strong>`的响应式数据（基本类型不要用它，要用 ``ref``函数）
- 语法：``const 代理对象= reactive(源对象)``接收一个对象（或数组），返回一个 `<strong style="color:#DD5145">`代理对象（Proxy的实例对象，简称proxy对象）`</strong>`
- reactive定义的响应式数据是“深层次的”。
- 内部基于 ES6 的 Proxy 实现，通过代理对象操作源对象内部数据进行操作。

#### 4.Vue3.0中的响应式原理

##### vue2.x的响应式

- 实现原理：

  - 对象类型：通过 ``Object.defineProperty()``对属性的读取、修改进行拦截（数据劫持）。
  - 数组类型：通过重写更新数组的一系列方法来实现拦截。（对数组的变更方法进行了包裹）。

    ```js
    Object.defineProperty(data, 'count', {
        get () {}, 
        set () {}
    })
    ```
- 存在问题：

  - 新增属性、删除属性, 界面不会更新。
  - 直接通过下标修改数组, 界面不会自动更新。

##### Vue3.0的响应式

- 实现原理:

  - 通过Proxy（代理）:  拦截对象中任意属性的变化, 包括：属性值的读写、属性的添加、属性的删除等。
  - 通过Reflect（反射）:  对源对象的属性进行操作。
  - MDN文档中描述的Proxy与Reflect：

    - Proxy：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy
    - Reflect：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect

      ```js
      new Proxy(data, {
      	// 拦截读取属性值
          get (target, prop) {
          	return Reflect.get(target, prop)
          },
          // 拦截设置属性值或添加新属性
          set (target, prop, value) {
          	return Reflect.set(target, prop, value)
          },
          // 拦截删除属性
          deleteProperty (target, prop) {
          	return Reflect.deleteProperty(target, prop)
          }
      })

      proxy.name = 'tom'   
      ```

#### 5.reactive对比ref

- 从定义数据角度对比：
  - ref用来定义：`<strong style="color:#DD5145">`基本类型数据 `</strong>`。
  - reactive用来定义：`<strong style="color:#DD5145">`对象（或数组）类型数据 `</strong>`。
  - 备注：ref也可以用来定义 `<strong style="color:#DD5145">`对象（或数组）类型数据 `</strong>`, 它内部会自动通过 ``reactive``转为 `<strong style="color:#DD5145">`代理对象 `</strong>`。
- 从原理角度对比：
  - ref通过 ``Object.defineProperty()``的 ``get``与 ``set``来实现响应式（数据劫持）。
  - reactive通过使用 `<strong style="color:#DD5145">`Proxy `</strong>`来实现响应式（数据劫持）, 并通过 `<strong style="color:#DD5145">`Reflect `</strong>`操作 `<strong style="color:orange">`源对象 `</strong>`内部的数据。
- 从使用角度对比：
  - ref定义的数据：操作数据 `<strong style="color:#DD5145">`需要 ``</strong>````.value ``，读取数据时模板中直接读取 `<strong style="color:#DD5145">```不需要</strong>``````.value``。
  - reactive定义的数据：操作数据与读取数据：`<strong style="color:#DD5145">`均不需要 ``</strong>````.value``。

#### 6.setup的两个注意点

- setup执行的时机
  - 在beforeCreate之前执行一次，this是undefined。
- setup的参数
  - props：值为对象，包含：组件外部传递过来，且组件内部声明接收了的属性。
  - context：上下文对象
    - attrs: 值为对象，包含：组件外部传递过来，但没有在props配置中声明的属性, 相当于 ``this.$attrs``。
    - slots: 收到的插槽内容, 相当于 ``this.$slots``。
    - emit: 分发自定义事件的函数, 相当于 ``this.$emit``。

#### 7.计算属性与监视

##### 1.computed函数

- 与Vue2.x中computed配置功能一致
- 写法

  ```js
  import {computed} from 'vue'

  setup(){
      ...
  	//计算属性——简写,这里可以直接用对象,相当于在对象里面添加了某个属性
      let fullName = computed(()=>{
          return person.firstName + '-' + person.lastName
      })
      //计算属性——完整
      let fullName = computed({
          get(){
              return person.firstName + '-' + person.lastName
          },
          set(value){
              const nameArr = value.split('-')
              person.firstName = nameArr[0]
              person.lastName = nameArr[1]
          }
      })
  }
  ```

##### 2.watch函数

- 与Vue2.x中watch配置功能一致
- 两个小“坑”：

  - 监视reactive定义的响应式数据时：oldValue无法正确获取、强制开启了深度监视（deep配置失效）。
  - 监视reactive定义的响应式数据中某个属性时：deep配置有效。

  ```js
  //情况一：监视ref定义的响应式数据
  watch(sum,(newValue,oldValue)=>{
  	console.log('sum变化了',newValue,oldValue)
  },{immediate:true})

  //情况二：监视多个ref定义的响应式数据
  watch([sum,msg],(newValue,oldValue)=>{
  	console.log('sum或msg变化了',newValue,oldValue)
  }) 

  /* 情况三：监视reactive定义的响应式数据
  			若watch监视的是reactive定义的响应式数据，则无法正确获得oldValue！！
  			若watch监视的是reactive定义的响应式数据，则强制开启了深度监视 
  */
  watch(person,(newValue,oldValue)=>{
  	console.log('person变化了',newValue,oldValue)
  },{immediate:true,deep:false}) //此处的deep配置不再奏效

  //情况四：监视reactive定义的响应式数据中的某个属性
  watch(()=>person.job,(newValue,oldValue)=>{
  	console.log('person的job变化了',newValue,oldValue)
  },{immediate:true,deep:true}) 

  //情况五：监视reactive定义的响应式数据中的某些属性
  watch([()=>person.job,()=>person.name],(newValue,oldValue)=>{
  	console.log('person的job变化了',newValue,oldValue)
  },{immediate:true,deep:true})

  //特殊情况
  watch(()=>person.job,(newValue,oldValue)=>{
      console.log('person的job变化了',newValue,oldValue)
  },{deep:true}) //此处由于监视的是reactive素定义的对象中的某个属性，所以deep配置有效
  ```

##### 3.watchEffect函数

- watch的套路是：既要指明监视的属性，也要指明监视的回调。
- watchEffect的套路是：不用指明监视哪个属性，监视的回调中用到哪个属性，那就监视哪个属性。
- watchEffect有点像computed：

  - 但computed注重的计算出来的值（回调函数的返回值），所以必须要写返回值。
  - 而watchEffect更注重的是过程（回调函数的函数体），所以不用写返回值。

  ```js
  //watchEffect所指定的回调中用到的数据只要发生变化，则直接重新执行回调。
  watchEffect(()=>{
      const x1 = sum.value
      const x2 = person.age
      console.log('watchEffect配置的回调执行了')
  })
  ```

#### 8.生命周期

<div style="border:1px solid black;width:380px;float:left;margin-right:20px;"><strong>vue2.x的生命周期</strong><img src="https://cn.vuejs.org/images/lifecycle.png" alt="lifecycle_2" style="zoom:33%;width:1200px" /></div><div style="border:1px solid black;width:510px;height:985px;float:left"><strong>vue3.0的生命周期</strong><img src="https://v3.cn.vuejs.org/images/lifecycle.svg" alt="lifecycle_2" style="zoom:33%;width:2500px" /></div>

1

- Vue3.0中可以继续使用Vue2.x中的生命周期钩子，但有有两个被更名：
  - ``beforeDestroy``改名为 ``beforeUnmount``
  - ``destroyed``改名为 ``unmounted``
- Vue3.0也提供了 Composition API 形式的生命周期钩子，与Vue2.x中钩子对应关系如下：
  - `beforeCreate`===>`setup()`
  - `created`=======>`setup()`
  - `beforeMount` ===>`onBeforeMount`
  - `mounted`=======>`onMounted`
  - `beforeUpdate`===>`onBeforeUpdate`
  - `updated` =======>`onUpdated`
  - `beforeUnmount` ==>`onBeforeUnmount`
  - `unmounted` =====>`onUnmounted`

#### 9.自定义hook函数

- 什么是hook？—— 本质是一个函数，把setup函数中使用的Composition API进行了封装。
- 类似于vue2.x中的mixin。
- 自定义hook的优势: 复用代码, 让setup中的逻辑更清楚易懂。

#### 10.toRef

- 作用：创建一个 ref 对象，其value值指向另一个对象中的某个属性。
- 语法：``const name = toRef(person,'name')``
- 应用:   要将响应式对象中的某个属性单独提供给外部使用时。
- 扩展：``toRefs`` 与 ``toRef``功能一致，但可以批量创建多个 ref 对象，语法：``toRefs(person)``

### 4、其它 Composition API

#### 1.shallowReactive 与 shallowRef

- shallowReactive：只处理对象最外层属性的响应式（浅响应式）。
- shallowRef：只处理基本数据类型的响应式, 不进行对象的响应式处理。
- 什么时候使用?

  - 如果有一个对象数据，结构比较深, 但变化时只是外层属性变化 ===> shallowReactive。
  - 如果有一个对象数据，后续功能不会修改该对象中的属性，而是生新的对象来替换 ===> shallowRef。

#### 2.readonly 与 shallowReadonly

- readonly: 让一个响应式数据变为只读的（深只读）。
- shallowReadonly：让一个响应式数据变为只读的（浅只读）。
- 应用场景: 不希望数据被修改时。

#### 3.toRaw 与 markRaw

- toRaw：
  - 作用：将一个由 ``reactive``生成的 `<strong style="color:orange">`响应式对象 `</strong>`转为 `<strong style="color:orange">`普通对象 `</strong>`。
  - 使用场景：用于读取响应式对象对应的普通对象，对这个普通对象的所有操作，不会引起页面更新。
- markRaw：
  - 作用：标记一个对象，使其永远不会再成为响应式对象。
  - 应用场景:
    1. 有些值不应被设置为响应式的，例如复杂的第三方类库等。
    2. 当渲染具有不可变数据源的大列表时，跳过响应式转换可以提高性能。

#### 4.customRef

- 作用：创建一个自定义的 ref，并对其依赖项跟踪和更新触发进行显式控制。
- 实现防抖效果：

  ```vue
  <template>
  	<input type="text" v-model="keyword">
  	<h3>{{keyword}}</h3>
  </template>

  <script>
  	import {ref,customRef} from 'vue'
  	export default {
  		name:'Demo',
  		setup(){
  			// let keyword = ref('hello') //使用Vue准备好的内置ref
  			//自定义一个myRef
  			function myRef(value,delay){
  				let timer
  				//通过customRef去实现自定义
  				return customRef((track,trigger)=>{
  					return{
  						get(){
  							track() //告诉Vue这个value值是需要被“追踪”的
  							return value
  						},
  						set(newValue){
  							clearTimeout(timer)
  							timer = setTimeout(()=>{
  								value = newValue
  								trigger() //告诉Vue去更新界面
  							},delay)
  						}
  					}
  				})
  			}
  			let keyword = myRef('hello',500) //使用程序员自定义的ref
  			return {
  				keyword
  			}
  		}
  	}
  </script>
  ```

#### 5.provide 与 inject

<img src="https://v3.cn.vuejs.org/images/components_provide.png" style="width:300px" />

- 作用：实现 `<strong style="color:#DD5145">`祖与后代组件间 `</strong>`通信
- 套路：父组件有一个 `provide` 选项来提供数据，后代组件有一个 `inject` 选项来开始使用这些数据
- 具体写法：

  1. 祖组件中：

     ```js
     setup(){
     	......
         let car = reactive({name:'奔驰',price:'40万'})
         provide('car',car)
         ......
     }
     ```
  2. 后代组件中：

     ```js
     setup(props,context){
     	......
         const car = inject('car')
         return {car}
     	......
     }
     ```

#### 6.响应式数据的判断

- isRef: 检查一个值是否为一个 ref 对象
- isReactive: 检查一个对象是否是由 `reactive` 创建的响应式代理
- isReadonly: 检查一个对象是否是由 `readonly` 创建的只读代理
- isProxy: 检查一个对象是否是由 `reactive` 或者 `readonly` 方法创建的代理

### 5、Composition API 的优势

#### 1.Options API 存在的问题

使用传统OptionsAPI中，新增或者修改一个需求，就需要分别在data，methods，computed里修改 。

<div style="width:600px;height:370px;overflow:hidden;float:left">
    <img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f84e4e2c02424d9a99862ade0a2e4114~tplv-k3u1fbpfcp-watermark.image" style="width:600px;float:left" />
</div>
<div style="width:300px;height:370px;overflow:hidden;float:left">
    <img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e5ac7e20d1784887a826f6360768a368~tplv-k3u1fbpfcp-watermark.image" style="zoom:50%;width:560px;left" /> 
</div>

#### 2.Composition API 的优势

我们可以更加优雅的组织我们的代码，函数。让相关功能的代码更加有序的组织在一起。

<div style="width:500px;height:340px;overflow:hidden;float:left">
    <img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bc0be8211fc54b6c941c036791ba4efe~tplv-k3u1fbpfcp-watermark.image"style="height:360px"/>
</div>
<div style="width:430px;height:340px;overflow:hidden;float:left">
    <img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6cc55165c0e34069a75fe36f8712eb80~tplv-k3u1fbpfcp-watermark.image"style="height:360px"/>
</div>

### 6、新的组件

#### 1.Fragment

- 在Vue2中: 组件必须有一个根标签
- 在Vue3中: 组件可以没有根标签, 内部会将多个标签包含在一个Fragment虚拟元素中
- 好处: 减少标签层级, 减小内存占用

#### 2.Teleport

- 什么是Teleport？—— `Teleport` 是一种能够将我们的 `<strong style="color:#DD5145">`组件html结构 `</strong>`移动到指定位置的技术。

  ```vue
  <teleport to="移动位置">
  	<div v-if="isShow" class="mask">
  		<div class="dialog">
  			<h3>我是一个弹窗</h3>
  			<button @click="isShow = false">关闭弹窗</button>
  		</div>
  	</div>
  </teleport>
  ```

#### 3.Suspense

- 等待异步组件时渲染一些额外内容，让应用有更好的用户体验
- 使用步骤：

  - 异步引入组件

    ```js
    import {defineAsyncComponent} from 'vue'
    const Child = defineAsyncComponent(()=>import('./components/Child.vue'))
    ```
  - 使用 ``Suspense``包裹组件，并配置好 ``default`` 与 ``fallback``

    ```vue
    <template>
    	<div class="app">
    		<h3>我是App组件</h3>
    		<Suspense>
    			<template v-slot:default>
    				<Child/>
    			</template>
    			<template v-slot:fallback>
    				<h3>加载中.....</h3>
    			</template>
    		</Suspense>
    	</div>
    </template>
    ```

### 7、其他

#### 1.全局API的转移

- Vue 2.x 有许多全局 API 和配置。

  - 例如：注册全局组件、注册全局指令等。

    ```js
    //注册全局组件
    Vue.component('MyButton', {
      data: () => ({
        count: 0
      }),
      template: '<button @click="count++">Clicked {{ count }} times.</button>'
    })

    //注册全局指令
    Vue.directive('focus', {
      inserted: el => el.focus()
    }
    ```
- Vue3.0中对这些API做出了调整：

  - 将全局的API，即：``Vue.xxx``调整到应用实例（``app``）上| 2.x 全局 API（``Vue``）  | 3.x 实例 API (`app`)                               |
    | ------------------------ | ---------------------------------------------------- |
    | Vue.config.xxxx          | app.config.xxxx                                      |
    | Vue.config.productionTip | `<strong style="color:#DD5145">`移除 `</strong>` |
    | Vue.component            | app.component                                        |
    | Vue.directive            | app.directive                                        |
    | Vue.mixin                | app.mixin                                            |
    | Vue.use                  | app.use                                              |
    | Vue.prototype            | app.config.globalProperties                          |

#### 2.其他改变

- data选项应始终被声明为一个函数。
- 过度类名的更改：

  - Vue2.x写法

    ```css
    .v-enter,
    .v-leave-to {
      opacity: 0;
    }
    .v-leave,
    .v-enter-to {
      opacity: 1;
    }
    ```
  - Vue3.x写法

    ```css
    .v-enter-from,
    .v-leave-to {
      opacity: 0;
    }

    .v-leave-from,
    .v-enter-to {
      opacity: 1;
    }
    ```
- `<strong style="color:#DD5145">`移除 `</strong>`keyCode作为 v-on 的修饰符，同时也不再支持 ``config.keyCodes``
- `<strong style="color:#DD5145">`移除 ``</strong>````v-on.native``修饰符

  - 父组件中绑定事件

    ```vue
    <my-component
      v-on:close="handleComponentEvent"
      v-on:click="handleNativeClickEvent"
    />
    ```
  - 子组件中声明自定义事件

    ```vue
    <script>
      export default {
        emits: ['close']
      }
    </script>
    ```
- `<strong style="color:#DD5145">`移除 `</strong>`过滤器（filter）

  > 过滤器虽然这看起来很方便，但它需要一个自定义语法，打破大括号内表达式是 “只是 JavaScript” 的假设，这不仅有学习成本，而且有实现成本！建议用方法调用或计算属性去替换过滤器。
  >
- ......

## Vue插件

### 1. 插件swiper(这个是轮播图插件):

1. 基本用法:

```javascript
  npm i swiper
```

```javascript
<swiper :options="swiperOptionTop" class="gallery-top" ref="swiperTop">
						<swiper-slide v-for="(item) of productDetailData.sliderImageArr" :key="item"
							:style="{backgroundImage: 'url('+ $api.BASEURL+item +')'}"></swiper-slide>
					</swiper>
<!-- 这个是那个小地图 -->
<swiper :options="swiperOptionThumbs" class="gallery-thumbs" ref="swiperThumbs">
<swiper-slide v-for="(item, index) of productDetailData.sliderImageArr" :key="index"
:style="{backgroundImage: 'url('+ $api.BASEURL+item +')'}">
<div style="width: 100%; height: 100%;" @click="thumbsClick(index)"></div>
</swiper-slide>
</swiper>
```

2. 项目配置文件(**注意这个项目值要交给行内属性 `options`**):

```javascript
// 这两个是用来操控图片的
				swiperTop: null,
				swiperThumbs: null,

				// 这个是定义配置对象与options密不可分
				swiperOptionTop: {
					spaceBetween: 10,
					loop: true,// 循环模式选项
					loopedSlides: 20
				},
				// 这个是定义配置对象与options密不可分
				swiperOptionThumbs: {
					// 这个是侧边定义按钮
					navigation: {
						nextEl: '.swiper-button-next',
						prevEl: '.swiper-button-prev'
					},
					direction: 'vertical',//这个表示垂直切换选项
					spaceBetween: 10,
					slidesPerView: 3,//这个表示小地图显示的数量
					loop: true,
					freeMode: true,
					loopedSlides: 20, // looped slides should be the same
					centeredSlides: true,
					watchSlidesVisibility: true
				},
```

### Vuex

#### 配置Vuex

```shell
//安装路由
npm install vue-router@4
```

创建router文件夹,创建index.js文件

```JavaScript
import {
    createRouter,
    createWebHashHistory,
} from 'vue-router'
import bookDetails from '../components/book/bookDetails.vue'
import home from '../components/home/home.vue'

const routes = [
    {
        path:'/bookDetails',
        component:bookDetails
    },
    {
        path:'/',
        component:home
    }
]

// 创建路由对象
const router = createRouter({
    history: createWebHashHistory(),
    routes
})
export default router;

```

对main.js进行启动插件

```JavaScript
import { createApp } from 'vue'
import App from './App.vue'

// import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
import installElementPlus from './plugins/element'
import router from './router';  

const app = createApp(App)
installElementPlus(app)
//对插件进行装配
app.use(router)
//对插件进行启动
app.mount('#app')
```

# javaWeb

## 一. 异常

### 问题一：在javaweb里面打开一个html页面不能用请求转发，必须用请求重定向，不然会报出异常。

# ES6-study

## 1. 常用语法总结

### 1. 变量形式的改变

1. 在es6中定义一个变量使用 `let`,定义一个常量使用 `const`,使用...来获取实参,其中实参像java一样被装进一个数组当中

```js
const c = '我是一个常量'
let a = '我是一个变量'
function a(...yt){
    console.log(yt)
}
```

### 2. 在数组方面的扩展

1. es6中的扩展运算符,可以把数组里面的参数全部以 `a,b,c..`的方式取出来:

```js
let d = [{
    ab : {
        name:'黄石',
        age:100,
        show(){
            console.log('你是一只猪')
        }
    },
    f(){
        return "奥特曼"
    }
}]
console.log(...d)
```

范例:

+ 使用新特征进行数组合并

```js
//使用es6新特征进行数组的合并
let qq = [21,23,54,65]
let qa = ['a','b','c','k']
let qqs = [...qq,...qa]
```

+ 使用新特征进行数组克隆

```js
let q =[]
let qs = ['a','b',1,2,3]
q = [...qs]
```

### 3.模板字符串

**模板字符串概述**：模板字符串（template string）是增强版的字符串，用反引号（`）标识，特点：字符串中可以出现换行符；可以使用 ${xxx} 形式引用变量

```js
let b = "abc"
//使用${}的方式去支持变量
let a = `<h1>你是一只猪${b}</h1>`
```

### 4. 新的关键字Symbol

**解释**:使用Symbol方法能在内存地址中指定不一样的值,也就是创建了一个唯一值,这个主要用于声明属性和方法

```js
//Symbol的使用场景
let guigan = {
    name:'age',
    age:'1',
    show:'无敌'
}
//向guigan属性中添加show方法,平常的添加会破坏数据的唯一性
//这样添加的话就不会破坏数据的原始结构,哪怕撞名
guigan[Symbol('show')] = function(){
    console.log("桂钢是猪")
}
console.log(guigan)
```

![image-20220102140820966](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20220102140820966.png)

### 5. 函数的变化

**变化:** es6允许函数自带默认值,一般在书写中把这种带默认值的参数放在后面

![image-20220102142614193](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20220102142614193.png)

### 6.迭代器

**概述:** 遍历器（Iterator）就是一种机制。它是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署 Iterator 接口，就可以完成遍历操作

**特征:** ES6 创造了一种新的遍历命令 for...of 循环，Iterator 接口主要供 for...of 消费；原生具备 iterator 接口的数据(可用 for of 遍历):

+ Array；
+ Arguments；
+ Set；
+ Map；
+ String；
+ TypedArray；
+ NodeList；
