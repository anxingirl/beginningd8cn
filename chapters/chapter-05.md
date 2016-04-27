#第5章 内容类型

当你问Drupal最强大的特性是什么? 许多人都会说是因为它可以可以自定义内容类型。 什么是内容类型呢? 你可以理解为内容模板,你可以选择Drupal 内核中已经有的内容类型比如"Basic page" 或者 "Article" 来满足你网站的所有需要 。但是，很多时候你需要是使用自定义内容类型来控制用户输入更多信息,或者是显示更多内容。 这一个章节,将会从零开始向你展示自定义一个内容类型是多么的简单 ! 请找一个舒适的环境，带上你自己,开始我们新的旅程吧 !


<!-- more -->


## 5.1 基础页面和文章内容类型

这是Drupal核心自有的两个内容类型, 当你使用基础页面创建一个内容时,你会发现它包含了两个字段:标题 和 内容。
一个作者可以很容易的通过输入内容和标题(红色星号标注表示必填字段)创建一个基础页面。 并且,内容页面很灵活,它支持一般著作所需的任何类型:

* 使用HTML渲染一整本书 (包含标题,表格,CSS等)
* 插入一个图片
* 写一个句子 


文章内容类型和基本页面内容类型很像,它还支持通过独立的元素提交图片,比如文章中经常使用的banner(并非嵌入到内容区域内),还有一些用来对文章进行归类的标签（第四章详细解释如何对内容进行分类）.
 
 和基本页面类似,文章类型可以用来创建任何主题的文章,内容区域(body)依然支持多种格式的文本。
 
看起来基础页面和文章类型基本很完美的解决日常的需求,但是仔细想想,比如下面这些案列:

* 需要在作者提交内容之前补充更多信息: 比如事情发生的时间,地点甚至是Google Map的链接
* 具备基于某个字段的计算能力
* 具备按照某个字段排序的能力
* 具备依据某个字段的值过滤或者限制某些内容项显示的能力
* 具备控制内容项在页面中如何显示的能力:比如你要按照标题,作者,ISBN,价格,书籍描述的顺序显示一本书的详细内容。


假如你只能通过基础页面和文章发布你的所有内容，并且还要赋予它排序,过滤,计算,声明必须字段,甚至结构化输入的能力,想想该有多困难啊! 很幸运,Drupal提供了自定义内容类型的能力让以上这些功能容易很多,并且还有其他你想不到的功能等待你的发现 。

## 5.2 定义一个自定义内容类型

一个自定义的内容类型可以被你或者Drupal管理者基于基础页面和文章内容类型定义,并且由Drupal 8核心底层支持。

为了演示创建自定义内容类型的灵活性,我们先创建一个捕获行事历(即将发生事件的信息)的内容类型。 也许是一场音乐会、一场戏、一堂课、一个游戏或者是其他提前规划的事情。

  当需要用户输入事件的详细信息的时候,你也许希望包含以下细节:

* 名字或者标题
* 开始的时间
* 结束的时间
* 事件发生的地点
* 相关描述
* 需要的花费

等会你会发现,Drupal给我们提供了非常简单的创建管理自定义内容类型的界面。
并且,当你创建了自定义内容类型之后,拥有相关权限的用户就能针对此内容类型增删改查。


## 5.3 创建自定义内容类型


### 5.3.1 基本内容填写和设定
创建自定义内容类型需要两个步骤:

1. 列出所需信息的内容类型
2. 使用Drupal管理页面创建自定义内容类型

这里我们按照上一小姐列出内容创建一个内容类型。

