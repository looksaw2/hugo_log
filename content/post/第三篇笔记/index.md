+++
date = '2025-02-25T17:15:06+08:00'
draft = false
title = '正则表达式'
+++

### 什么是正则表达式
正则表达式是一种处理文本的重要的方法，试想一下你需要打开一个较大的文本，其中有包含有Cat字符串，你需要将其中的Cat字符串检索出来，但是不想将其他的如cat，CATV等字符串检索出来，这时就有一个较好的技术叫做正则表达式。这里有一个在线学习的网站<a href="https://regex101.com">测试网站</a>

### 正则表达式初体验
进入上面的正则表达式网站，可以发现网站的大体上分为两个部分，一部分叫Regular Expression，另一个叫Test string 可以简单的看到，一部分为需要输入的正则表达式，另一部分为输入的测试文本。例如我们There is a cat on the windows，然后正则表达式输入`\bcat\b`就可以发现文本中的cat已经标蓝，即使用`\bcat\b`正确的匹配了cat字符。但是，更进一步的，我们想要匹配的字符串部分不区分大小写呢？例如文本是下面这个样子：
```
There is a cat on the windows
There is a Cat on the windows
There is a CAT on the windows
```
我们应该如何匹配呢？这样的话，我们可以采用如下的正则表达式，例如`\b[Cc][Aa][Tt]\b`然后可以发现所有的cat都标蓝了，说明这样是可行的。

> 测试一: My name is Ben. Please visit my website at http://WWW.forta.com 请用正则表达式匹配my和My
> 答案 : \b[Mm]y\b

下面来看一种更加先进的模式匹配，例如有一个文件名列表，需要将其中sales开头的文件都筛选出来。例如:
```
sale1.xlsx
order1.xlsx
na1.xlsx
na2.xlsx
order2.xlsx
sa1.xlsx
sa2.xlsx
sale2.xlsx
sale3.xlsx
sa3.xlsx
order2.xlsx
```
这是使用正则表达式`sale.`其中`.`是一个任意匹配字符，可以匹配任何一个字符，自然可以匹配`sale1`,`sale2`,`sale3`,以此类推，如果需要匹配sa和na是不是也可以使用`.a.`来匹配吗，不妨进行测试，可以发现其中还匹配了`sal` 因为sal也满足了`.a.`的匹配方式，那么如何满足匹配的方式呢，注意到需要匹配的是[]a[].xlsx 那么是不是可以`.a..xlsx`但是这样不可以，因为.匹配的是任意的字符，那么如何匹配成功呢？，这里我们需要转义字符，采用这样的`.a.\.xlsx` 可以发现匹配成功。因为在正则表达式中`\.`和.表达的意思相同。

但是考虑下面的一种情况，文本中新加了一个ca1.xlsx，变成了下面的这个文本
```
sale1.xlsx
order1.xlsx
na1.xlsx
na2.xlsx
order2.xlsx
sa1.xlsx
sa2.xlsx
sale2.xlsx
sale3.xlsx
sa3.xlsx
order2.xlsx
ca1.xlsx
```
显然，按照上面的匹配方法，会将新添加的ca1.xlsx匹配进去，如果我们只想匹配na1.xlsx，na2.xlsx,sa1.xlsx,sa2.xlsx,sa3.xlsx那应该怎么办？那可以采用这样的模式匹配的方法[ns]a.\.xlsx的方法来匹配对应的，其中的[ns]表示a前面的字符只能从n，s两个单词中选取一个，这样就派除了c这个单词的干扰。

下面，让事情变得更加复杂一点，不妨加入nax.xlsx,sax.xlsx这样的文本，但是不允许选择nax.xlsx,sax.xlsa这样的文本
```
sale1.xlsx
order1.xlsx
na1.xlsx
na2.xlsx
order2.xlsx
sa1.xlsx
sa2.xlsx
sale2.xlsx
sale3.xlsx
sa3.xlsx
order2.xlsx
ca1.xlsx
nax.xlsx
sax.xlsx
```
在学习过上面的例子过后显然可以想到有这样的一种方法`[ns]a[0123456789]\.xlsx`但是[0123456789]需要输入的字符过多，显然可以简化，不如这样的简化`[ns]a[0-9]\.xlsx`经过测试发现显然可以和上面的情况一致有效的缓解了需要输入过多字符的不爽感。下面介绍一下一些常见的正则范围`[A-Z]`表示所有的大写字母，`[a-z]`表示所有的小写字母，`[A-z]`表示所有的大小写字母(不常用，包含了除开了大小写字母之外的其他符号)

