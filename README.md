# springboot-encrypt-decode

> 关于对称加密，非对称加密，加密算法的学习


# 加密解密相关知识扫盲



## 1. 加密概念

密码学是研究编制密码和破译密码的技术科学。以数学为基础，在加密和解密、攻击和防守、矛和盾的对抗过程中交替发展起来。从数学算法的角度看，它包含对称密码算法、非对称密码算法和杂凑算法。

我们先来看下加密中经常提到的一些概念吧！

- **明文**：明文指的是未被加密过的原始数据。
- **密文**：明文被某种加密算法加密之后，会变成密文，从而确保原始数据的安全。密文也可以被解密，得到原始的明文。
- **密钥**：密钥是一种参数，它是在明文转换为密文或将密文转换为明文的算法中输入的参数。密钥分为对称密钥与非对称密钥，分别应用在对称加密和非对称加密上。



## 2. 对称加密

对称加密又叫做私钥加密，即信息的发送方和接收方使用同一个密钥去加密和解密数据。对称加密的特点是算法公开、加密和解密速度快，适合于对大数据量进行加密。

> **加密过程如下**：明文 + 加密算法 + 私钥 => 密文
> **解密过程如下**：密文 + 解密算法 + 私钥 => 明文





![image-20230327185717948](/images/image-20230327185717948.png)



对称加密中用到的密钥叫做私钥，私钥表示个人私有的密钥，即该密钥不能被泄露。 其加密过程中的私钥与解密过程中用到的私钥是同一个密钥，这也是称加密之所以称之为“对称”的原因。由于对称加密的算法是公开的，所以一旦私钥被泄露，那么密文就很容易被破解，所以对称加密的缺点是密钥安全管理困难。

**如果你不是很理解，就看这个通俗易懂的例子**：

> 甲对乙说，我这有一把锁，以后我们互相传消息，就把消息放盒子里，然后用这个锁锁上再传，这个锁有两把一模一样的钥匙，咱俩一人一把，说完甲把钥匙递给了乙。

## 3. 非对称加密

非对称加密也叫做公钥加密。非对称加密与对称加密相比，其安全性更好。对称加密的通信双方使用相同的密钥，如果一方的密钥遭泄露，那么整个通信就会被破解。而非对称加密使用一对密钥，即公钥和私钥，且二者成对出现。私钥被自己保存，不能对外泄露。公钥指的是公共的密钥，任何人都可以获得该密钥。用公钥或私钥中的任何一个进行加密，用另一个进行解密。

> **被公钥加密过的密文只能被私钥解密，过程如下**：
> 明文 + 加密算法 + 公钥 => 密文， 密文 + 解密算法 + 私钥 => 明文





![image-20230327185908815](/images/image-20230327185908815.png)



由于加密和解密使用了两个不同的密钥，这就是非对称加密“非对称”的原因。非对称加密的缺点是加密和解密花费时间长、速度慢，只适合对少量数据进行加密。

**如果你不是很理解，就看这个通俗易懂的例子**：

> 甲对乙说，我这里有A型号锁，对应钥匙A，我给你一大箱子A锁，但是钥匙A不给你，以后你给我发消息就用A锁锁在盒子里给我，然后我自己用钥匙A就能打开看。
> 乙对甲说，我这里有B型号锁，对应钥匙B，我给你一大箱子B锁，但是钥匙B不给你，以后你给我发消息就用B锁锁在盒子里给我，然后我自己用钥匙B就能打开看。

## 4. 常见加密算法比较

加密算法分 对称加密 和 非对称加密，其中对称加密算法的加密与解密 密钥相同，非对称加密算法的加密密钥与解密 密钥不同，此外，还有一类 **不需要密钥** 的 **散列算法**。

常见的 对称加密 算法主要有 **DES、3DES、AES** 等，常见的 非对称算法 主要有 **RSA、DSA** 等，散列算法 主要有 **SHA-1、MD5** 等。

### 4.1. 散列算法比较

| 名称  | 安全性 | 速度 |
| ----- | ------ | ---- |
| MD5   | 中     | 快   |
| SHA-1 | 高     | 慢   |

### 4.2. 对称加密算法比较

| 名称 | 密钥名称        | 运行速度 | 安全性 | 资源消耗 |
| ---- | --------------- | -------- | ------ | -------- |
| DES  | 56位            | 较快     | 低     | 中       |
| 3DES | 112位或168位    | 慢       | 中     | 高       |
| AES  | 128、192、256位 | 快       | 高     | 低       |

### 4.3. 非对称加密算法比较

| 名称 | 成熟度 | 运行速度 | 安全性 | 资源消耗 |
| ---- | ------ | -------- | ------ | -------- |
| RSA  | 高     | 中       | 高     | 中       |
| ECC  | 高     | 慢       | 高     | 高       |

对称加密 的 密钥管理比较难，不适合互联网，一般用于内部系统，安全性只能算中等，但加密速度快好 几个数量级 (软件加解密速度至少快 100 倍，每秒可以加解密数 M 比特 数据)，适合大数据量的加解密处理。非对称加密 的 密钥容易管理，安全性也较高，但是加密速度比较慢，适合 小数据量 加解密或数据签名。





## 5. 常见加密算法使用

### 5.1. MD5算法

> MD5 用的是 哈希函数，它的典型应用是对一段信息产生 信息摘要，以 防止被篡改。严格来说，MD5 不是一种 加密算法 而是 摘要算法。
> 无论是多长的输入，MD5 都会输出长度为 128bits 的一个散列值串 (通常表示为32位的16进制数)。

Java使用案例：

