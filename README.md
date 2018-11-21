# EosFunHash

## eosfun采用最新区块hash值进行开奖(结果可验证)
> EOS区块HASH是一个以16进制显示的32位的字符串，它是根据一系列非常复杂的加密算法随机生成的，，而我们的开奖号码正是利用了这样一个真正的随机的结果来计算开奖号码，实现绝对公平。在crash倒计时结束后，获取最新的区块Hash来计算开奖结果

## 计算方法
> crash(爆点） = crashGame(hash);  
--
比如， crash = crashGame("0140de717d445df9faaf34604807e4800b93a5f54da22655453e2290e98c0430");  
结果放大了100倍，比如 101 表示 1.01x， 808表示8.08x  
开奖结果位于 100-970000之间，也就是 1.0x - 9700x之间

## java 代码实现如下

```java
    /**
    * calculate crash result
    */
    public static int crashGame(String hash){
        int num = custom_hash(hash);
        num = num % 10000;
        int res = 970000 / (10000 - num);
        return res < 100 ? 100 : res;
    }
    
    /***
    * hash
    */
    public static int custom_hash(String hash) {
        int h = 0;
        //将字符串转字符数组，java的库函数，（很多人对此有疑问？可以请教一下编程朋友们）
        char[] value = hash.toCharArray();
        if (value.length > 0) {
            char val[] = value;
            for (int i = 0; i < value.length; i++) {
                h = 31 * h + val[i];
            }
        }
        return (h < 0) ? -h : h;
    }
```