首先,点击管理页面的结构菜单,在其子菜单中点击内容类型链接 (/Structure/Content types）

![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/content_type.png)
Figure 5-1 Structure page with "Content types" link


"内容类型"页面列出了所有的已存在的内容类型,在这里有Drupal核心中的文章和基础页面。点击"添加内容类型"(Add content type) 按钮,添加我们的事件类型。

![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/add_content_type.png)
Figure 5-2, 内容类型列表


当你点击"添加内容类型"(Add content type)按钮后,显示出一表单(如图Figure 5-3) ,它有一个标题(Name)属性,一个描述(description)属性,一个标题的标签(label)属性,还有其他一些我们稍后介绍的配置选项

![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/add_content_type_detail.png)

Figure 5-3 内容类型创建表单

这些表单项什么意思或者怎么填写呢? 请看下面的介绍:

* 填写内容类型的标题(Name): 在这里我们填入"Event",注意我们应该遵循Name 表单项下面的指导信息。
* 提供该内容类型的描述信息 : 比如"本内容类型用来记录将要发生的事"
* 将 “标题的标签”(Title field label) 从 标题(Title)改成"事件的名称"(Event title),这能够给使用此模板创作的作者更加友好的提醒。
* 把"在提交之前预览"(Preview before submitting) 设置为可选
* 提供清晰的提交向导 : 这个一个可选的值, 并非一定要填写! 在这里，我们可以填写"请在提交之前填写完整所有必填的项目",在创建内容类型的时候你可以选择使用或者忽视这个字段。

还有其他可选的设置选项需要你仔细思考。
### 5.3.2 发布设定
首先是左边菜单栏的发布选项(Publish options) 你可以点击它(Figure 5-4)
![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/publish_options.png)
Figure 5-4 发布选项
</br>
</br>

你可以按照自己的意愿设置你是否想自动发布(在网站中可见)，是否自动显示在网站的首页上。 对于我们事件类型,我们计划让他保存的时候自动发布,但是不想它们自动发布在首页上。因此,我们取消选择"Promoted to front page"单选框,我们也可以设置是否固定在列表的上方(如果有多个内容类型,此类型总是在上方)。此外,我们想在作者更新事件内容的时候创建一个新的版本(通常是一个好想法,但是取决于你是否在之后的某些时候想看到曾经你改动过什么,或者是当目前的版本错误的时候恢复到之前的版本)。 对于我们的事件类型,我们选择"创建新版本"(Create new revision)。

### 5.3.3 显示设定
接下来是显示设定。 点击左侧的“显示设定”（Display settings）选项卡,
你将会看到相关可用的配置(Figure 5-5),你可以设定Drupal 是否显示作者的名字,和创作时间.在这里我们并不想显示作者和时间,所以我们取消选择这个单选框。你当然可以更具自己的内容类型做出对应的选择。

![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/display_settings.png)
Figure 5-5 显示设定

### 5.3.4 菜单设定
最后一个选择是关于菜单相关的设定。 点击“菜单设定(Menu setting)” 选项卡可以显示出相关的设定. “可用的菜单”展示出这个内容类型可以展示在哪些菜单的下面。 在内容创建期间,作者可以选择是否可被被选择的菜单按钮链接到。这里按照图 **Figure 5-6**,只有“主导航栏(Main navigation)”是可以被选的。你可以取消选择主导航栏，也可以选择不止一个允许后续作者选择菜单。 “默认父菜单 (Default parent item)” 允许你设置哪一个菜单将会在用户创建与此类型对应的内容时被默认选择。

![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/menu_setting.png)
**Figure 5-6** 菜单设定

然后,我们点击“保存并且管理字段(Save and manage fields)”按钮。

Drupal 现在显示“管理字段(Manage field)”页面 (Figure 5-7)

</br>
</br>
![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/manage_field.png)

Figure 5-7. 事件类型的管理字段页面
</br>


## 5.4 自定义内容类型



到这里我们就可以根据我们的事件类型创建事件,但是,事件类型只包含两个字段,分别是事件标题和事件内容. 而我们需要事件描述，开始事件，结束事件，事件地址,座位类型,会场是否提供协助,会议类型,是否提供可被下载的文件(爬虫或者访问者)。 

### 5.4.1 添加事件描述字段
你可以在 Figure 5-8 中看到，Drupal自动创建了内容字段,用于做事件描述.
![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/changing_label.png)


我们通过修改内容字段的标签----“内容(Body)”改为"事件描述(Event description)"，这样我们创建了一个更好的类型提示符,点击内容(body)字段的编辑按钮,修改其标签(Label)字段---“内容(body)”改为"事件描述(Event descripttion)" （见Figure 5-8）,然后表单底部的点击“保存设置(Save settings)”按钮。

保存更新后的内容标签后,Drupal将会跳转到修改标签后的"管理字段（manage fields）"页面,见Figure 5-9

![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/revised_field.png)


### 5.4.2 添加开始时间字段
	
点击 “添加字段(Add field)”按钮,下一步是选择添加什么类型的字段,或者是添加已经存在的字段到这个内容类型 . 一个之前创建的字段可以在新创建的内容类型中重用,而不用重新创建改字段,相当于我们可以在列表中选择已经存在的字段。

![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/add_field.png)


点击时间类型后,你讲会被提示输入新属性的标签,这个便签将会备用来,说明这个字段具体代表的意义。 因为我们将要创建事件的开始事件,因此我们在标签栏中输入"开始事件(Start Data)" 然后点击 "保存并且继续（Save and continue）" 按钮。

接下来是设置时间字段为是日期和时间或者是仅有日期,还有该字段允许的数量 (见Figure 5-11)。 通常一个事件往往只对应一个时间,因此我们为“日期类型(Data type)”设置“日期和时间(Date and time)”,将“允许的值数量(Allowed number of values)”选项设置为“限制(Limited)”并且"1",因为我们的事件仅仅发生一次。 你会发现"允许的值数量"配置选项将会出现在每一次的字段创建中,你也许有场景需要用户针对一个字段有创建多个值得能力。比如，将来相同的时间发生多次. 那么我们可以设定"允许的值数量"为大于1的数,那么在我们创建该类型的内容时，将会产生对应数量的该字段的输入框. 如果你设置为"不限制",那么用户将会通过“添加(add another)”按钮随意创建任意个值。 因此在创建字段之前我们需要想清楚该字段具体什么作用,然后设置"允许的值数量",也许 1 并不是最好的解决方案。 点击"保存字段设置(Save field settings)"按钮继续下一步。

</br>

![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/setting_date.png)


</br>
</br>

Drupal 显示的下一个表单将会向你展示关于事件开始事件字段的更多配置细节,在这个表单中你将会做以下工作

* 修改标签的内容: 除非之前定义的内容错误的,否则你不用修改这里
* 在"Help text"字段中输入相关的帮助信息,这是一个提示用户输入更标准内容的好地方,比如你需要用户输入mm/dd/yyy格式的日期. 这是一个可选的字段
* 定义这个字段是否为必须字段。 一个必须字段将会用红色星行标注,Drupal 将会在用户保存前强制用户输入这个字段的值。因为我们的内容类型是关于事件,并且日期对于事件是非常重要的字段,因此我们将会选择"Required field"单选框。
* 定义是否为该字段设定一个默认值。 因为我们我们处理的将来的某个日期,提供一个默认的值没有任何作用。 当然对于某些字段是很有必要的,比如选择一个默认的座位。

</br>
</br>
![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/setting_date2.png)

</br>
</br>

点击"保存设置(Save settings)"按钮完成开始日期字段的配置,Drupal将会重新显示已经添加了开始日期字段(Start Date)的“管理字段(Manage field)”页面(见Figure 5-13)。

![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/manage_field2.png)


现在我们添加其他字段: 结束时间,事件描述,和事件地址. 按照之前的创建结束时间字段。当创建时间地址的时候,选择"文本(格式化,长)"  。当你完成后，你的列表将会如Figure 5-14

![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/event_List.png)



我们的事件类型已经准备好,为了测试新的类型,点击左上角的“返回站点(Back to site)"按钮并且点击"添加内容(Add Content)"链接,我们将会看到一个新的内容类型列表。

我们的事件类型显示在可用的内容类型列表,点击事件内容类型,可以看到新的内容创建页面。 这个页面显示了事件标题,事件描述,开始时间,结束时间,事件地址.


![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/new_event.png)


使用事件创建表单创建一个事件类型的样例,当你输入完所有的属性,点击"保存并发布(Save and publish)" , Drupal 将会渲染新的事件内容。如 Figure 5-16所示

![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/content_view.png)



## 5.5 其他字段类型

在我们的事件内容类型中,我们创建了一些方便用户输入日期和地点的字段。这里有一些除文本外的字段类型。

* 单选框(Radio buttons): 给用户提供一系列的选择,但是仅能选择其中一个。
* 多选框(Check boxes) : 允许选择多个值
* Select list : 
* 文件上传(File upload) : 提供上传并且将一个文件附属与一个内容
* 图片上传(Image upload): 上传并显示图片
* 文本区域(Text area) : 提供输入一个段落,它将会提供一个可以输入多行的文本框,text 字段只能提供单行的文本输入
* 数字字段(Numeric field) : 数字输入
* 实体字段(Entity reference fields) : 用于关联其他内容类型                                                                           
* Term reference field : 关联分类相关字段(taxonomy terms)

这些字段类型全部来自于Drupal 8核心模块。 还有一些社区自定义的字段类型可以在贡献模块中找到,你可以在 www.drupal.org/project/modules 页面,通过在"Module categories"过滤选择 fields,然后开始搜索,你将会找到很多扩展模块
	
### 5.5.1 单选按钮与复选框(Radio Buttons & Check box)


![radio_buttons](http://work.beiweng.org/d/file/drupal/chapter5/2016-04-08/03effcb355bd3630bf41f53d5da21197.png)

图5-17。添加列表字段


{%asset_img radio_button.png radio_button%}
1. 如图5-17,首先我们添加list
2. 如图5-18,枚举列表的值
	* 格式问题:使用 key | label 这样的格式枚举每一个值,其中被选中的key将会被存储到数据库中,而label 将能够被用户看到
	* 当 "允许的值数量(Allowed number of values)" 等于1时,表现为单选框,当大于1时表现为复选框


### 5.5.2 下拉列表(Select List)

与单选复选框对比
相同之处: 添加列表可选值的方式一样
不同之处: 控件类型之前的为"Check boxes/radio buttons",而这里我们选择默认的"Select list"

这里显示的效果如下 

![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/select_list.png)


### 5.5.3 文件上传

功能: 提供用户一个显示文件浏览器的按钮,供用户选择文件。

配置: 

* 文件是否可见
* 文件默认显示,还是由用户手动显示
* 文件上传的位置
* 限制的数量

![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/file_upload.png)



高级配置

*  终点是允许的文件类型 : txt,doc,docx,ppt,pptx,pdf 
	* 填写的时候用空格隔开就好  
*  文件大小限制
*  是否为文件添加描述文件

![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/file_configure_more.png)



### 5.5.4 文本区域

功能 : 提供多行的富文本输入
配置 : 

* Full   HTML : 允许用户输入WYSIWYG的全部功能 。
* Basic  HTML : 提供基本的功能


![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/text_area.png)



### 5.5.5 数字字段

定义 : 本质上是只能接受数字的文本字段(text field)

### 5.5.6 格式化自定义内容的输入

操作指导 :

* 拖动左边箭头可以改变显示的顺序
* 每一个字段都有各自的显示配置

![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/manage_display.png)



### 5.5.7 格式化自定义内容的输出

操作指导

* 拖动左边箭头改变显示的顺序
* 配置LABEL显示位置
	* Above: 	在对应字段的上边
	* Inline: 	显示在控件的左边
	* Hidden:	隐藏
* 文本框配置 : 
	*  Default : 按照创建时候指定的格式显示
	*  摘要和裁剪 : 如果包含摘要就显示摘要 , 否则裁剪指定的长度
	*  裁剪 : 裁剪指定的长度,如果内容比指定的长度长,就显示"阅读更多(Read More)" 按钮;
	* 隐藏 : 隐藏这个字段的显示;
* 不同模式的显示 : 比如RSS,Search index 和Search result
	* 只要点击管理显示页面下面的 "自定义显示设置(Custom display settings)" 	
* 自定义显示模式: Structure/Display Modes/View modes 然后点击"添加显示模式(Add Display Mode)" ，然后从列表中选择你要显示的内容,一旦新的显示模式被创建,你就可以在管理显示页面去定义指定的输出。
 
 ![](http://llwoll.github.io/2016/04/20/Drupal-%E5%86%85%E5%AE%B9%E7%B1%BB%E5%9E%8B/manage_display2.png)



## 总结 

内容类型是Drupal杀手级应用之一,也是一个我们需要深入理解的重要的概念。以上我们介绍了内容类型的创建,使用,显示配置等。 除了自建内容类型我们也可以去Drupal Moudle所有页面找到第三方的模块比如Curtomers,Products,Departments,FAQs,Locations和Employees 。我们的模块之旅顺利完成,请抽空多多实践 ,毕竟孰能生巧,谢谢你的阅读 。 

















