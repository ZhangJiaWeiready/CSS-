# CSS(二)
##
### 1、CSS2回顾+选择器
	1.Cascading  style sheets
	2.样式表的组成
		规则
			选择器+声明块
					声明
						CSS合法的属性名+属性值
	3.浏览器渲染样式表的顺序
		从右往左
	4.选择器
		基本选择器及其扩展
			* . # 后代 组合（#test.pink）
			> + ~ 分组（，结合符）
		属性选择器
			存在与值 属性选择器
				[attr] [attr="val"] [attr~="val"](只认空格)
			子串值 属性选择器
				^ $ * |(val val-)
		伪类与伪元素选择器
			链接伪类
				:link :visited :target(css实现选项卡)
			动态伪类
				:hover :active(lvha)
			表单伪类
				:disabled :enabled	:checked(自定义单选按钮) :focus
			结构性伪类
				ele:nth-child(index)
				ele:nth-of-type(index) 以元素为中心
				
				区别：
					1.nth-child找到第index个子元素  这个子元素必须满足ele的规则
					  nth-of-type找到底index个ele子元素
					2.nth-of-type以元素为中心
				注意：
					index可以是变量n（只能是n  0到正无穷）
							odd：奇数
							even：偶数	
			伪元素
				::after
				::before
				
		CSS声明的优先级
			层叠
				先按来源进行筛选
				如果来源相同，按选择器的特殊性继续筛选
				选择器的特殊性如果相同，按顺序继续筛选
	5.自定义字体
		@font-face
		字体图标
			1.制作一套矢量图
			2.将矢量图与字符进行绑定
			3.使用工具或者站点生成一套字体
			4.最终使用
		 字体兼容处理网站
	       https://www.fontsquirrel.com/tools/webfont-generator
	    icomoon字体图标
	       https://icomoon.io/#home
	
	6.文本新增样式
		文本阴影
		怎么溢出显示省略号
			white-space=no-wrap
			overflow=hidden
			text-overflow=ellipsis
			包裹区域必须不能让子元素撑开
###
### 2、盒模型/阴影
	1.盒模型新增样式
		box-shadow
			关键字(内 外阴影)
			length(x轴的偏移量)
			length(y轴的偏移量)
			length(模糊程度)
			length(阴影面积)
			color(阴影颜色)
		text-shadow
			length(x轴的偏移量)
			length(y轴的偏移量)
			length(模糊程度)
			color(阴影颜色)
	2.倒影（webkit内核  文字描边  背景镂空）
		渐变倒影
	3.box-sizing
		border-box：代表元素上设置的width和height表示的是border-box尺寸
		content-box：代表元素上设置的width和height表示的是content-box尺寸
	4.层级
		a.浮动提升半层，只有在浮动的情况下，才需要考虑元素分两层
			定位元素提一层
				相对定位会在文档流你有残留
		b.z-index为1怎么都会比a高;z-index为-1怎么都会比a低
	5.包含块
		初始包含块：和视窗大小位置尺寸一样的矩形
			滚动系统滚动条会不会影响初始包含块的位置？
				会
			禁止系统滚动条
				html,body{
					height:100%;
					overflow:hidden
				}
			怎么解决ie6下固定定位失效的问题？
				用绝对定位来模拟固定定位
					1.禁止系统滚动条
					2.将滚动条作用在最外层的包裹器上或者在body上
					3.因为移动包裹器或者body身上的滚动条并不会影响初始包含块的位置
						所以一个按照初始包含块定位的元素就不会产生移动
	6.边框图片、渐变
	7.背景
		css2
			background-color	平铺整个border-box
			background-image	默认从padding-box开始绘制，从border-box开始剪裁
								css3中有多背景，默认绘制时尺寸是自己的位图像素
			background-repeat
								控制平铺与否
			background-position
								控制背景图片在背景区域中的位置
								px
								百分比
									参照于背景区域减去背景图片的位图像素值
			background-attachment
								scroll：默认值，背景图不会随着元素滚动条的滚动而滚动
								fixed：背景图铺在视口中固定定位了
		css3
			background-origin
			background-clip
			background-size 
				图片是自适应的
	8.如何实现一张图片的垂直水平居中
		* body:after{
			content: "";
			display: inline-block;
			height: 100%;
			vertical-align: middle;
		}
		img{
			vertical-align: middle;
		}
		* div{
			  position:absolute;
			  top:0;
		      left:0;
			  right:0;
			  bottom:0;
			  margin:auto;
		}
		* div{
			 position:absolute;
			 left:50%;
			 top:50%;
			 margin-top:-"一半"px; //相对于自己高度的50%
			 margin-left：-"一半"px; //相对于自己宽度的50%
		}
		* div{
			 position:absolute;
			 left:50%;
			 top:50%;
			 transform:translate(-50%，-50%)
		 }
		
