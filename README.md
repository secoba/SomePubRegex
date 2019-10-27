## Some useful regexes

> Collecting some useful regex string, if you know some, pls tell me. :)

---

[TOC]

#### 校验密码强度 (password strength check)
> 密码的强度必须是包含大小写字母和数字的组合，不能使用特殊字符，长度在8-10之间
```text
^(?=.*\\d)(?=.*[a-z])(?=.*[A-Z]).{8,10}$
```

#### 校验中文 (verify chinese)
> 字符串仅能是中文。
```text
^[\\u4e00-\\u9fa5]{0,}$
```

#### 由数字、字母或下划线 (only number、letter or underline)
> 由数字、字母或下划线组成的字符串
```text
^\\w+$
```

#### 手机号码 (CN-phone number)
> 下面是国内 13、15、18开头的手机号正则表达式。
```text
^(13[0-9]|14[5|7]|15[0|1|2|3|5|6|7|8|9]|18[0|1|2|3|5|6|7|8|9])\\d{8}$
```

#### 校验身份证号码 (CN-identity card)
> 身份证号码的正则校验(15 或 18位)

##### 15位
```text
^[1-9]\\d{7}((0\\d)|(1[0-2]))(([0|1|2]\\d)|3[0-1])\\d{3}$
```

##### 18位
```text
^[1-9]\\d{5}[1-9]\\d{3}((0\\d)|(1[0-2]))(([0|1|2]\\d)|3[0-1])\\d{3}([0-9]|X)$
```

#### 邮箱地址 (email address)
> email地址合规性的正则检查语句
```text
[\\w!#$%&'*+/=?^_`{|}~-]+(?:\\.[\\w!#$%&'*+/=?^_`{|}~-]+)*@(?:[\\w](?:[\\w-]*[\\w])?\\.)+[\\w](?:[\\w-]*[\\w])?
```

#### 校验日期 (verify datetime "yyyy-mm-dd" format)
> "yyyy-mm-dd" 格式的日期校验，已考虑平闰年
```text
^(?:(?!0000)[0-9]{4}-(?:(?:0[1-9]|1[0-2])-(?:0[1-9]|1[0-9]|2[0-8])|(?:0[13-9]|1[0-2])-(?:29|30)|(?:0[13578]|1[02])-31)|(?:[0-9]{2}(?:0[48]|[2468][048]|[13579][26])|(?:0[48]|[2468][048]|[13579][26])00)-02-29)$
```

#### 提取页面超链接 (get url address)
> 提取html中的超链接
```text
(<;a\\s*(?!.*\\brel=)[^>;]*)(href="https?://)((?!(?:(?:www\\.)?'.implode('|(?:www\\.)?', $follow_list).'))[^"]+)"((?!.*\\brel=)[^>;]*)(?:[^>;]*)>
```

#### 抽取注释 (get html comment)
> 查找HMTL中的注释
```text
<!--(.*?)-->
```

#### 匹配HTML标签 (matching html tag)
> 匹配出HTML中的标签。
```text
</?\\w+((\\s+\\w+(\\s*=\\s*(?:".*?"|'.*?'|[\\^'">\\s]+))?)+\\s*|\\s*)/?>
```

#### 验证域名 (verify domain)
> 匹配完整域名
```text
^(?=^.{3,255}$)[a-zA-Z0-9][-a-zA-Z0-9]{0,62}(\.[a-zA-Z0-9][-a-zA-Z0-9]{0,62})+$
```

#### Win文件路径及扩展名校验 (verify win path and extension)
> 验证文件路径和扩展名
```text
^([a-zA-Z]\\:|\\\\)\\\\([^\\\\]+\\\\)*[^\\/:*?"<>|]+\\.txt(l)?$

# import re
# regx = """^([a-zA-Z]\\:|\\\\)\\\\([^\\\\]+\\\\)*[^\\/:*?"<>|]+\\.txt(l)?$"""
# print(re.match(regx,"""C:\\fewfewfw\\fewf\\test.txtf"""))
```

#### 提取Color Hex Codes (get color hex)
> 抽取网页中的颜色代码
```text
\\#([a-fA-F]|[0-9]){3,6}
```

#### 提取网页图片 (get image address)
> 提取网页中所有图片
```text
\\< *[img][^\\>]*[src] *= *[\\"\\']{0,1}([^\\"\\'\\ >]*)
```

#### 校验IPv4地址 (verify ipv4)
> IP4 正则语句。
```text
\\b(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\\b
```

#### 校验IPv6地址 (verify ipv6)
> IP6 正则语句。
```text
(([0-9a-fA-F]{1,4}:){7,7}[0-9a-fA-F]{1,4}|([0-9a-fA-F]{1,4}:){1,7}:|([0-9a-fA-F]{1,4}:){1,6}:[0-9a-fA-F]{1,4}|([0-9a-fA-F]{1,4}:){1,5}(:[0-9a-fA-F]{1,4}){1,2}|([0-9a-fA-F]{1,4}:){1,4}(:[0-9a-fA-F]{1,4}){1,3}|([0-9a-fA-F]{1,4}:){1,3}(:[0-9a-fA-F]{1,4}){1,4}|([0-9a-fA-F]{1,4}:){1,2}(:[0-9a-fA-F]{1,4}){1,5}|[0-9a-fA-F]{1,4}:((:[0-9a-fA-F]{1,4}){1,6})|:((:[0-9a-fA-F]{1,4}){1,7}|:)|fe80:(:[0-9a-fA-F]{0,4}){0,4}%[0-9a-zA-Z]{1,}|::(ffff(:0{1,4}){0,1}:){0,1}((25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])\\.){3,3}(25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])|([0-9a-fA-F]{1,4}:){1,4}:((25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])\\.){3,3}(25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9]))
```

#### 检查URL的前缀 (get url prefix)
> 很多时候需要区分请求是HTTPS还是HTTP，通过下面的表达式可以取出一个url的前缀然后再逻辑判断。
```text
^[a-zA-Z]+:\\/\\/

# print(re.findall("^[a-zA-Z]+:\\/\\/","ftp://test.com"))
```

#### 校验金额 (verify money)
> 金额校验，精确到2位小数。
```text
^[0-9]+(.[0-9]{2})?$
```

#### 判断IE的版本 (get IE version)
> IE目前还没被完全取代，很多页面还是需要做版本兼容，下面是IE版本检查的表达式。
```text
^.*MSIE [5-8](?:\\.[0-9]+)?(?!.*Trident\\/[5-9]\\.0).*$
```
