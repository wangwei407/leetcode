## 位操作基础
![picture](http://static.oschina.net/uploads/space/2015/0510/142121_eD1A_120166.png)
### 判断奇偶
```java 
用 (i&1)==0 代替 a%2==0
```
### 交换两个数
```java
int a=1,b=2;
//第一步 a=a^b,b=b^(a^b)=b^b^a,任何数和自身的异或为0，0与任何数的异或为任何数。所以结果为b=a,最后a=a^b=a^b^a=b.
a^=b;
b^=a;
a^=b;
```
### 变换符号
```java
//取反+1
int a,b=11,-11;
a=~a+1;
b=~b+1;
```
### 求绝对值
#### method1
```java
// int i=a>>31,右移31位，如果是整数，i==0,如果是负数,i==-1
int i=a>>31
i==0? a:(~a+1)
```
#### method 2
```java 
//现在再分析下。对于任何数，与0异或都会保持不变，与-1即0xFFFFFFFF异或就相当于取反。因此，a与i异或后再减i（因为i为0或-1，所以减i即是要么加0要么加1）也可以得到绝对值。所以可以对上面代码优化下：
int j=a>>31;
(a^j)-j
```
### 在某一个整数的指定位置放1
```java
//在e的第十位置1
int e=0;
e|=1<<10;
```

### 检查某一位是否为1
```java e>>3 & 1 ==1?``` 

```java
//使用位操作 来代替boolean数组
int[] bits=new int[40];
for(int m=0; m<40; m+=3){
bits[m/32]|=(1<<m%32);
}
```

### 一些常用的功能
```java
 /**
     * 获取运算数指定位置的值<br>
     * 例如： 0000 1011 获取其第 0 位的值为 1, 第 2 位 的值为 0<br>
     * 
     * @param source
     *            需要运算的数
     * @param pos
     *            指定位置 (0<=pos<=7)
     * @return 指定位置的值(0 or 1)
     */
    public static byte getBitValue(byte source, int pos) {
        return (byte) ((source >> pos) & 1);
    }
    
/**
     * 将运算数指定位置的值置为指定值<br>
     * 例: 0000 1011 需要更新为 0000 1111, 即第 2 位的值需要置为 1<br>
     * 
     * @param source
     *            需要运算的数
     * @param pos
     *            指定位置 (0<=pos<=7)
     * @param value
     *            只能取值为 0, 或 1, 所有大于0的值作为1处理, 所有小于0的值作为0处理
     * 
     * @return 运算后的结果数
     */
     
     //如果value的值大于0， 我们按照1算， 只要用|就行， 否则按照0处理，将原来的数取反 改为& 原位置是0 为0，原位置是1 也为0
     //1与某位取或 该位为1 0与某位取为0
    public static byte setBitValue(byte source, int pos, byte value) {

        byte mask = (byte) (1 << pos);
        if (value > 0) {
            source |= mask;
        } else {
            source &= (~mask);
        }

        return source;
    }  
   /**
     * 将运算数指定位置取反值<br>
     * 例： 0000 1011 指定第 3 位取反, 结果为 0000 0011; 指定第2位取反, 结果为 0000 1111<br>
     * 
     * @param source
     * 
     * @param pos
     *            指定位置 (0<=pos<=7)
     * 
     * @return 运算后的结果数
     */
     //用1与某位异或 取反该位 如果用0与某位异或 就是保持该位不变
    public static byte reverseBitValue(byte source, int pos) {
        byte mask = (byte) (1 << pos);
        return (byte) (source ^ mask);
    }
// 1. 获得int型最大值
System.out.println((1 << 31) - 1);// 2147483647， 由于优先级关系，括号不可省略
System.out.println(~(1 << 31));// 2147483647

// 2. 获得int型最小值
System.out.println(1 << 31);
System.out.println(1 << -1);

// 3. 获得long类型的最大值
System.out.println(((long)1 << 127) - 1);

// 4. 乘以2运算
System.out.println(10<<1);

// 5. 除以2运算(负奇数的运算不可用)
System.out.println(10>>1);

// 6. 乘以2的m次方
System.out.println(10<<2);

// 7. 除以2的m次方
System.out.println(16>>2);

// 8. 判断一个数的奇偶性
System.out.println((10 & 1) == 1);
System.out.println((9 & 1) == 1);

// 9. 不用临时变量交换两个数（面试常考）
a ^= b;
b ^= a;
a ^= b;

// 10. 取绝对值（某些机器上，效率比n>0 ? n:-n 高）
int n = -1;
System.out.println((n ^ (n >> 31)) - (n >> 31));
/* n>>31 取得n的符号，若n为正数，n>>31等于0，若n为负数，n>>31等于-1
若n为正数 n^0-0数不变，若n为负数n^-1 需要计算n和-1的补码，异或后再取补码，
结果n变号并且绝对值减1，再减去-1就是绝对值 */

// 11. 取两个数的最大值（某些机器上，效率比a>b ? a:b高）
System.out.println(b&((a-b)>>31) | a&(~(a-b)>>31));

// 12. 取两个数的最小值（某些机器上，效率比a>b ? b:a高）
System.out.println(a&((a-b)>>31) | b&(~(a-b)>>31));

// 13. 判断符号是否相同(true 表示 x和y有相同的符号， false表示x，y有相反的符号。)
System.out.println((a ^ b) > 0);

// 14. 计算2的n次方 n > 0
System.out.println(2<<(n-1));

// 15. 判断一个数n是不是2的幂
System.out.println((n & (n - 1)) == 0);
/*如果是2的幂，n一定是100... n-1就是1111....
所以做与运算结果为0*/

// 16. 求两个整数的平均值
System.out.println((a+b) >> 1);

// 17. 从低位到高位,取n的第m位
int m = 2;
System.out.println((n >> (m-1)) & 1);

// 18. 从低位到高位.将n的第m位置为1
System.out.println(n | (1<<(m-1)));
/*将1左移m-1位找到第m位，得到000...1...000
n在和这个数做或运算*/

// 19. 从低位到高位,将n的第m位置为0
System.out.println(n & ~(0<<(m-1)));
/* 将1左移m-1位找到第m位，取反后变成111...0...1111
n再和这个数做与运算*/    
```
