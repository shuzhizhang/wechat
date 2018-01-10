# 使用jieba、wordcloud制作简单词云

词云就是对文本中出现频率较高的“关键词”予以视觉上的突出，形成“关键词云层”或“关键词渲染”，从而过滤掉大量的文本信息，使浏览者只要一眼扫过文本就可以领略文本的主旨。

本文以《“健康中国2030”规划纲要》文档为例，在python中使用jieba分词和wordcloud词云制作工具，制作该文档的简单版词云，最终结果如下：

![](https://github.com/shuzhizhang/wechat/blob/master/ciyun/img/Figure.png)

点击文尾的“阅读原文”跳转至github仓库，仓库里中有《规划纲要》文档text.md和本文操作截图ciyun.jpg。建议大家在pc端参考该仓库中的资料进行操作。

#### 一、安装python环境
推荐Anaconda，见[Anaconda安装](https://mp.weixin.qq.com/s/-VGHDUw7bYS8gmunge1U-w)。  
安装完成，在开始菜单见下图。

![](https://github.com/shuzhizhang/wechat/blob/master/ciyun/img/anzhuang.jpg)


#### 二、安装jieba和wordcloud

点击打开安装好的Anaconda命名提示符（Anaconda Prompt）。

##### 安装jieba
输入命令pip install jieba进行安装，安装成功提示如下。

![](https://github.com/shuzhizhang/wechat/blob/master/ciyun/img/jieba.jpg)

如果不能成功安装，详见jieba的github中安装部分：  
https://github.com/fxsjy/jieba


##### 安装wordcloud
输入命令pip install wordcloud进行安装，安装成功提示如下。

![](https://github.com/shuzhizhang/wechat/blob/master/ciyun/img/wordcloud.jpg)

安装过程中，可能会提示缺少基库块，请按照提示下载安装相应的基础库。  
笔者在安装过程中，要求安装了两个基础库：.NET Framework 4.5.1和Microsoft Visual C++ Build Tools，自行下载安装后再次pip install wordcloud后才安装成功。  
如果不能成功安装，详见wordcloud的github中安装部分：  
https://github.com/amueller/word_cloud

安装成功后，查看这两个工具的版本号，如下：

![](https://github.com/shuzhizhang/wechat/blob/master/ciyun/img/done.jpg)


#### 三、准备

将“C:\Windows\Fonts”下的微软雅黑字体文件复制到“E:\ciyun\fonts\”目录中，备用。  
将github仓库中的“规划纲要”文档text.md下载到“E:\ciyun\”目录中，备用。md文件为类txt文档，可以使用系统自带的记事本打开查看文档内容。

以下操作的截图，详见github仓库中的操作截图。

点击打开安装好的Anaconda命名提示符（Anaconda Prompt），执行ipython命令打开python操作环境。  

把jieba和wordcloud以及plt绘图工具导入备用：  
In [1]: import jieba as jb  
In [2]: from wordcloud import WordCloud  
In [3]: import matplotlib.pyplot as plt  



#### 四、对《规划纲要》文档预处理

读入《规划纲要》文档:  
In [4]: text = open('E:\\ciyun\\text.md', encoding='utf-8').read()  
可以输入text后回车，查看读入的文档内容， 限于篇幅，截图中没有进行该操作，大家可自行操作。 

发现文档中有大量的“\n\n”、“#”、“\u3000”等无意义的内容，  
去掉“\u3000”；去掉连续换行符，去掉“#”：  
In [5]: text = text.replace('\u3000','')  
In [6]: text = text.replace('\n\n','\n')  
In [7]: text = text.replace('#','')

可以输入text后回车查看处理后的文档内容。

#### 五、使用jieba对文档进行分词
使用jieba的cut函数对文档进行切分，使用“/”符号把分词连起来，备用：  
In [8]: seg_list = jb.cut(text)  
In [9]: text_cut = '/'.join(seg_list)  

此时，可以输入text_cut后回车，查看用“/”符号分割的文档字符。

#### 六、使用wordcloud制作词云
设置词云图片的背景色为白色，字体为微软雅黑，图片宽度和高度，以分词为内容生成词云：  
In [10]: wordcloud = WordCloud(background_color="white",font_path='E:\\fonts\\msyh.ttf',width=1000, height=860, margin=2).generate(text_cut)

把词云放置在绘图工作中；隐藏图片的坐标轴；显示绘图结果：  
In [11]: plt.imshow(wordcloud);plt.axis("off");plt.show()

点击绘图结果中的保存按钮，选择保存位置，保存词云图片。也可以自行调整相关的参数，查看不同的词云效果。

退出ipython：  
In [12]: exit  

再次exit退出Anaconda命名提示符（Anaconda Prompt）。


#### 七、注意
##### 执行命令
如果执行命令中出现错误，请仔细检查命令行的书写是否正确，  
拼写实在有困难，可以复制命令，粘贴到命名提示符（Anaconda Prompt）中执行，  
复制执行命令时的错误，很可能是引号的问题。请在英文输入法下替换命令中的引号。

##### 优化分词  
jieba对文档的分词不一定完美，可参考jieba文档进一步完善分词过程，使关键字的提取更加完善，  
wordcloud有更多的制作选项，比如，以一个造型为框架的词云，详见wordcloud文档。

##### 工具的“封装“特性  
现代的工具，大多有封装的特性，  
知道微波炉操作面板上几个按钮的意义，不用知道微波炉的内部构造，就能较好的使用微波炉，  
用手机VS造手机，考驾照VS汽车制造，  
也就是说，“编程”能力也分为不同的能力，对大部分人来说，类似于胶水，把工具拼接起来，也是“编程”能力。
