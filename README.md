# 签到题
加群直接获得

# Crypto
## 贝斯一家
题目  
```
R1pCVE9PSldHTTNUSU5SV0c1QkRJTVpYR0kzVFNOWlFHNDJETVJSVklZMkRTTlpUR1ZEREtNWldJWTJVTU5CVEdaRERNUlJXSU0yVU1NUlJHVkRER1JSWElRPT09PT09
```  
base64decode得到`GZBTOOJWGM3TINRWG5BDIMZXGI3TSNZQG42DMRRVIY2DSNZTGVDDKMZWIY2UMNBTGZDDMRRWIM2UMMRRGVDDGRRXIQ======`
base32decode得到`6C796374667B43727970746F5F49735F536F5F436F6F6C5F215F3F7D`  
base16decode得到flag

## (╯°□°）╯︵ ┻━┻ 
题目`d4e8e1f4a0f7e1f3a0e6e1f3f4a1a0d4e8e5a0e6ece1e7a0e9f3baa0ecf9e3f4e6fbb7b9b8e4b5b5e4e2b7b6b5b5b2e1b9b2b2e4b0b0e4b7b7b5e5b3b3b1b1b9b0b7fd`  
一组十六进制字符串，两个字符一组，转10进制  
```python
s = 'd4e8e1f4a0f7e1f3a0e6e1f3f4a1a0d4e8e5a0e6ece1e7a0e9f3baa0ecf9e3f4e6fbb7b9b8e4b5b5e4e2b7b6b5b5b2e1b9b2b2e4b0b0e4b7b7b5e5b3b3b1b1b9b0b7fd'
a = []
for i in range(0,len(s),2):
	a.append(eval('0x' + s[i:i+2]))

for x in range(1,161):
	flag = ''
	for v in a:
		if (v-x) <32 or (v-x) > 126:
			break
		else:
			flag += chr(v-x)
	print(flag)

```  

每一位数字范围都超过127，其中最小值为160，尝试移位爆破, 找出均为可见字符的字符串，完整脚本入下  
```python
s = 'd4e8e1f4a0f7e1f3a0e6e1f3f4a1a0d4e8e5a0e6ece1e7a0e9f3baa0ecf9e3f4e6fbb7b9b8e4b5b5e4e2b7b6b5b5b2e1b9b2b2e4b0b0e4b7b7b5e5b3b3b1b1b9b0b7fd'
a = []
for i in range(0,len(s),2):
	a.append(eval('0x' + s[i:i+2]))

for x in range(1,161):
	flag = ''
	for v in a:
		if (v-x) <32 or (v-x) > 126:
			break
		else:
			flag += chr(v-x)
	print(flag)
```  

