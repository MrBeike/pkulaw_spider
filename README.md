## pkulaw_spider
## 爬取北大法宝网http://www.pkulaw.cn/Case/

1.打开网站，导航栏点击司法案例，看左边法律文档按案由分类，可以看见大概一共2kw左右的文书，实时与裁判文书网同步更新。

2.可以看见文书案例顶部有筛选条件，可以按照日期、法院等筛选。（本爬虫按照日期爬取所有的文书）

3.分析网站内容时发现，点击下一页按钮地址栏的链接并无变化，属于动态网页。

4.使用浏览器自带抓包工具或者fidder,点击下一页按钮，查看http请求。

5.发现记录由/Recod传送，该请求即是需要模拟的请求link，使用requests模拟浏览器直接请求数据库，带上浏览器headers和post data

6.分析得到的url，可以发现start和end参数，我们修改其为我们所需的日期范围。

7.pagesize我们设置为1000，太小页数过多，太大网页加载太慢。pageIndex为页号，其它参数默认。

8.模拟请求数据库，得到法律文档标题和id,第一步先save这些数据。

9.接下来我们来分析单个案件文本内容的请求url

10.点击任一个案件的链接，进入页面，分析http请求

11.我们发现_getFulltext请求的response为我们所需的内容（案件文本）,进入getFulltext，http://www.pkulaw.cn/case/FullText/_getFulltext发现并不
12 能返回什么[请求出处],此时查看该请求的headers和data:library=pfnl&gid=1970324872344528&loginSucc=0,只需将data显示的加入url中即可，即http://www.pkulaw.cn/case/FullText/_getFulltext?library=pfnl&gid=1970324872344528&loginSucc=0

13.通过上述url，爬取文书内容。

14.该爬虫是以前无聊写的一个练手程序，最近加了注释上传至github，一为了不使该程序浪费，二可供新手小白参考动态网页的分析，直接分析出数据源请求比
15 使用selenium+phantomJS效率高得多。三可为法律文档研究者提供语料来源借鉴。

16.本人小白，代码较乱，欢迎咨询：1049755192@qq.com

17.本项目玩具级别，不喜勿扰。