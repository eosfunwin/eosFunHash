# eosFunHash

## eosfun采用最新区块hash值进行开奖

## 计算方法
crash(爆点） = crashGame(hash);

比如， crash = crashGame("0140de717d445df9faaf34604807e4800b93a5f54da22655453e2290e98c0430");
结果放大了100倍，比如 101 表示 1.01x， 808表示8.08x

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
