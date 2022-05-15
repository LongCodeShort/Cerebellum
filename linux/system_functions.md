### help：查看当前函数的用法

- 基本语法：`函数 --help`  或 `help 函数`

```shell
cut --help
help cd
```

------

### read：读取控制台输入

- 基本语法：`read [选项][变量]`
- 选项：
  1. `-p`：指定读取值时的提示符
  2. `-t`：指定读取值时等待的时间（单位秒）
- 参数：
  1. 变量：指定要读取值的变量名

```shell
# 提示5秒，读取控制台输入的名称
read -t 7 -p "Enter your name in 5 seconds" NAME
echo $NAME
```
------
### basename：删除字符串（路径）中最后一个'/'字符前的部分。（通常用于获取文件名）

- 基本语法：`basename 字符串 [suffix]`
- 参数
  1. 字符串：要被删除的目标字符串或路径
  2. suffix(可选)：指定要删除的后缀部分

```shell
# 结果为test
basename /home/longcodeshort/test.txt .txt
```
------
### dirname：获取字符串（文件绝对路径）的目录路径部分

- 基本语法：`dirname 字符串`
  1. 字符串：要被删除的目标字符串或路径

```shell
# 结果为 /home/longcodeshort
dirname /home/longcodeshort/test.txt
# 结果为 /home
dirname /home/longcodeshort/
# 结果为 /
dirname /home
```
------

### cut：从文件中每一行剪切字节、字符和字段并将剪切的内容输出

- 基本语法：`cut [选项] 文件名`
- 选项：
  1. `-f`：列号，指定提取分割后的第几列
  2. `-d`：指定分隔符（默认分隔符为制表符）
  3. `-b`：以字节单位为进行分割，指定字节的位数或者区间（切割的字节会自动从前到后排序输出）

```shell
# 测试数据 test.txt
dong shen
guan zhen
wo  wo
lai  lai
le  le1

# 获取第一列数据
cut -d ' ' -f 1 test.txt
dong
guan
wo
lai
le

# 获取二三列数据
cut -d ' ' -f 2,3 test.txt
shen
zhen
 wo
 lai
 le1

# 获取'guan'
cut -b 1-4 test.txt | grep guan

# 选取系统变量PATH第二个“:”后的所有路径
echo $PATH | cut -d : -f 2-

# 获取ifconfig中docker0网卡的IP地址
ifconfig docker0 | grep "inet" | cut -d ' ' -f 10
```

------

### grep：文本过滤工具

基本语法：`grep [选项] 文件名`

- 选项：
- `-E`：支持扩展正则（等价于`egrep`）
- `-An`：匹配到内容后显示匹配的内容和匹配内容下面的n行(after)
- `-Bn`：匹配到内容后显示匹配的内容和匹配内容上面的n行(before)
- `-Cn`：匹配到内容后显示匹配的内容和匹配内容上下的n行(context)
- `-c`：显示匹配到的的行数（效果等效于`wc -l`）
- `-v`：排除掉匹配的行
- `-n`：显示行号
- `-i`：忽略大小写
- `-w`：精确匹配
- `-o`：只显示匹配到的字符串，每个字符串显示时占一行

```shell
# 精确匹配new
echo news new | grep -w new
echo news new | grep '\new\b'
echo news new | grep '\<new\>'
```



### sed：文件流编辑器，一次处理一行，把当前行的内容存储在临时缓冲区（模式空间）进行处理，处理完成后把缓冲区的内容输出到标准输出，接着处理下一行，直到文件末尾，原文件默认不会改变。

- 基本语法：`sed [选项] 文件名`
- 选项：
  1. `-e`：指定的script来处理输入的文本文件（可以省略，但是后面的脚本需要用引号包含）
  2. `-f`：指定的script文件来处理输入的文本文件
  3. `-n`：仅显示处理后的结果
  4. `-i`：是当前修改作用于原文件
- 脚本动作：
  1. `a\`： 在当前行后面加入一行指定文本
  2. `i\` ：在当前行上面插入一行指定文本
  3. `d` ：从模版块删除行
  4. `c\` ：用新的文本改变指定行的文本
  5. `s/正则表达式/新内容/g`：用新内容替换正则表达式匹配的内容。（‘/’分隔符可以替换为其他符号；‘g’为全局替换，用于当前行多个匹配内容时全部替换）
  6. `h`：拷贝模板块的内容到内存中的缓冲区
  7. `p`：指定要打印的行
  8. `q`：退出脚本

```shell
# 测试数据 test.txt
dong shen
guan zhen
wo  wo
lai  lai
le  le1

# 将'abc'插入到第2行的下一行
sed '2a\abc' test.txt

# 将'abc'插入到第2行的下一行,将'def'跟着换行插入
sed '2a\abc\
def' test.txt

# 删除第2和第3行
sed '2,3d' test.txt

# 删除第3行到最后一行
sed '3,$d' test.txt

# 替换最后一行为'good' 
sed '$c\good' test.txt

# 搜寻字母e行并显示
sed -n '/e/p' test.txt

# 搜寻字母e的行并删除
sed '/e/d' test.txt

# 搜寻'en'并替换为'eng'
sed 's/en/eng/' test.txt

# 搜寻'o'并替换为'oo',
sed 's|o|oo|g' test.txt

# 搜寻字母u所在行并执行替换脚本，输出结果
sed -n '/u/{s/en/eng/;p;q}' test.txt

# 连续命令
sed -e '$a\good' -e 's/o/oo/g' test.txt
```

