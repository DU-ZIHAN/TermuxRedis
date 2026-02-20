# TermuxRedis
🚀小白也能一键跑起来的 Redis 配置 | Termux/Linux 通用 | 全中文注释 | 安全稳定


1.什么是 Redis？

Redis（REmote DIctionary Server）是一款开源、高性能、基于内存的键值（Key-Value）型 NoSQL 数据库。 它把数据优先存在内存里，读写速度极快，同时支持持久化到硬盘，兼顾速度与数据安全。

 

2.Redis 能用来做什么？

缓存：加速网站、接口、小程序响应速度​

会话存储：登录状态、用户信息快速读写​

消息队列：简单任务队列、异步处理​

排行榜/计数器：点赞、浏览量、积分排名​

分布式锁：多服务/多设备互斥控制​

小型数据库：直接当轻量持久化库使用

 

3.Redis 核心特点

极快：内存操作，每秒可处理百万级请求​

多数据结构：支持字符串、哈希、列表、集合、有序集合等​

持久化：RDB 快照 + AOF 日志，断电不丢数据​

可跨设备访问：支持局域网/服务器远程连接​

轻量稳定：资源占用小，适合服务器、手机 Termux 运行

 

4.本仓库提供什么？

一份带完整中文注释、可直接在 Termux/ZeroTermux(移动端) / Linux 上使用的 Redis 配置模板：

每一行配置都有翻译 + 作用说明​

开启密码认证 + AOF+RDB 双持久化​

限制内存、自动淘汰、日志规范、安全稳定​

适合新手从零搭建 Redis 服务

 

5.适合谁用？

刚学 Redis、看不懂英文配置的新手​

用 Termux 在手机搭服务器的玩家​

做小项目、测试环境的开发者​

需要一份安全、规范、可直接运行的 Redis 模板的人

 

6.重要提醒

不要无脑照抄目录与密码，必须按自己设备路径修改​

外网开放时一定要设强密码​

根据设备内存调整部分参数

⚠︎⚠︎⚠︎再次重要提醒:

-千万千万千万不要无脑抄目录，除非您已创建或者愿意创建

-千万不要把参数原封不动的抄上去，需要拿到AI修改一下，保证运行更稳定。

-需要拥有Redis运行载体(Redis-Server,Redis-CLI)

7.我的配置(密码是只是占位符，需自行修改)

bind 0.0.0.0
port 6379
daemonize yes
loglevel notice
logfile /data/data/com.termux/files/home/Xinhao/Server/logs/redis.log
dir /data/data/com.termux/files/home/Xinhao/Server/data/redis
protected-mode no
requirepass Redisserver-start@myredis
appendonly yes
appendfsync everysec
maxmemory 256mb
maxmemory-policy allkeys-lru
maxclients 500
timeout 300
databases 16
tcp-keepalive 60
save 900 1
save 300 10
save 60 100


-再警告一遍，这是我的配置，别直接抄！！！特别是密码和日志,数据目录

8.给你们的配置模板(主要内容，你们移动端Termux配置只需要跟着他，一些参数建议自己改一下)

bind 0.0.0.0

翻译：允许所有 IP 地址连接 Redis​

意思：局域网、本机、其他设备都能连。

 

port 6379

翻译：Redis 服务端口设为 6379​

意思：默认端口。

 

daemonize yes

翻译：以守护进程（后台）方式运行​

意思：关闭终端，Redis 还在后台跑。

 

loglevel notice

翻译：日志级别为 notice​

意思：只记录重要信息，不刷大量日志。

 

logfile /data/data/com.termux/files/home/Xinhao/Server/logs/redis.log

翻译：日志文件保存到指定路径​

意思：所有运行日志写在这个文件里。

-注意:这是我的目录，请替换为您的目录

dir /data/data/com.termux/files/home/Xinhao/Server/data/redis

翻译：数据文件存放目录​

意思：RDB、AOF 都存在这里。

-注意:这个是我的目录，请更换为您的目录

protected-mode no

翻译：关闭保护模式​

意思：允许外部设备连接，不限制只能本机访问。

 

requirepass 你设置的强密码

翻译：设置 Redis 连接密码​

意思：连接必须先认证密码，否则无法操作。

 

appendonly yes

翻译：开启 AOF 持久化​

意思：把每一条写操作记录到文件，重启可恢复。

 

appendfsync everysec

翻译：每秒同步一次 AOF 文件到磁盘​

意思：性能与数据安全平衡。

 

maxmemory 256mb

翻译：最大使用内存限制为 256MB​

意思：超过就开始删键。

 

maxmemory-policy allkeys-lru

翻译：内存满时，删除最久未使用的键​

意思：保证服务不崩，自动清理。

 

maxclients 500

翻译：最大同时连接数 500​

意思：最多允许 500 个客户端连进来。

 

timeout 300

翻译：客户端空闲 300 秒（5分钟）自动断开​

意思：释放无用连接。

 

databases 16

翻译：共创建 16 个数据库​

意思：默认 0~15 号库。

 

tcp-keepalive 60

翻译：TCP 心跳检测 60 秒一次​

意思：及时发现死连接。

 

save 900 1

翻译：900 秒内至少 1 次修改，就生成 RDB 快照

save 300 10

翻译：300 秒内至少 10 次修改，就生成 RDB 快照

save 60 100

翻译：60 秒内至少 100 次修改，就生成 RDB 快照

AOF + RDB 双持久化​

带密码、外网可连、安全够用​

内存限制、自动淘汰、稳定​

日志、数据目录规范​

日志无任何报错，运行完全正常

-新手注意:根据实际硬件和需求调整maxmemory等参数，千万不要照抄，除非你愿意自己一个一个创建目录。

9.工具安装(要是没装的话，不看绝对倒霉)

-安装主程序(Redis): Linux环境(包括模拟器):apt install -y redis

10.启动,连接,停止服务命令

-启动服务命令:redis-server /你的路径/redis.conf

-连接服务命令(0.0.0.0,要是不是0.0.0.0的话，就没有别人连接你的):

你连接你的:redis-cli -h 127.0.0.1 -p 6379 -a 密码(如果你有,没有不输-a)

别人连接你的:redis-cli -h 你手机的IP -p 6379 -a 密码(如果你有,没有不输-a)

关闭服务命令:pkill -f redis-server

11.免责声明

-本仓库提供的配置请先经过AI确认是否彻底有效

-如果无效本仓库作者不负责

12.反馈建议

-如果无效，本仓库接受反馈

-反馈后我们会及时改正

反馈邮箱:duzihan111@163.com