### 3、过渡和2d变换
	a.过渡只关系元素的初始状态和结束状态，没有方法可以获取元素在过渡中每一帧的状态
	b.元素在初次渲染还没有结束的时候，是没有办法触发过渡的
	c.在绝大部分变换样式的切换时，变换组合的个数或位置不一样时，是没有办法触发过渡的


	1.过渡
		transition-property 
			指定过渡动画的属性（并不是所有的属性都可以动画）
		transition-duration
			指定过渡动画的时间（0也要带单位）
		transition-timing-function
			指定过渡动画的形式（贝塞尔）
		transition-delay
			指定过渡动画的延迟
		transition
			第一个可以被解析成时间的值会赋给transition-duration
		transtionend事件（DOM2）
			在每个属性完成过渡时都会触发这个事件
		当属性值的列表长度不一致时
			跟时间有关的重复列表
			transition-timing-function使用默认值
	
	2.2D变换（transform）
		rotate
			旋转
		translate
			平移
		skew
			斜切
		scale
			缩放
		变换组合!
			计算的顺序是从右往左的，变换的底层其实就是矩阵的运算。
			执行的顺序还是从左到右。
		基点的变换
		transform-origin（x y z）
		* 必须带单位 px/s/ms
		* /*Y正值表示推动右胳膊，负值表示推左胳膊*/
            /*X正值表示推动脑袋，负值推腿*/
            /*Z正值表示顺时针转，负值逆时针转*/
	transform中的个数尽量都相同
### 04、3D变换/动画
	1.3D变换
	![](https://i.imgur.com/IRn9XxQ.jpg)
	/- X轴-水平从左到右
	/- Y轴-垂直从上到下
	/- Z轴-从里到外    
	* 景深--
	* perspective
		* 概念：肉眼到物体之间的距离
		* 不可继承
		* 设置于包裹器内，作用于后代元素（不是自己本身）
		*   * 值越大 离我们越远；看见的东西也会多一点；灭点越近
			* 值越小 离我们越近；看见的东西越少；灭点越远
	* 灭点
		* 立体图形各条边的延伸线的相交点 
	* perspective-origin
		* 设置在父元素 -对后代元素起作用
		* （x y z） 三个轴的基点调整
		* 景深基点默认值为盒模型的50%,默认的参照物是border-box
	* transform：prespective（depth）
		* 默认值为none
		* 设置于要体现效果的元素身上
		* 必须防止在transform内的首位，否则没效果
		* 避免 叠加景深
	* transform-style--具有层次感
		* -preserve-3d -- 子元素在3D平面呈现
		* -flat（默认） -- 子元素在2D平面显示
		* 营造3d舞台
		* 不继承
		* 作用于子元素 --so放置在父级身上
	* backface-visibility
		* 设置是否现实元素的背面，默认显示
		* hidden/visible
	* 3D缩放
		* transform：scaleZ（）
			* 需要和translatez(length)配合
		* transform：scale3d（X，Y，Z）
	* 3D旋转
		* transform：rotateX
		* rotateY
		* rotateZ --默认
		* rotate3d（x,y,z）
	* 3D平移
		* translateZ（) 不能为百分比（无意义）
		* translateX（）/Y（）可以为百分比
	2.动画
	* animation-name  
		* 动画的名 由@keyframes定义
	* animation-duration  
		* 动画周期，必须有单位，不为负值 （动画内）
	* animation-timing-function 
		* 作用于每一个关键帧周期 属性值同（transform-timing-function） 默认（ease）快到慢 （作用于动画内的属性-重复关键帧）
	* animation-delay 
		* 定义动画的延迟 （动画外）
	* animation-iteration-count 
		* 定义动画执行的次数 （只管理动画内的属性）
		* infinite循环
	* animation-direction：
		* 改变关键帧的执行方向
		* nomarl（正常 ft ft ft）reverse （tf tf tf） （动画的方向 反转的是关键帧和运动的形式）alternate （f->t->f->t->f） alternate-reverse(t->f->t->f->t)
	* animation-fill-mode:
			* none:form之前状态存在，to之后状态存在
            forwards：from之前状态存在，to之后状态取消
            backwards：from之前状态取消，to之后状态存在
            both：from和to的状态都取消
		* 管理动画外的状态
	* animation-play-state：
		* 定义了动画的运行和暂停（paused）
	* 关键帧
		* @keyframes animationName{
			* from{cssstyle}
			* to{cssstyle}
		* }
		from ：0%   可以设置多个关键帧
		to：100%
