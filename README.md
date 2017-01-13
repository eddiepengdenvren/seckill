# seckill
仿慕课网ssm商品高并发秒杀项目代码
Java高并发秒杀系统迷你版


项目涉及技术

BootStrap + jQuery
Spring MVC
Spring
MyBatis
MySQL + Redis
ProtoStuf
开发环境

windows10 + IntelliJ IDEA + Java8 + Tomcat8 + Maven + MySQL + Redis

项目简介

用户对系统开发的商品进行秒杀。 前端采用BootStrap框架开发前端交互页面 后端采用Spring MVC + Spring + MyBatis开发。 数据库MySQL + Redis缓存
# seckill
(1).商品表,用户表和抢购成功信息表

(2).列表页->详情页->倒计时->显示抢购地址->执行秒杀操作->返回结果

(3).倒计时用到jquery-countdown插件，用jquery-cookie保存用户电话号码

(4).高并发可能发生的地方: 详情页 获取系统时间 显示抢购地址 执行秒杀操作

(5).详情页优化：使用CDN,减少访问后端服务器的次数

(6).倒计时优化：单独获取服务器时间，避免倒计时每次都要访问服务器

(7).抢购地址接口优化：采用redis缓存，通过超时维护一致性.
redis缓存时需要序列化，JDK默认序列化效率低
解决办法：采用protostuff序列化

(8).秒杀操作优化：采用存储过程，把事务操作放到数据库端，减少事务锁时间。
在一个事务中，先insert操作插入抢购成功信息，然后在update更新库存。
如果重复秒杀，则insert失败回滚，无需update，减少update行级锁等待时间。
(抢购成功信息表中设置联合主键，即商品id+用户id。
一个用户可以抢购多个商品，但是一个用户对单个商品只能抢购一次。
当主键重复时，不会插入到抢购成功信息中，解决重复秒杀问题)




