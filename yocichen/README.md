> Refs: [yocichen's blog](https://www.cnblogs.com/yocichen/p/11847478.html)

* craw_src.py 是从一个豆瓣书籍标签（[小说](https://book.douban.com/tag/%E5%B0%8F%E8%AF%B4)）爬取所有的书单的豆瓣地址([活着](https://book.douban.com/subject/4913064/))。
* craw_info.py 根据craw_src.py 获得的src地址，爬取具体的书籍名称、评分、摘要、图片地址等，爬取的效果些许地方不妥，会出现NULL情况。 **注意**：原博客中需要将`read_booksrc_get_info`里（868，row+1） -> (1,row+1)

* 主要技术点 模拟浏览器`header`拉取html代码`get_one_page`函数，使用`beautiful` & `re` 抽取需要的文本或者链接。
