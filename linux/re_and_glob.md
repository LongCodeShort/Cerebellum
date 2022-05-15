## 通配符

1. `*`：匹配任意长度的任意字符

2. `?`：匹配任意单个字符

3. `[]`：匹配指定范围内的任意单个字符

   - `[^]`：匹配指定范围外...
   - `[0-9]`：匹配数字
   - `[a-Z]`：匹配所有英文字母
   - `[A-Z]`：匹配大写英文字母
   - `[:alnum:]`：匹配任意数字或字母
   - `[:space:]`：匹配空格字符
   - `[:punct:]`：匹配所有标点符号

## 正则

- 基础正则BRE：Linux系统默支持该模式

  - `^`：匹配以什么开头的行

  - `$`：匹配以什么结尾的行

  - `^$`：匹配空行（没有任何符号）
  - `.`：匹配任意一个字符（不匹配空行）
  - `\`：转译字符，去除原有符合特殊含义或者表示特定的转译字符序列（`\n \t`等）

  - `*`：匹配前一个字符连续出现0次或者0次以上（贪婪匹配）
  - `.*`：匹配所有内容（包括空行）

- 扩展正则ERE：部分指令通过选择支持

  - `[]`：匹配任意一个中括号内的一个字符，参考通配符（括号内的内容会被去掉特殊含义）

  - `+`：匹配前一个字符连续出现1次或者1次以上（贪婪匹配）
  - `|`：或者关系
  - `()`：表示为一个整体（字符）
  - `{}`：匹配前一个字母出现的次数（贪婪匹配）
    - `{n,m}`：匹配前一个字母至少出现n次，最多出现m次
    - `{n}`：匹配前一个前一个字母刚好出现n次
    - `{n,}`：匹配前一个字母至少出现n次，最多没限制
    - `{,m}`：匹配前一个字母至少出现0次，最多出现m次
  - `?`：匹配前一个字符出现0次或者1次

- PCRE正则：部分指令通过选择支持

```shell
# 测试用例 test.txt
Ideal issss the beacon. Without ideal, there is no secure direction; without direction, there is no life 
We must accept finite disappointment, but we must never lose infinite hope.
It is at our mother“s knee that we acquire our noblest and truest and highest, but there is seldom any money in them.
If winter comes, can spring be far behind?

# 找到以'We'开头的行
grep '^We' test.txt

# 找到以'?'结尾的行
grep '?$' test.txt

# 找到以'.'结尾的行
grep '\.$' test.txt
grep '[.]$' test.txt

# 找到出现‘is或isss...’的行
egrep 'is+' test.txt
grep 'is\+' test.txt

# 找到出现 ‘no‘或者’money’的行
egrep 'We|we' test.txt
egrep '(W|w)e' test.txt
egrep '[Ww]e' test.txt
```

