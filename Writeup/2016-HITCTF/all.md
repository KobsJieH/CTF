writeup
====

Welcome--签到题  
-------
  题目说注意比赛说明，去看了一下，我以为是自己猜，试了几个，结果不对。就查看源码，在末尾处发现flag！


Web—find me  
-------
  进入网址，就这样一个页面，”这里什么都没有!”   

But how can I believe you? 还是查看源码吧。结果是一大堆谎言：“这里什么都没有”，把那些没用的删掉后  
![这里什么都没有](https://cloud.githubusercontent.com/assets/16100215/16905094/7cac1c94-4cd3-11e6-9a67-cfbf98a04aff.png)  

发现其中有hidden和disabled属性，删掉后试试。  
![最后提交](https://cloud.githubusercontent.com/assets/16100215/16905228/46d01cb8-4cd5-11e6-8f31-3cc73f6e89f2.jpg)  

结果显示了这么一个页面，注意到开始还有“告诉我大赛名称是什么”这么一个信息，于是提交HITCTF。  

得到flag:  
![find me](https://cloud.githubusercontent.com/assets/16100215/16905283/01af803c-4cd6-11e6-812b-0c3267cacfdd.jpg)
 
Crypto-- fdhvdu3affine5
-------
看这题目，应该就是affine cipher了。下面给出解密脚本：  
```python
# -*- coding: utf-8 -*-
def affine(a, b):
    pwd_dic = {}
    for i in range(26):
        pwd_dic[chr(((a*i+b)%26)+97)] = chr(i+97)
    return pwd_dic
if __name__ == '__main__':
    pwd_dic = {}
    pwd = "tjauvoqqmuunihtegnohjimqqeeaoqi"
    plain = []
    str = ''
    pwd_dic = affine(a,b)
    for i in pwd:
        plain.append(pwd_dic[i])
    print  str.join(plain)
```

但是参数如何选择呢？看题目先试一下3和5吧。结果却不知道是什么东西。后面又试着给字符串进行凯撒移位解密，还是没有
正确flag。后来官方给出tips只是确认这两种解密来进行解答。于是使用工具JDK_406.jar编码转换神器，先进行凯撒移位得到
26个字符串， 转换成字符串数组，依次进行参数为3和5的解密，看了看26个解密的信息，看到其中有个信息看着比较顺眼，  
![fdhvdu3affine5](https://cloud.githubusercontent.com/assets/16100215/16905310/855a7a40-4cd6-11e6-8f65-635c99ae6136.png)  
激动地跑去提交，结果还是不对，再仔细看了看，发现后面似乎多了一个r，去掉后再次提交，显示正确！



Misc--我们还是得学习一个
-------
下载下来是一个.docx文档。打开看，是一首诗,先学习一波[xiao cry!]。  
```
出门一笑莫心哀，浩荡襟怀到处开。
时事难从无过立，达官非自有生来。
风涛回首空三岛，尘壤从头数九垓。
休信儿童轻薄语，嗤他赵老送灯台。

```
好吧，看了后一头雾水！  
后面随手把文件后缀改成了rar，解压后得到一些文件。好，这就给人希望了，至少不用看着一首诗发呆了（虽然学习确实可以提高我们姿势水平-_-）。把这些xml文档都看了一下，结果发现styles.xml文件里有个注释，里面给了百度云地址。好吧，去看看(或许有什么福利之类的—---大笑)。得到一张图片，intersting.jpg---“狗”“梨”“郭嘉”“婴儿（生）”“墓（死）”“椅”,什么鬼？。  
![intersing](https://cloud.githubusercontent.com/assets/16100215/16905343/302bf3a4-4cd7-11e6-8821-64abeacd15bb.jpg)  
图片用winhex打开查看十六进制数据，往下拉很长一段都没有发现什么有用信息，不够结尾令人感动，看到两个flag字样。  
![interstinghex](https://cloud.githubusercontent.com/assets/16100215/16905365/83fe6d18-4cd7-11e6-8984-0536b8d746b1.png)  
 观察许久还发现504B0304十六进制数据，这是zip文件的文件头标识，回想起前段时间看过的一篇隐写术博客介绍，有一个关于图种的东西。 于是该图片后缀为zip。用winrar打开，里面发现有一个flag文件，但是那个激动啊，flag已近在咫尺。但是，实践证明，我还是太天真。解压还需要密码，于是，在原来解压出来的xml文档里找，试了好多种组合，都是无用之功，后来还想着是不是伪加密什么的，改了十六进制数据，却是各种错误。就这样，很长很长一段时间过去了。。。。。。  
 
后来突发脑洞，搜了搜这首诗，发现和“苟利国家生死以，岂因祸福避趋之”是同一首诗，欸，“狗”“梨”“郭嘉”“婴儿（生）”“墓（死）”“椅”，好吧，试一试这个解压密码吧！  

####flag：hitctf{7_in_or_f_b_qu_z}
