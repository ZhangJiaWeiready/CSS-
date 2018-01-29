# CSS3(三) -- 媒体查询
## css2中的媒体查询
* < link rel="stylesheets" type="text/css" media="screen" / >
* media 值为screen 时表示只有在屏幕中的时候css才会有效
* media值为print时表示只有在打印的时候css才会有效
## css3中的媒体查询
* css3媒体查询响应式方式的核心
* 媒体类型	
	* all -- 所有的媒体（默认值）
	* print -- 打印预览
	* screen -- 彩色屏幕
	* projection     手持设备
	* tv                   电视
    * braille           盲文触觉设备
    * embossed     盲文打印机
    * speech        “听觉”类似的媒体设备
    * tty                 不适用像素的设备
* 媒体属性
	* width	--> 浏览器窗口的尺寸 -->（可加max min前缀）
	* height --> 浏览器窗口尺寸 -->（可加max min前缀）基本不用
	* device-width --> 设备-独立像素/PC端-分辨率/移动端-基本参数（可加max min前缀）
	* -webkit-device-pixel-ratio--像素比（可加max min前缀，需要加webkit前缀）
	* orientation --> 区分屏幕是否为竖屏/横屏  portrait竖屏
					*landscape横屏
* 媒体关键字（操作符）
	*only 防止老旧版本的浏览器，不支持带媒体属性的查询而应用到给定的样式
	@media only screen and （min-width：800px）{规则}
	@media screen and （min-width：800px）{规则}
		* 在老版本浏览器中
			* @media only --> 因为没有only这种设备， 规则会被忽略
	   		* @media screen --->   因为有screen这种设备而且老浏览器会忽略带媒体属性的查询
		* 建议每次写的时候都写上only 	
	* and
		* 连接媒体属性、连接媒体类型
		* 对于所有的连接选项都要匹配成功才能应用规则
	* " , "   或的意思
		* 对于所有的连接选项只要能匹配成功一个就能应用规则
	* not
		* 取反			
* 用法 -- > 在style中
	@media only screen and (max-width:100px){
		规则：选择器+声明块 （属性名+属性值）
		div{
			width:100px;
	}		}
* 位置 -- > 都必须防止在已设置的规则后面 否则会被覆盖 无效

## 多列布局
* column-width 决定每列的宽度  列数=width/column（取整）-1  因为列于列之间有间隙
* column-count 决定分成几列
* column-gap 决定列于列之间的间隔
* column-rule 决定列的边框 值与border 相似

## CSS的预处理器
### Less是什么？
* less是一种动态样式语言，属于css预处理器的范畴，扩展了css语言
* 增加了变量、mixin、函数等特性，使css更易维护和扩展
* 既可以在客户端上运行，也可以借助Node.js在服务端运行
* less的中文官网：http://lesscss.cn/
* bootstrap中less教程：http://www.bootcss.com/p/lesscss/
### Less的编译工具
* koala 官网：www.koala-app.com
### Less中的注释
* // 开头的注释，不会被编译到css文件中
* /**/ 包裹的注释，会被编译到css文件
### 用法
* 普通属性值 @name ： red -->  color ：@name
* 选择器 @div:#div --> @{div}{}
* 属性名 @width：width --> @{width}:800px;
* 给元素设置：hover 用& 否则会有空格 紧贴选择器后面
* 变量的延迟加载
	* @var: 0;
	.class {
	@var: 1;
    	.brass {
      	@var: 2;
      	three: @var;//3  
      	@var: 3;
    	}
  	one: @var;  
	}
###Less混合
混合就是将一系列属性从一个规则集引入到另一个规则集的方式
	1.普通混合
		.cssstyle{可以共用的属性} 
		--> .cssstyle
		后果 --> 普通混合会输出到css文件中     
	2.不带输出的混合
	.cssstyle（）{可以共用的属性} 
		--> .cssstyle（）
	3.带参数的混合
	.cssstyle（@a，@B，@C）{可以共用的属性} 
		--> .cssstyle（100px,100px,red）
	4.带参数并且有默认值的混合
	.cssstyle（@a:10px，@B:10px，@C:red）{可以共用的属性} 
		--> .cssstyle（）
	5.带多个参数的混合
	6.命名参数
	.cssstyle(@c:black) 指定某个的参数
	7.匹配模式
	@import""引入less文件
	8.arguments变量