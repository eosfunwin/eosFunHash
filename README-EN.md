# eosFunHash

## Eosfun uses the latest block hash value to resolve your bet (results can be verified)
> The EOS block HASH is a 32-Byte string displayed in hexadecimal, which is randomly generated according to a series of 
> very complicated encryption algorithms, and our lottery number is using such a truly random result. Calculate the lottery 
> number to achieve absolute fairness. After the crash countdown, get the latest block hash to calculate the lottery result.

## Calculation method
crashValue = crashGame(hash);
--
For example， crash = crashGame("0140de717d445df9faaf34604807e4800b93a5f54da22655453e2290e98c0430");
The result has been expanded by 100 times，such as 101 means 1.01x， 808 means 8.08x
crashValue between 100-970000，also between 1.0x - 9700x

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
