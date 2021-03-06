[TOC]

# 生成pcb和元件的摆放

## 生成pcb

1. 在上一章中，我们绘制完成原理图并且分配好了各种元件的封装，接下来我们就可以生成pcb了。点击EDA上面的 `设计` --> `原理图转pcb` 就可以将原理图转换成pcb了。

   ![image-20210820174051841](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210820174051841.png)

2. 当我们点击转pcb后，会弹窗询问是否要检查网络，这时候我们一定要检查网络，避免设计上的缺陷。可以看到我的检查网络出现了错误，`COL14`网络没有画完整，`ESC`键的row和col不在线上。像这种错误如果我们没有进行网络检查的话就会被忽略掉了。所以我们一定要记得网络检查，尽可能的排除错误，再进行pcb的生成。比如下面的错误，因为我加了阶梯键caps的兼容，检测到`caps0`键的焊盘不匹配。分配封装的时候注意空格一排的卫星轴一定要分配REVERS封装，也就是卫星轴钢丝在上，螺丝在下的封装，与其他卫星轴相反，避免钢丝在外面碰到壳子。

   ![image-20210820174617714](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210820174617714.png)

   ![image-20210820175429461](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210820175429461.png)

3. 当我们修正所有错误后，再次点击原理图转pcb，原理图就可以转换成pcb文件了。确认好单位是mm，就可以点应用了。

   ![image-20210820192144255](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210820192144255.png)

4. 应用后如下图，可以看到EDA自动分配的边框和所有元件的封装。这里的边框代表pcb未来的样子，元件封装，代表未来元件在pcb上的焊盘。我们需要最终将pcb做成我们想要的样子，所以要删除掉本来的边框，导入我们绘制的dxf格式的边框文件，来画出我们需要的pcb。

   ![image-20210820192246006](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210820192246006.png)

## PCB的成型

#### 导入文档层

1. 要想理解文档层的作用，首先要理解pcb的层级概念，可以查看这个链接对层级的介绍：https://www.pianshen.com/article/4282153746/

   看文章和网上的介绍有些复杂，为了更好的理解，既然我们用的是立创EDA，并且使用双层板子设计键盘的pcb。那简单介绍一下立创EDA的双层板层级，与其他的pcb绘制软件是同样的。

   	1. 顶层：pcb板上面的电路层
   	2. 底层：PCB板下面的电路层
   	3. 顶层丝印层：pcb上面写文字用作标注的层
   	4. 底层丝印层：pcb下面写文字用作标注的层
   	5. 顶层锡膏层：喷锡工艺和沉金工艺的焊盘层，帮助焊接使用，可以不用理解，一般用不到。
   	6. 底层锡膏层：与上同。
   	7. 顶层阻焊层：盖油层，绿色盖油的板子就是大绿板子，黑色就是黑板子，常见的还有白色、黄色、蓝色、红色、无色，还有嘉立创最近退出的紫色。开窗等词汇就是说某些部分不盖油，也与该层有关。
   	8. 底层阻焊层：同上。
   	9. 飞线层：用来指示pcb上焊盘的连线。与生产无关，但是在画pcb的时候具有重要的指示作用。
   	10. 边框层：也叫机械层，是用来限制pcb的外观的，长款多少，形状如何。都是通过这个层来完成的。
   	11. 文档层：用来辅助元件的摆放，指示元件摆放位置的。所以叫文档层。

   ![image-20210820192848328](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210820192848328.png)

2. 我们在第一章中制作了两个dxf的文件，带键位的是文档层文件，用于元件的定位，不带元件的是边框层文件，用于pcb边框的确定。接下来我们将导入文档层文件用来当作标识文档，以便摆放元件，再导入边框文件，文件--->导入--->DXF。然后删除默认自动生成的边框线。导入后，找一个与文档层共同的点，将边框层与文档层贴在一起。

   ![image-20210820194144162](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210820194144162.png)
   ![边框](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210821125432012-1629685249067.png)		![image-20210823102257782](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823102257782.png)
   
   ![image-20210823102642907](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823102642907.png)

#### 元件属性更改与摆放

我们将凌乱的元件分类。将键位分成一类，其他元件都是红色的，代表都是顶层的元件，分成一类，以便我们来批量操作。

##### 修改元件属性

1. 我们通过仔细观察发现轴座封装没有键值，只有编号，但是编号太不直观，所以我们全选按键封装，将所有按键的属性改成显示键值，如果嫌编号碍事，也可以隐藏掉。全选轴座封装，在右边的位置更改全体属性。

   ![image-20210823103837078](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823103837078.png)

   ![image-20210823103920145](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823103920145.png)

2. 然后我们发现其他的所有元件都在pcb顶层，我们全部更改为pcb的底层。全选封装，右边更改属性为底层。

   ![image-20210823104158065](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823104158065.png)

##### 摆放元件

###### 摆放轴座封装

1. 我们接下来摆放元件，首先选中typec口，按R键旋转，将c口摆放在我们留出的pcb突起位置。

   ![image-20210823105001754](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823105001754.png)