## music
下载音乐，分析频谱，发现摩斯电码  
![wp](http://oznkfpsbn.bkt.clouddn.com/%E8%8E%AB%E6%96%AF1.png)  
提取出来  
```
...../-.../-.-./----./..---/...../-..../....-/----./-.-./-.../-----/.----/---../---../..-./...../..---/./-..../.----/--.../-../--.../-----/----./..---/----./.----/----./.----/-.-.
```
解开得到`5bc925649cb0188f52e617d70929191c`
尝试提交，出错，好吧，去cmd5.com解md5
得到`valar dohaeris`  


# 逆向
## 逆向签到
提取出dex，转jar，用jd-gui查看，明文
![wp](http://oznkfpsbn.bkt.clouddn.com/%E9%80%86%E5%90%91%E7%AD%BE%E5%88%B0.png)  
## App200
核心内容  
![wp](http://oznkfpsbn.bkt.clouddn.com/app200.png)  
拿参数一md5，然后每间隔一位提取字符，最后和参数二的值进行比较  
打开APP验证一下，参数一就按提示输吧`aoteman`  
其md5值为`b89d9bde9a90248a33d1ab2b4628fe53`, 隔位取字符得到`b99d99283da242f5`,作为参数二的值填入  
![wp](http://oznkfpsbn.bkt.clouddn.com/app200-1.png)  
成功，这个就是flag了，带上格式提交就行

## App300
跟踪逻辑，用python还原一下，直接丢脚本吧
```pythhon
s = [b'94', b'99', b'72', b'38', b'68', b'72', b'87', b'89', b'72', b'36', b'118', b'100', b'78', b'72', b'87', b'121', b'83', b'101', b'39', b'69', b'70', b'72', b'66', b'64', b'103', b'100']

for i in s:
	print(chr(int(i)^0x17), end='')
```

# MISC
## 神奇的图片 
下载下来查看文件头，确认是png无误
![wp](http://oznkfpsbn.bkt.clouddn.com/%E7%A5%9E%E5%A5%87%E5%9B%BE%E7%89%87.png)  
emmm,ISCC2018的题目，修改png的高就可以了，参考png文件协议  
![wp](http://oznkfpsbn.bkt.clouddn.com/%E7%A5%9E%E5%A5%87%E5%9B%BE%E7%89%872.png)  

## 远在天边
题目3edr5tgy7 8ujko9 5rfgy6  
拿个键盘画一下，这里被坑了一下U？还是O？  
提交了你就知道←v←  
![wp](http://oznkfpsbn.bkt.clouddn.com/%E8%BF%9C%E5%9C%A8%E5%A4%A9%E8%BE%B91.png)  
![wp](http://oznkfpsbn.bkt.clouddn.com/%E8%BF%9C%E5%9C%A8%E5%A4%A9%E8%BE%B92.png)  

## 海贼王
jpg图片，HexEditor打开，直接找文件尾 FFD9  
后面还有东西，PK头，ZIP文件，提取出来  
![wp](http://oznkfpsbn.bkt.clouddn.com/%E6%B5%B7%E8%B4%BC1.png)  
文件被加密，不是伪加密……爆破吧  
![wp](http://oznkfpsbn.bkt.clouddn.com/%E6%B5%B7%E8%B4%BC2.png)  
解压查看flag.txt  

## Zipfile One
根据提示先生成password字典  
```python
for x in xrange(0,1000000):
	if x < 10:
		print 'lyun' + '00000' + str(x)
		continue
	if x < 100:
		print 'lyun' + '0000' + str(x)
		continue
	if x < 1000:
		print 'lyun' + '000' + str(x)
		continue
	if x < 10000:
		print 'lyun' + '00' + str(x)
		continue
	if x >= 10000 and x < 100000:
		print 'lyun' + '0' + str(x)
		continue
	if x > 100000:
		print 'lyun' + str(x)
```
根据字典爆破得到密码  
![wp](http://oznkfpsbn.bkt.clouddn.com/zipfileone1.png)  
解压得到flag 

## Broken Heart
下载的2个文件用hexeditor打开，jpg没有ffd9结尾，另一个文件尾是ffd9，两个直接拼接得到完整图片
获得flag【我的脖子……要扭了】  
![wp](http://oznkfpsbn.bkt.clouddn.com/%E5%BF%83%E8%84%8F1.png)  
![wp](http://oznkfpsbn.bkt.clouddn.com/%E5%BF%83%E8%84%8F2.png)

## 图片怎么打不开了
修复文件头  
![wp](http://oznkfpsbn.bkt.clouddn.com/%E6%80%8E%E4%B9%88%E6%89%93%E4%B8%8D%E5%BC%801.png)  
逐帧分离  
![wp](http://oznkfpsbn.bkt.clouddn.com/%E6%80%8E%E4%B9%88%E6%89%93%E4%B8%8D%E5%BC%802.png)  
注意，这不是全黑，仔细看，有字的，都提取出来【懒得写代码，肉眼看吧  
`Y2F0Y2hfdGhlX2R5bmFtaWNfZmxhZ19pc19xdWl0ZV9zaW1wbGU=`  
base64解开得到flag,注意格式  


# WEB
## 计算器
点开F12，发现没有form，没有cookie，随便输个1点击验证，没有网络请求，排除编程快速提交这种题目  
应该是本地验证，然而JS只有一个JQ，怀疑对JQ动手脚  
搜索输入框的id`code`，果然在JQ动手脚，得到flag  
![wp](http://oznkfpsbn.bkt.clouddn.com/web%E8%AE%A1%E7%AE%97%E5%99%A8.png)  
## 看看源码
查看源码，有段JS，把eval改成console.log查看  
![wp](http://oznkfpsbn.bkt.clouddn.com/web%E6%9F%A5%E7%9C%8B%E6%BA%90%E7%A0%811.png)  
```javascript
function checkSubmit() {
    var a = document.getElementById("password");
    if ("undefined" != typeof a) {
        if ("67d709b2b54aa2aa648cf6e87a7114f1" == a.value) return ! 0;
        alert("Error");
        a.focus();
        return ! 1
    }
}
document.getElementById("levelQuest").onsubmit = checkSubmit;
```  
提交`67d709b2b54aa2aa648cf6e87a7114f1`得到flag

## WEB1
右键和F12都被禁了，用Chrome的view-source查看源码  
![wp](http://oznkfpsbn.bkt.clouddn.com/web1-1.png)  
emmm，没必要去跟踪混淆逻辑，最后的document.write改成console.log执行，得到flag  lyctf{web1-236482-5469857}  
![wp](http://oznkfpsbn.bkt.clouddn.com/web1-2.png)  

## WEN2
来自出题者的恶意，一堆alert，全局禁用JS后安静了，查看源码  
![wp](http://oznkfpsbn.bkt.clouddn.com/WEB2.png)  
发现HTML实体字符，解码得到flag

## 正则匹配
代码审计题，变量覆盖，猜测是$flag  
get提交args=flag  
得到flag 

## WEB3
看到md5函数弱类型比较，很激动，直接用数组就可以绕过了  
get提交flag1[]=1  
post提交flag2[]=2  
得到flag  

## WEB4
WEB3的进阶版，md5的结果用了===进行比较，然而前面的flag1和flag2的数值比较依然是弱类型==比较  
get提交flag1[]=0e1  
post提交flag2[]=2  
得到flag   

## 靶机
这个300我有点看不懂，题目直接说在根目录flag.txt  
那就访问xx.xx.xx.xx/flag.txt  
得到flag,一开始以为是假的，尝试着提交一下……成功了  

## PPC
首元素为7120597，公差为8161045, 现在要求找出属于该等差数列中的第7219个素数并输出  
直接丢脚本吧  
```python
import math
import sys

def isPrime(n):
	for i in range(2, int(math.sqrt(n)) + 1):
		if n % i == 0:
			return False
	return True


num = 7120597
primeCount = 0
while True:
	if isPrime(num):
		primeCount += 1
		if primeCount == 7219:
			print(num)
			sys.exit(0)
	num += 8161045
```  


# 总结
挺高兴受邀请参加此次赛项的，还有，题目量好多！！！  

