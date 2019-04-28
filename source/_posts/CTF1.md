---
title: "[CTF] CTF(1) MD5之守株待兔"
catalog: true
toc_nav_num: true
date: 2019-04-28 10:51:24
subtitle: "CTF练习题"
header-img: "/img/article_header/article_header.png"
tags:
- CTF
catagories:
- CTF

---
# 题目描述
>从系统锁下手，通过get方式key字段提交答案，直到您的钥匙与系统锁相等则成功。
>
>格式：CTF{}
>
>解题链接： http://ctf5.shiyanbar.com/misc/keys/keys.php

# 题目解析
![avatar](/img/CTF/CTF1-1.png)
1. 打开网页发现有一个false字符串（在解题时我们会用到）
2. 每次刷新发现系统密钥一直在变化，这使我想到了它可能是一个时间戳
(不懂时间戳的请戳[这里](https://baike.baidu.com/item/unix%E6%97%B6%E9%97%B4%E6%88%B3/2078227?fr=aladdin))
3. 您的密钥一直不变

# 写脚本之前对该题的猜想
该题目应该是让我Get一个经过MD5加密的时间戳和它给出的时间戳相等即可

# 撸脚本时间(Python)
```
import requests
import time
url ="http://ctf5.shiyanbar.com/misc/keys/keys.php"
key_time =int(time.time())+10
url ="http://ctf5.shiyanbar.com/misc/keys/keys.php?key="+str(key_time)
while 1:
        res = requests.get(url)
        print (res.text)
        if 'false'  not in res.text:  //这里用到了网页中的false进行判断
            break
```

# 得到结果
>flag{c04ffec18156c696}
![avatar](/img/CTF/CTF1-2.png)