#WEB API
基于json通信
基于POST方法

##web api 签名验证
###签名方法
调用 API 时需要对请求参数(除sign)进行签名验证，服务器会对该请求参数进行验证是否合法的。方法如下：
根据参数名称（除签名和图片文件）将所有请求参数按照字母先后顺序排序:key + value .... key + value
例如：将foo=1,bar=2,baz=3 排序为bar=2,baz=3,foo=1，参数名和参数值链接后，得到拼装字符串bar2baz3foo1

###系统暂时只支持MD5加密方式：
1. md5：将 appsecret 拼接到参数字符串头、尾进行md5加密，格式是：md5(appsecretkey1value1key2value2...appsecret)
2. 注：我们需要的是32位的字符串，字母全部小写（如果是md5出来的是大写字母，请转为小写），图片文件不用加入签名中测试。
3. 以下所有api均需要以下参数： appid， sign_method, sign

#新闻WEB API
##参数列表：
<table>
<tbody>
<tr><td><em>参数名</em></td><td><em>必填</em></td><td><em>描述</em></td><td><em>默认值</em></td></tr>
<tr><td>appid</td><td>yes</td><td>应用ID</td><td>您自己的appid</td></tr>
<tr><td>sign_method</td><td>yes</td><td>签名方式</td><td>目前支持MD5</td></tr>
<tr><td>sign_method</td><td>yes</td><td>签名方式</td><td>目前支持MD5</td></tr>
<tr><td>tag</td><td>yes</td><td>新闻分类</td><td>分类见下表</td></tr>
<tr><td>limit</td><td>yes</td><td>新闻分类</td><td>分类见下表</td></tr>
<tr><td>tag</td><td>yes</td><td>新闻分类</td><td>分类见下表</td></tr>
</tbody>
</table>
    appid, sign, sign_method, tag，limit，page

##获取新闻接口，前三条为置顶新闻
###接口地址： http://api.doubi.so/news/
###参数说明：
    tag：分类，page: 第几页，limit:每页最多显示的条数
####分类列表:
<table>
<tbody>
<tr><td><em>标签</em></td><td>推荐</td><td>热点</td><td>社会</td><td>娱乐</td><td>科技</td><td>汽车</td><td>时尚</td></tr>
<tr><td><em>字段</em></td><td>__all__</td><td>news_hot</td><td>news_society</td><td>news_entertainment</td><td>news_tech</td><td>news_car</td><td>news_fashion</td></tr>
</tbody>
</table>
###举例：
    http://api.doubi.so/news/
    tag=__all__
    page=1
    limit=20
    appid:10000
    sign_method:md5
    sign=*****************************


##获取美女图片接口
###接口地址： http://api.doubi.so/newsgirlpic/
###参数说明：
####获取全部美女图片分类: tag为空
####获取分类下的没图片: tag可选参数如下
    [
    // 视觉大片
    'photograph_gallery',
    // 八卦
    'gossip',
    // 服饰搭配
    'style',
    // 美体瘦身
    'body',
    // 彩妆美发
    'beauty',
    ]
###举例:
    http://api.soubi.so/newsgirlpic/
    tag=gossip
    page=1
    limt=10
    appid:10000
    sign_method:md5
    sign=*****************************



#小说WEB API
##参数列表：
    一级分类： first （男／女）
    二级分类： second
    小说ID: novelid
    章节ID: chapterid
    应用ID：appid
    签名ID：sign
    签名方法：sign_method

##获取小说分类接口
###接口地址： http://api.doubi.so/taglist/
###参数说明:
    获取全部小说分类: first 为空 second 为空 
    举例： 
    http://api.doubi.so/taglist/
appid:10000
sign_method:md5
sign=*****************************
###返回字段： 
first  second  name(二级分类名称)

##获取某分类下的小说列表接口
###接口地址： http://api.doubi.so/novellist/ 
###参数说明:
    根据分类列表获取的first  second查询
    举例：
    http://api.doubi.so/
    first=1
    second=1
    appid:10000
    sign_method:md5
    sign=*****************************
###返回字段：title， novelid, author, picture, introduction

##获取小说简介接口
###接口地址： http://api.doubi.so/novelintroduction/
###参数说明：
    根据分类下的小说列表中返回的novelid获取小说简介
    举例： 
    http://api.doubi.so/
    novelid=1
    appid:10000
    sign_method:md5
    sign=*****************************
####返回字典： 
    title, novelid, author, picture, introduction

##获取小说的章节列表接口
###接口地址： 
    http://api.doubi.so/novelchapter/
###参数说明：
    根据某分类下的小说列表中返回的novelid字段获取相应小说章节列表
    举例：
    http://api.doubi.so/
    novelid=10
    appid:10000
    sign_method:md5
    sign=*****************************
###返回字段：
    \title(小说标题), subtitle(小说章节标题)， chapterid(章节id), novelid , author, picture, introduction

##获取章节内容接口
###接口地址： 
    http://api.doubi.so/novelcontent/
###参数说明：
    根据小说章节列表中返回的chapterid 获取章节内容
    举例： 
    http://api.doubi.so/
    chapterid=10
    appid:10000
    sign_method:md5
    sign=*****************************
###返回字段：
title(小说标题), subtitle(小说章节标题), novelid(小说ID), content(内容)

##小说点击事件上传
###接口地址：
    http://api.doubi.so/novelclick/
###参数说明：
    上传用户小说点击数，用来记录小说总阅读数
