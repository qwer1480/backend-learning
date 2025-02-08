当partition没有指定的时候，就通过key算出hash值，然后和分区数取余得到发到那个分区，所以只要key一样，你的hahs一样就一样，发送到分区的地方就一样。

![image-20250123104133469](https://shuaiyao85.oss-cn-qingdao.aliyuncs.com/img/202501231041556.png)

数据达到那个分区是由分区策略来搞的。

![image-20250123141659120](https://shuaiyao85.oss-cn-qingdao.aliyuncs.com/img/202501231416179.png)