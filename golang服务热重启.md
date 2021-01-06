

# 服务热重启

# 前言

心血来潮想给博客的http服务器加个热更新......

### 现有方案

热更新即服务器在不停止对外服务的前提下更新服务版本，服务器热更新一般有两种方案

- 接入层负载均衡，轮次更新
- 子进程监听父的端口（fd复用/端口复用），父进程在处理完请求后退出



### 服务热更新方案

第一种方案显然太复杂了，直接pass掉。

第二种方案实现方式有两种，fd复用和端口复用。在golang上，这两者实现有细微差别。如果要设置端口复用选项，golang并不能跨平台，这意味着使用者要陷入不同平台细节。而fd复用则不需要操心。



#### 验证方案

长链接，延迟10s再回包即可， 对比下直接暴力关闭和graceful 重启是否可以做到。



![image-20210106191905910](https://i.loli.net/2021/01/06/PKBfQAbCivExXml.png)



关闭链接：http://127.0.0.1:6333/shutdown

延迟10秒获取数据:http://127.0.0.1:6333/keepalive

优雅关闭：http://127.0.0.1:6333/webhook



经过验证，

- 当延迟获取时，如果直接shutdown，会返回



![image-20210106225542555](https://i.loli.net/2021/01/06/7YxAdBX8yipmzGb.png)

- 当使用graceful shutdown时，这个链接可以正常返回



### 代码地址

[git](https://github.com/Hank00AAA/light_blog)



#### 参考资料

[端口复用/地址复用区别](https://stackoverflow.com/questions/14388706/how-do-so-reuseaddr-and-so-reuseport-differ)

[golang graceful shutdown](https://leileiluoluo.com/posts/golang-shutdown-server-gracefully.html)

[golang graceful restart](http://kuangchanglang.com/golang/2017/04/27/golang-graceful-restart#references)

[如何让多个进程监听同一个端口](https://blog.csdn.net/L13763338360/article/details/106519027)



[go-endless热更新机制](https://studygolang.com/articles/25123?fr=sidebar)