```text
public static final byte[] computeMD5(byte[] content) {
    try {
        MessageDigest md5 = MessageDigest.getInstance("MD5");
        return md5.digest(content);
    } catch (NoSuchAlgorithmException e) {
        throw new RuntimeException(e);
    }
}
```

参考测试代码


[MessageDigest是什么？](https://blog.csdn.net/qq_41918166/article/details/115552035)


### 5.2. SHA1算法

> SHA1 是和 MD5 一样流行的 消息摘要算法，然而 SHA1 比 MD5 的 安全性更强。
> 对于长度小于 2 ^ 64 位的消息，SHA1 会产生一个 160 位的 消息摘要,表示为40位的十六进制数。
> 基于 MD5、SHA1 的信息摘要特性以及 不可逆 (一般而言)，可以被应用在检查 文件完整性 以及 数字签名 等场景。

Java使用案例：

```text
public static byte[] computeSHA1(byte[] content) {
    try {
        MessageDigest sha1 = MessageDigest.getInstance("SHA1");
        return sha1.digest(content);
    } catch (NoSuchAlgorithmException e) {
        throw new RuntimeException(e);
    }
}
```

### 5.3. HMAC算法

> MAC 是密钥相关的 哈希运算消息认证码（Hash-based Message Authentication Code）
> HMAC 运算利用 哈希算法 (MD5、SHA1 等)，以 一个密钥 和 一个消息 为输入，生成一个 消息摘要 作为 输出。
> HMAC 发送方 和 接收方 都有的 key 进行计算，而没有这把 key 的第三方，则是 无法计算 出正确的 散列值的，这样就可以 防止数据被篡改。

**MAC公式：MAC算法+密钥+要加密的信息=密文**

HMAC 是Keyed-Hashing for Message Authentication的缩写。
HMAC的MAC算法是hash算法，它可以是MD5, SHA-1或者 SHA-256，他们分别被称为HMAC-MD5，HMAC-SHA1， HMAC-SHA256。

HMAC用公式表示：

H(K XOR opad, H(K XOR ipad, text))

其中： 
> H：hash算法，比如（MD5，SHA-1，SHA-256） 
> B：块字节的长度，块是hash操作的基本单位。这里B=64。 
> L：hash算法计算出来的字节长度。(L=16 for MD5, L=20 for SHA-1)。 
> K：共享密钥，K的长度可以是任意的，但是为了安全考虑，还是推荐K的长度>B。当K长度大于B时候，会先在K上面执行hash算法，将得到的L长度结果作为新的共享密钥。 如果K的长度<B, 那么会在K后面填充0x00一直到等于长度B。 
> text： 要加密的内容 opad：外部填充常量，是 0x5C 重复B次。 
> ipad： 内部填充常量，是0x36 重复B次。 
> XOR： 异或运算。


**注意**：HMAC 算法实例在 多线程环境 下是 不安全的。但是需要在 多线程访问 时，进行同步的辅助类，使用 ThreadLocal 为 每个线程缓存 一个实例可以避免进行锁操作。

参考测试代码

### 5.4. AES算法

ES、DES、3DES 都是 对称 的 块加密算法，加解密 的过程是 可逆的。
常用的有 AES128、AES192、AES256 (默认安装的 JDK 尚不支持 AES256，需要安装对应的 jce 补丁进行升级 jce1.7，jce1.8)。

DES 加密算法是一种 分组密码，以 64 位为 分组对数据 加密，它的 密钥长度 是 56 位，加密解密 用 同一算法。DES 加密算法是对 密钥 进行保密，而 公开算法，包括加密和解密算法。这样，只有掌握了和发送方 相同密钥 的人才能解读由 DES加密算法加密的密文数据。
因此，破译 DES 加密算法实际上就是 搜索密钥的编码。 对于 56 位长度的 密钥 来说，如果用 穷举法 来进行搜索的话，其运算次数为 2 ^ 56 次。3DES 是基于 DES 的 对称算法，对 一块数据 用 三个不同的密钥 进行 三次加密，强度更高。

> AES 加密算法是密码学中的 高级加密标准，该加密算法采用 对称分组密码体制，密钥长度的最少支持为 128 位、 192 位、256 位，分组长度 128 位，算法应易于各种硬件和软件实现。这种加密算法是美国联邦政府采用的 区块加密标准。AES 本身就是为了取代 DES 的，AES 具有更好的 安全性、效率 和 灵活性。
>

DES:分组块大小--64位
AES:分组块大小--128位

**区块结构：涉及区块链知识体系**


**AES加密解密见代码**


### 5.5. RSA算法

> RSA 加密算法是目前最有影响力的 公钥加密算法，并且被普遍认为是目前 最优秀的公钥方案 之一。RSA 是第一个能同时用于 加密 和 数字签名 的算法，它能够抵抗到目前为止已知的 所有密码攻击，已被 ISO 推荐为公钥数据加密标准。

RSA 加密算法 基于一个十分简单的数论事实：**将两个大 素数 相乘十分容易，但想要对其乘积进行 因式分解 却极其困难，因此可以将 乘积 公开作为 加密密钥**。

**RSA加密解密例子见代码**


## 6. 数字签名

数字签名技术是基于非对称加密技术之上的，

数字签名特点:

  * 防篡改：数据不会被修改。
  * 防抵赖：消息签署者不能抵赖。
  * 防伪造：发送的消息不能够伪造。


## 7. 加密解密相关知识脑图



![encrypt_decode](/images/encrypt_decode.png)



[参考文章](https://zhuanlan.zhihu.com/p/605549569)