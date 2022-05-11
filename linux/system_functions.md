### Read：读取控制台输入

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
