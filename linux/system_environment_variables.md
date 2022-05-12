### 相关操作

```shell
# 查看所有环境变量
env

# 系统永久环境变量储存文件，对所有用户生效
/etc/profile

# 用户永久环境变量，对当前用户生效
~/.bash_profile

# 用于修改变量后马上生效，不然只能在下次重新登录时生效
source /etc/profile
source ~/.bash_profile

# 本次连接生效，断开连接失效
export 变量名=变量值
```



### 常用环境变量

```shell
# 当前用户的home绝对路径
$HOME

# 当前所在目录的绝对路径（pwd 命令等效于 echo $PWD）
$PWD

# 上一次访问目录的绝对路径
$OLDPWD

# 当前用户名
$USER

# 当前用户的登录名
$LOGNAME

# 主机名称
$HOSTNAME

# 查看当前使用的脚本解析器
$SHELL

# 系统语言
$LANG

# 当前用户的邮件存放目录
$MAIL

# 函数和可执行文件的目录路径，多个用‘:’隔开，用于全局使用函数
$PATH
```

