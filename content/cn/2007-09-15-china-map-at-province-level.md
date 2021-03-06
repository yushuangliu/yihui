---
title: 终于搞定了中国分省市地图
date: '2007-09-15'
slug: china-map-at-province-level
---

今天费了半天劲，才一点点从GIS数据中把中国各省市的多边形“抠”出来。问题缘起于COS论坛上的这个帖子：<https://cosx.org/cn/topic/785>)，其实我后面的回复基本都跑题了，跑着跑着突然想起上学期上课的时候Prof. Peng, F曾经提到他当年是如何辛辛苦苦用作图软件去搞定地图图示的，我当时听着觉得不应该太困难，于是下课之后去告诉他用R可以很容易做出地图来，他当时问我是不是S-Plus（看来在他们脑子里还是S-Plus的名气大一点），我说类似但不完全一样，云云，最后他问能否作出重庆市的地图，我当时也没仔细注意这个问题，回来一看，`map("china")`还真没有重庆市。

之后我又花了很长时间找地理数据，其间联系过Victoria University of Wellington的Ray Brownrigg（**maps**和**mapdata**等包的作者），他说没有他也没有数据，告诉我要是我能搞到数据他也许可以给我一点Hints，不过我后来死活也没找到；于是开始打另一个注意，就是活生生去读一幅空白中国地图，从中获得线条（实际上是点）的坐标，然后再用坐标结合`plot()`把图形还原出来，后来发现这种方法做出来的地图太粗糙，而且面临最大的困难是很不容易把各省的坐标数据分开，这样对于地理信息展示是没有意义的。

今天再次找数据的时候，却鬼使神差地发现了国家基础地理信息中心的网站：<http://nfgis.nsdi.gov.cn>，里面可以免费下载GIS数据，我今天一眼就看见了国界与省界数据，各种数据都是一个zip压缩包，里面是`*.dbf`、`*.shp`和`*.shx`文件，这是`shapefile`的通用格式，R里面有**maptools**包可以读取（`read.shape()`函数），事实上作图的时候作出来是925个多边形（polygon），我到现在也没明白为什么会有那么多，不过顺利的是我已经知道哪34个多边形是我想要的了。下面是我的一个示例：

![中国分省市地图（借助R的maptools包实现）](https://db.yihui.org/imgur/EJMNL.png)