# flex布局
* ！！！项目永远在主轴的正方向上排列
* 1.旧版 box
* why？好多移动端浏览器内核版本低，需要用到旧版布局
* display：-webkit-box
	* a：容器的布局方向 
		* 主轴：-webkit-box-orient
			* horizontal - 主轴为水平x轴
			* vertocal - 主轴为垂直y轴 
	* b： 容器的排列方向
		* 主轴的方向：-webkit-box-direction
			* normal - 左到右/上到下
			* reverse - 右到左/下到上
	* c ：富裕空间的管理 （不给项目分配富裕空间，只是确定富裕空间的位置）
		* 主轴 -webkit-box-pack 
		*（1）X轴为主轴
			* start 右边 
			* end 左边
			* center 左右两边
			* justify 项目之间
		*（2）Y轴为主轴
			* start 下边 
			* end 上边
			* center 上下两边
			* justify 项目之间 
		* 侧轴 -webkit-box-align
		* （1）侧轴是x轴
				start：在右边
				end：  在左边
				center：在两边
		* （2）侧轴是y轴
				start：在下边
				end：   在上边	
				center：在两边
	* d：弹性空间的管理
		* 将富裕空间按比例分配到各个项目上
		* -webkit-box-flex ：1
		* 默认值为0
		* 不可继承
* - 老版本的box通过两个属性四个属性值控制了主轴的位置和方向
* 2.新版  flex
* display：flex/ -webkit-flex
	* a：容器的布局方向/排列方向 
		* 主轴：flex-direction
			* row - 主轴为水平x轴
			* column - 主轴为垂直y轴		
			* row-reverse - x轴方向反
			* column-reverse - y轴方向反
	* b：富裕空间的管理（只是确定富裕空间的位置，不给项目分配） 
		* 主轴 flex-content
			* flex-start 在主轴的正方向
			* flex-end 在主轴的反方向
			* center 在两边
			* space-between 在项目之间
			* space-around 在项目两边
		* 侧轴 align-items
			* flex-start 在侧轴的正方向
			* flex-end 在侧轴的反方向
			* center 在两边
			* baseline 基线对齐
			* stretch 等高布局（项目没有高度）
	* c：弹性空间的管理
		* flex-grow
		* 按比例分
	* d：容器
		* flex-wrap 控制容器为单行/列还是多行/列，定义了侧轴的方向
			*  nowrap
			*  wrap
			*  wrap-reverse
		*  align-content 定义侧轴上的位置 一行的时候无效
			*  flex-start
			*  flex-end
			*  center
			*  space-around
			*  stretch
		* flex-flow 是属性flex-direction和flex-wrap的简写
			* row nowrap 默认值 不继承  
	* e：项目
		*  order 定义项目的布局顺序 
			*  值为number 
			*  order越大越后面
		* align-self  对项目的某一个进行设置对齐flex元素，并覆盖align-items的值 
		* flex-shrink
			* 指定flex元素的收缩因子 默认值为1 
		* flex-basis
			* 指定了flex元素在主轴方向上的出使大小
		默认值为0
		* flex 是flex-grow/flex-shrink/flex-basis的简写属性
	* F：：
		* flex-shrink（收缩） 默认值为1 只有在 flex-wrap:nowrap时才有作用
			* 计算收缩因子与基准值乘的总和
			* 计算收缩因数 
				* 收缩因数=（项目的收缩因子*项目基准值）/第一步计算总和  
			* 移除空间的计算
				* 移除空间= 项目收缩因数 x 负溢出的空间 
		* flex-grow/box-flex(拉伸)默认值为0
			*  可用空间 = (容器大小 - 所有相邻项目flex-basis的总和)
			*  可扩展空间 = (可用空间/所有相邻项目flex-grow的总和)
			*  每项伸缩大小 = (伸缩基准值 + (可扩展空间 x flex-grow值))
* - 新版本的flex通过一个属性四个属性值控制了主轴的位置和方向	





* flex-wrap: nowrap/wrap/wrap-reverse
* flex-flow:可写 flex方向和换行
* align-content：--控制纵轴的排列方式
* justify-content：--控制水平x轴的排列方式