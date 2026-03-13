CF-Blog搭建步骤
这是一个运行在cloudflare workers 上的博客程序(blog),使用 cloudflare KV作为数据库,无其他依赖.
兼容静态博客的速度,以及动态博客的灵活性,方便搭建不折腾.

项目地址:https://github.com/gdtool/cloudflare-workers-blog

主要特点
使用workers提供的KV作为数据库
使用cloudflare缓存html来降低KV的读写
所有html页面均为缓存,可达到静态博客的速度
使用KV作为数据库,可达到wordpress的灵活性
后台使用markdown语法,方便快捷
一键发布(页面重构+缓存清理)
承载能力
KV基本不存在瓶颈,因为使用了缓存,读写很少
唯一瓶颈是 workers的日访问量10w,大约能承受2万IP /日
文章数:1G存储空间,几万篇问题不大
部署步骤
创建workers 和KV
新建一个KV(名字随意)和一个workers,并绑定新建的KV到新建的workers,变量名称CFBLOG注意大写,绑定后是这效果
补充一下绑定步骤:workers->点击刚才新建的worker—>设置—>KV 命名空间绑定—>编辑变量—>变量名称:”CFBLOG”—>KV 命名空间:选择刚才的新建的KV

域名设置

添加一个域名DNS: 例如blog.gezhong.vip,IP随意,橙色云朵必须打开
域名绑定到workers:域名—> workers —>添加路由 https://blog.gezhong.vip/*
获取缓存API token:域名概述—>右下角,记录区域ID,以及获取一个清理缓存的 API 令牌,如图

粘贴源码中index.js内容到workers,根据需求修改参数

进入/admin进行设置 和发布文章
主题扩展性
可以用任意主题为参照,快速开发出新主题,默认主题在Iconic One基础上做的,回头补充专题

关于评论系统
由于本博客的缓存效果类似静态博客,评论依赖于第三方,这里推荐Valine,其他的我都对比过了,大家不用去看了
Valine的国际版申请
国内版需要绑定手机,+实名认证,今天有点忙,自己先试着申请一下,回头补充专题,今天时间匆促,坑比较多,大家谅解,回头一一填平

前端演示:https://blog.gezhong.vip