2. 然后我们从第一个键进行摆放轴座。`ctrl+F`搜索k0，也就是ESC键。找到后`ctrl+x`剪切，选中四个顶点中的任意一个作为参考点（这样会与文档层按键顶点进行吸附，比较好操作）。粘贴到我们已经画好的文档层`ESC`键内。但是我们发现焊盘出现冲突，有很多黄色的叉，我们再次选中此键封装，按R键将其旋转180度，因为热插拔轴座的焊盘面积较大，位置靠外，所以会与gh60尺寸的焊盘发生冲突，所以C口附近的两个轴需做成倒装，解决这个问题。带来的副作用是会导致在用厂高键帽的时候，`ESC`和`1！`两个按键触底有些肉，尤其在用jtk和菜菜的厂高键帽时候尤为明显。

   ![image-20210823105521176](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823105521176.png)

3. 然后我们用同样的方法摆放其他的按键。除了C口左右的两个键需要旋转，其他键不需要旋转。当我们放置完一排以后，全选一整排，看一下中心点是否相同，如果中心点全部相同都在同一排上，就证明所有轴的轴心圆点都会落在同一排。无需担心是否整齐。下面放置剩余的轴座封装。

   ![image-20210823112933114](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823112933114.png)

4. 因为我们绘制的是多配列兼容的热插拔pcb，因为轴座的焊盘面积较大，还会遇到下面这种焊盘冲突的现象。遇到这种现象只需要点击冲突的焊盘，更改焊盘的长宽高度，缩小焊盘面积即可。

   ![image-20210823132408719](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823132408719.png)

   ![image-20210823132615577](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823132615577.png)

   ![image-20210823132636664](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823132636664.png)

   1. 在我们摆放完毕轴座封装后，发现键值的位置杂乱，我们接下来选择按键的键值，对其进行处理一下。选中一个名成右击`查找相似对象`，直接点查找。即可全选元件名成，右边编辑区可以改字体，全选后直接拖动其中一个到合适的位置，其他的也会跟随。

   ![image-20210823132922472](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823132922472.png)

   ![image-20210823133025964](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823133025964.png)

   ![image-20210823133230624](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823133230624.png)

5. 调整好所有键位后，我想到要加一个6u的空格给tina-a这种真hhkb配列使用，我们该怎么操作呢？首先我们来到原理图。复制一个空格出来，并且将其连线改名`space4`后分配6u封装。保存原理图，点击左上角的设计更新pcb，就可以看到我们添加的6u空格封装更新到pcb上面了。

   ![image-20210823160656885](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823160656885.png)

   ![image-20210823162004714](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823162004714.png)

   ![image-20210823162107387](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823162107387.png)

6. 加完空格后，用同样的方法还要增加空格右侧的1.5u的option键和1ucommand键。当我们摆放好所有轴座封装后将摆放好的轴座封装全选，然后右击锁定。避免在接下来的操作过程中不经意移动了按键封装导致pcb做出来轴孔不对其等错误发生。

   ![image-20210823171543913](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823171543913.png)

   ![image-20210823171609474](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823171609474.png)

###### 摆放主控电容电阻和二极管

1. 摆放轴座封装之后，我们来摆放主控，首先拖动主控到pcb上，找一个能放下的位置。没有孔没有焊盘的位置。这样方便我们摆放其他元件，我选择的是这里。

   ![image-20210823171034532](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823171034532.png)

2. 接下来我们摆放其他元件，首先我们先安排好主控周围和主控到C口的元件，按原理图和飞线层的飞线指示摆放。一般不会出错，这里要注意去耦电容和晶振要尽量靠近主控，去耦电容能分散开到主控周围，尽量分散开，不要串联，否则去耦效果会打折扣。

3. 摆放R1、R2 阻值为5.1k的电阻用来实现CtoC功能。还记得这张图吗，不记得回顾第三章。

   ![img](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\ae51f3deb48f8c54432b5c4f2a292df5e1fe7fd2)

4. 摆放完成剩余的元件，在空间允许的情况下，请发挥主观能动性，随心所欲，为所欲为的摆放就行了。摆放完成后我们再摆放二极管。

   ![image-20210823184125735](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823184125735.png)

5. 这里要注意，二极管是有方向性的。所以一定要看好飞线的方向。我直接图省事，把二极管和轴座的焊盘放在了一起，但是依然要布线。养成良好布线习惯。当我们摆放好所有的元件之后，pcb的雏形就出现了。可以点击上面的2d/3d按钮进行预览，我给轴座封装加了3d模型。

   ![image-20210823184456345](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823184456345.png)

   ![image-20210823192124292](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823192124292.png)

   ![image-20210823192201059](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823192201059.png)

   ![image-20210823192235540](md/半吊子画pcb教程---第四章 生成pcb和元件的摆放.assets\image-20210823192235540.png)

6. 下面我们就可以对pcb进行布线了。



