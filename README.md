# 爬取豆瓣豆列书单
豆列分页显示，不支持搜索，想着把一些信息爬出来，在网上找了一下找到了一个前辈写的好的[博文代码](https://www.cnblogs.com/yocichen/p/11847478.html)。

## 学习模仿
将前辈的文件都放在了`yocichen/`下面
> Refs: [yocichen's blog](https://www.cnblogs.com/yocichen/p/11847478.html)
* craw_src.py 是从一个豆瓣书籍标签（[小说](https://book.douban.com/tag/%E5%B0%8F%E8%AF%B4)）爬取所有的书单的豆瓣地址([活着](https://book.douban.com/subject/4913064/))。
* craw_info.py 根据craw_src.py 获得的src地址，爬取具体的书籍名称、评分、摘要、图片地址等，爬取的效果些许地方不妥，会出现NULL情况。 **注意**：原博客中需要将`read_booksrc_get_info`里（868，row+1） -> (1,row+1)

* 主要技术点 模拟浏览器`header`拉取html代码`get_one_page`函数，使用`beautiful` & `re` 抽取需要的文本或者链接。

* craw_info.py 可以用来爬取我们给定的src的信息，比如拿全部的ISBN号，再用于其他网站的导入。

## 实现概要
因为主要是想要一个索引功能，就将所有的信息导出了，突然发现ISBN没有导出~

* 网页地址规律
```
https://www.douban.com/doulist/135073077/?start=0&sort=time&playable=0&sub_type=
https://www.douban.com/doulist/135073077/?start=25&sort=time&playable=0&sub_type=
https://www.douban.com/doulist/135073077/?start=50&sort=time&playable=0&sub_type=
https://www.douban.com/doulist/135073077/?start=75&sort=time&playable=0&sub_type=

url = 'https://www.douban.com/doulist/135073077/?start='+str(page_index*25)+'&sort=time&playable=0&sub_type='
```
* 获取网页html`get_one_page`
* `get_info_dict_list`:使用`beautiful` & `re` 抽取需要的文本或者链接
* `def write_lable_excel` & `write_bookinfo_excel` 持久化存储

* TODO
  * 万一要拿ISBN呢？
  * 一些NULL的处理
  * 页码数量可以脚本获取

