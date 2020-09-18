### 边框

## border-radius    圆角
border-radius: 20px;
## box-shadow       阴影
border-shadow: 10px 10px 10px #ccc;

## border-image





### 弹性盒子（Flex Box）

## 弹性盒子由弹性容器(Flex container)和弹性子元素(Flex item)组成。

## 弹性容器通过设置 display 属性的值为 flex 或 inline-flex将其定义为弹性容器。

## 弹性容器内包含了一个或多个弹性子元素。

## flex-direction
flex-direction 属性指定了弹性子元素在父容器中的位置。
语法
flex-direction: row | row-reverse | column | column-reverse

flex-direction的值有:

row：横向从左到右排列（左对齐），默认的排列方式。
row-reverse：反转横向排列（右对齐，从后往前排，最后一项排在最前面。
column：纵向排列。
column-reverse：反转纵向排列，从后往前排，最后一项排在最上面。

## justify-content 属性
内容对齐（justify-content）属性应用在弹性容器上，把弹性项沿着弹性容器的主轴线（main axis）对齐。

justify-content 语法如下：

justify-content: flex-start | flex-end | center | space-between | space-around

各个值解析:

flex-start：
弹性项目向行头紧挨着填充。这个是默认值。第一个弹性项的main-start外边距边线被放置在该行的main-start边线，而后续弹性项依次平齐摆放。

flex-end：
弹性项目向行尾紧挨着填充。第一个弹性项的main-end外边距边线被放置在该行的main-end边线，而后续弹性项依次平齐摆放。

center：
弹性项目居中紧挨着填充。（如果剩余的自由空间是负的，则弹性项目将在两个方向上同时溢出）。

space-between：
弹性项目平均分布在该行上。如果剩余空间为负或者只有一个弹性项，则该值等同于flex-start。否则，第1个弹性项的外边距和行的main-start边线对齐，而最后1个弹性项的外边距和行的main-end边线对齐，然后剩余的弹性项分布在该行上，相邻项目的间隔相等。

space-around：
弹性项目平均分布在该行上，两边留有一半的间隔空间。如果剩余空间为负或者只有一个弹性项，则该值等同于center。否则，弹性项目沿该行分布，且彼此间隔相等（比如是20px），同时首尾两边和弹性容器之间留有一半的间隔（1/2*20px=10px）。

## align-items 属性
align-items 设置或检索弹性盒子元素在侧轴（纵轴）方向上的对齐方式。

语法
align-items: flex-start | flex-end | center | baseline | stretch

各个值解析:

flex-start：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴起始边界。
flex-end：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴结束边界。
center：弹性盒子元素在该行的侧轴（纵轴）上居中放置。（如果该行的尺寸小于弹性盒子元素的尺寸，则会向两个方向溢出相同的长度）。
baseline：如弹性盒子元素的行内轴与侧轴为同一条，则该值与'flex-start'等效。其它情况下，该值将参与基线对齐。
stretch：如果指定侧轴大小的属性值为'auto'，则其值会使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵照'min/max-width/height'属性的限制。

## flex-wrap 属性
flex-wrap 属性用于指定弹性盒子的子元素换行方式。

语法
flex-wrap: nowrap|wrap|wrap-reverse|initial|inherit;

各个值解析:

nowrap - 默认， 弹性容器为单行。该情况下弹性子项可能会溢出容器。
wrap - 弹性容器为多行。该情况下弹性子项溢出的部分会被放置到新行，子项内部会发生断行
wrap-reverse -反转 wrap 排列。

## align-content 属性
align-content 属性用于修改 flex-wrap 属性的行为。类似于 align-items, 但它不是设置弹性子元素的对齐，而是设置各个行的对齐。

语法
align-content: flex-start | flex-end | center | space-between | space-around | stretch
各个值解析:

stretch - 默认。各行将会伸展以占用剩余的空间。
flex-start - 各行向弹性盒容器的起始位置堆叠。
flex-end - 各行向弹性盒容器的结束位置堆叠。
center -各行向弹性盒容器的中间位置堆叠。
space-between -各行在弹性盒容器中平均分布。
space-around - 各行在弹性盒容器中平均分布，两端保留子元素与子元素之间间距大小的一半。





## display	        指定 HTML 元素盒子类型。
## flex-direction	指定了弹性容器中子元素的排列方式
## justify-content	设置弹性盒子元素在主轴（横轴）方向上的对齐方式。
## align-items	    设置弹性盒子元素在侧轴（纵轴）方向上的对齐方式。
## flex-wrap	    设置弹性盒子的子元素超出父容器时是否换行。
## align-content	修改 flex-wrap 属性的行为，类似 align-items, 但不是设置子元素对齐，而是设置行对齐
## flex-flow	    flex-direction 和 flex-wrap 的简写
## order	        设置弹性盒子的子元素排列顺序。
## align-self	    在弹性子元素上使用。覆盖容器的 align-items 属性。
## flex	            设置弹性盒子的子元素如何分配空间。



### translate()函数是css3的新特性.在不知道自身宽高的情况下，可以利用它来进行水平垂直居中

position: absolute;
top: 50%; 
left: 50%;  // 以左上角为原点，故不处于中心位置
transform: translate(-50%, -50%);  // 往上（x轴）,左（y轴）移动自身长宽的 50%，以使其居于中心位置

