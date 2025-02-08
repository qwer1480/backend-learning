### **Object.sleep**

1. 是否释放锁   不会释放锁

![image-20241212143429859](https://shuaiyao85.oss-cn-qingdao.aliyuncs.com/img/202412121436566.png)

2. 是否对终端敏感   敏感

```java
throws InterruptedException
```

3. 是否释放cpu   会释放cpu

### Object.wait

1. 会释放锁  且进去等待队列
2. 对中断敏感
3. 是会释放cpu，让出cpu等待片进入等待队列

### Thread.join

1. 对中断敏感

```java
public final void join() throws InterruptedException
```

2. 是否释放cpu

释放 因为底层是调用的wait方法

```java
public final synchronized void join(long millis)
    throws InterruptedException {
        long base = System.currentTimeMillis();
        long now = 0;

        if (millis < 0) {
            throw new IllegalArgumentException("timeout value is negative");
        }

        if (millis == 0) {
            while (isAlive()) {  // 如果线程是存活状态
                wait(0); // 那么调用wait阻塞当前线程
            }
        } else {
            while (isAlive()) {
                long delay = millis - now;
                if (delay <= 0) {
                    break;
                }
                wait(delay);
                now = System.currentTimeMillis() - base;
            }
        }
    }
```

3. join方法会阻塞调用它的方法

```java
/**
 * join会阻塞调用join方法的线程  调用的线程被阻塞  t线程异步执行，当t线程结束之后 唤醒调用的线程，这里是主线程
 */
public class JoinExample {
    public static int i = 10;
    public static void main(String[] args) throws InterruptedException {
        Thread t = new Thread(
            () ->{
              i = 30;
            }
        );
        t.start();
        t.join();
        System.out.println("i = " + i);
    }
}
```

### 线程通信

1. 共享内存：使用static变量，但是需要锁来保证线程安全
2. 使用wait和notify
3. 使用vliatile变量，保证变量的可见性
4. 使用synchronized同步关键字
5. 使用condition.await/signal方法

