### Service接口

![image-20241212165157293](https://shuaiyao85.oss-cn-qingdao.aliyuncs.com/img/202412121651427.png)



![image-20241212165212770](https://shuaiyao85.oss-cn-qingdao.aliyuncs.com/img/202412121652884.png)

#### 整体流程

![image-20241213134701239](https://shuaiyao85.oss-cn-qingdao.aliyuncs.com/img/202412131347301.png)



### 批量提交

每一次提交都是一个新的sql  每一次都是网络请求

```java
  @Test
    void testSaveOneByOne() {
        long b = System.currentTimeMillis();
        for (int i = 1; i <= 100000; i++) {
            userMapper.saveUser(buildUser(i));
        }
        long e = System.currentTimeMillis();
        System.out.println("耗时:"+ (e - b));
    }
```

> 耗时:1555974

mb的批提交 先给你1000条打包  再请求   降低网络请求   但是还是一条一条执行

```java
@Test
    void testSaveBatch() {
        List<User> list = new ArrayList<>(1000);
        long b = System.currentTimeMillis();
        for (int i = 0; i < 100000; i++) {
            list.add(buildUser(i));
            if (i % 1000 == 0){
                userService.saveBatch(list);
                list.clear();
            }
        }
        long e = System.currentTimeMillis();
        System.out.println("耗时:"+ (e - b));
    }
```

如果能变成一条数据就是真正的批处理

![image-20241213134155325](https://shuaiyao85.oss-cn-qingdao.aliyuncs.com/img/202412131341566.png)

使用mysql的配置 `rewriteBatchedStatments`,默认为false  改为true就可以改写sql

> 耗时:24612

![image-20241213134546598](https://shuaiyao85.oss-cn-qingdao.aliyuncs.com/img/202412131345657.png)