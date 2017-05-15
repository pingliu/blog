# 一个故事告诉你什么是消息队列
> 摘要：本文属于原创，欢迎转载，转载请保留出处：[https://github.com/jasonGeng88/blog](https://github.com/jasonGeng88/blog)

## 案例
有一天，产品跑来说：“我们要做一个用户注册功能，需要在用户注册成功后给用户发一封成功邮件。”

小明（攻城狮）：“好，需求很明确了。” 不就提供一个注册接口，保存用户信息，同时发起邮件调用，待邮件发送成功后，返回用户操作成功。没一会功夫，代码就写完了。验证功能没问题后，就发布上线了。

线上正常运行了一段时间，产品匆匆地跑来说：“你做的功能不行啊，运营反馈注册操作响应太慢，已经有好多用户流失了。”

小明听得一身冷汗，赶紧回去改。他发现，原先的以单线程同步阻塞的方式进行邮件发送，确实存在问题。这次，他利用了 JAVA 多线程的特性，另起线程进行邮件发送，主线程直接返回保存结果。测试通过后，赶紧发布上线。小明心想，这下总没问题了吧。

没过多久，产品又跑来了，他说：“现在，注册操作响应是快多了。但是又有新的问题了，有用户反应，邮件收不到。能否在发送邮件时，保存一下发送的结果，对于发送失败的，进行补发。” 

小明一听，哎，又得熬夜加班了。产品看他一脸苦逼的样子，忙说：“邮件服务这块，别的团队都已经做好了，你不用再自己搞了，直接用他们的服务。”

小明赶紧去和邮件团队沟通，谁知他们的服务根本就不对外开放。这下小明可开始犯愁了，明知道有这么一个服务，可是偏偏又调用不了。

邮件团队的人说，“看你愁的，我给你提供了一个类似邮局信箱的东西，你往这信箱里写上你要发送的消息，以及我们约定的地址。之后你就不用再操心了，我们自然能从约定的地址中取得消息，进行邮件的相应操作。”

后来，小明才知道，这就是外界广为流传的消息队列（MQ）。你不用知道具体的服务在哪，如何调用。你要做的只是将该发送的消息，向你们约定好的地址进行发送，你的任务就完成了。对应的服务自然能监听到你发送的消息，进行后续的操作。这就是 MQ 最大的特点，将同步操作转为**异步处理**，将多服务共同操作转为职责单一的单服务操作，做到了**服务间的解耦**。

## 消息队列
### 名词解释
生产者
消费者
channal
点对点
发布订阅

### 特性

异步

分布式

可靠性

消息队列一般会把接收到的消息存储到本地硬盘上，当消息被处理完之后从可能将其删除，这样即使应用挂掉或者消息队列本身挂掉，消息也能够重新加载。

松耦合

消息队列可以实现系统直接的解耦，不同的服务和系统之间可以通过消息队列进行通信，而不用关心彼此的实现细节，只要定义好消息的格式就行。

## 总结
本文简单讲述了 MQ 的使用场景，以及主要的优势。这个案例活生生的告诉我们，任何技术的使用，都是由业务驱动的，说白了，都是被逼的。

之后会向大家讲述 JAVA 下的消息服务（JMS）的使用，包括点对点模式、发布订阅模式、消息队列的事务管理等。