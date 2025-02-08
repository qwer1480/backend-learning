## 基本介绍



## Fanout交换机



## Direct交换机

![image-20250122111615431](https://shuaiyao85.oss-cn-qingdao.aliyuncs.com/img/202501221116476.png)

根据`bindingKey`来进行投送消息，当`bindingKey`一样的时候  达到广播的效果。

发送方通过`routerKey`和队列的`bindingKey`继续暗号对比，一样的话才能发送到这个队列。

![image-20250122112315693](https://shuaiyao85.oss-cn-qingdao.aliyuncs.com/img/202501221123725.png)

这种交换机更加灵活。

## Topic交换机

![image-20250122112538171](https://shuaiyao85.oss-cn-qingdao.aliyuncs.com/img/202501221125226.png)

通过通配符达到了比Direct交换机更加灵活的发送消息，拓展性更加强。

![image-20250122113109178](https://shuaiyao85.oss-cn-qingdao.aliyuncs.com/img/202501221131212.png)

 
