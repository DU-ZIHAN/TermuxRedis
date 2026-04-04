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
 pidfile /data/data/com.termux/files/home/Xinhao/Server/run/Redis/Redis.pid
 tcp-backlog 511
 daemonize yes
 loglevel notice
 logfile /data/data/com.termux/files/home/Xinhao/Server/logs/Redis/Redis.log
 dir /data/data/com.termux/files/home/Xinhao/Server/data/redis
 protected-mode no
 requirepass Redisserver-start@myredis
 appendonly yes
 appendfsync everysec
 aof-rewrite-incremental-fsync yes
 aof-load-truncated yes
 aof-use-rdb-preamble yes
 appendfilename "appendonly.aof"
 maxmemory 256mb
 maxmemory-policy allkeys-lru
 maxclients 500
 timeout 300
 databases 16
 tcp-keepalive 60
 save 86400 100
 save 3600 10
 save 600 1

-再警告一遍，这是我的配置，别直接抄！！！特别是密码和日志,数据目录

8.给你们的配置模板(主要内容，你们移动端Termux配置只需要跟着他，一些参数建议自己改一下)

# ==============================================
# Redis 配置模板 for Termux / Linux
# 适用：个人本地服务、局域网部署
# 警告：以下配置为演示模板，部署前务必修改！
# 1. 目录警告：请自行更改目录，如果你执意要继续用我的目录，请先创建，否则服务运行不起来。
# 2. 密码警告：该密码为示例密码，请自行更改密码。
# 3. 内存警告：根据你手机硬件自行调整 maxmemory
# ==============================================

# 监听所有网卡（局域网/本机均可访问）
bind 0.0.0.0

# Redis 默认端口
port 6379

# 进程 PID 文件路径（目录需提前创建）
pidfile /data/data/com.termux/files/home/Xinhao/Server/run/Redis/Redis.pid

# 连接队列长度，高并发场景有用
tcp-backlog 511

# 后台守护进程运行（关闭终端仍保持服务）
daemonize yes

# 日志级别（notice 适合生产环境）
loglevel notice

# 日志存放路径（目录需提前创建）
logfile /data/data/com.termux/files/home/Xinhao/Server/logs/Redis/Redis.log

# Redis 数据工作目录（持久化文件会存在这里）
dir /data/data/com.termux/files/home/Xinhao/Server/data/redis

# 关闭保护模式，允许局域网连接（配合密码使用）
protected-mode no

# 连接密码（重要！请务必修改）
requirepass Redisserver-start@myredis

# ==============================================
# 持久化配置（数据安全）
# ==============================================

# 开启 AOF 持久化（每写操作都记录，数据最安全）
appendonly yes

# AOF 刷盘策略：每秒同步（性能与安全平衡）
appendfsync everysec

# AOF 重写时采用增量刷盘，降低阻塞
aof-rewrite-incremental-fsync yes

# AOF 文件被截断时仍允许加载（防止异常断电无法启动）
aof-load-truncated yes

# AOF 开头使用 RDB 格式，加载更快、体积更小
aof-use-rdb-preamble yes

# AOF 文件名
appendfilename "appendonly.aof"

# ==============================================
# 内存与淘汰策略（手机/低内存设备必备）
# ==============================================

# 最大使用内存（根据手机配置自行调整）
maxmemory 256mb

# 内存满后淘汰策略：删除最少使用的 key
maxmemory-policy allkeys-lru

# 最大同时连接数
maxclients 500

# 客户端空闲超时自动断开
timeout 300

# 数据库数量
databases 16

# TCP 长连接保活时间
tcp-keepalive 60

# ==============================================
# RDB 快照持久化（和 AOF 同时开启，双保险）
# ==============================================
# 900秒(15分钟) 至少1个key变化则保存
save 900 1
# 300秒(5分钟) 至少10个key变化则保存
save 300 10
# 60秒(1分钟) 至少10000个key变化则保存
save 60 10000


AOF + RDB 双持久化​

带密码、外网可连、安全够用​

内存限制、自动淘汰、稳定​

日志、数据目录规范​

日志无任何报错，运行完全正常

-新手注意:根据实际硬件和需求调整maxmemory等参数，千万不要照抄，除非你愿意自己一个一个创建目录。

9.自动脚本
仓库不提供自动脚本。

10.工具安装(要是没装的话，不看绝对倒霉)

-安装主程序(Redis): Linux环境(包括模拟器):apt install -y redis

11.启动,连接,停止服务命令

-启动服务命令:redis-server /你的路径/redis.conf

-连接服务命令(0.0.0.0,要是不是0.0.0.0的话，就没有别人连接你的):

你连接你的:redis-cli -h 127.0.0.1 -p 6379 -a 密码(如果你有,没有不输-a)

别人连接你的:redis-cli -h 你手机的IP -p 6379 -a 密码(如果你有,没有不输-a)

关闭服务命令:pkill -f redis-server

12.免责声明

-本仓库提供的配置请先经过AI确认是否彻底有效

-如果无效本仓库作者不负责

13.版权声明

-本仓库遵循GPL协议(https://www.gnu.org/licenses/gpl-3.0.html)
-但请勿盗用，闭源商用。

14.反馈建议

-如果无效，本仓库接受反馈

-反馈后我们会及时改正

反馈邮箱:duzihan111@163.com
