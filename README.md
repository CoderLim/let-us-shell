# let-us-shell

> 本文适合对shell基础知识有一定了解的童鞋

1. 语句的正确写法，注意空格，该有的不能少，不该有的不能有

```bash
input=$1 #等号左右不能有空格
if [ $input -lt 10 ]; then #[右边和]左边要有空格
  echo 'You should guess a greater number.'
elif [ $input -gt 10 ]; then
  echo 'You should guess a less numer'
else 
  echo 'You win!'
fi
```

2. 如何设置参数默认值

```bash
# 将该文件保存为1.sh
input=${1:-0} #表示取第2个参数，如果没有默认值为0

#执行`sh 1.sh 20`，那么$1就是20，$0就是1.sh
```



3. [如何判断参数是否已经设置](https://stackoverflow.com/questions/3601515/how-to-check-if-a-variable-is-set-in-bash)

```bash
if [ -z ${var+x} ]; then 
  echo "var is unset"; 
else echo "var is set to '$var'"; 
fi
```

4. 遍历当前目录，输出文件名称

```bash
for f in $(ls)
do
  if [ -f $f ]; then
    echo $f
  fi
done

# 打印desktop所有文件
for f in ~/Desktop/*
do
  if [ -f $f ]; then
    echo $f
  fi
done
```

5. set

昨天`阮一峰`发表了一篇文章，可以[参考一下](http://www.ruanyifeng.com/blog/2017/11/bash-set.html)

```bash
# 遇到不存在的变量打印error
set -u
# 输出所有被执行的命令
set -x
# 当遇到指令报错时终止执行
set -e
```

6. 重定向

```bash
# 0 STDIN 标准输入
# 1 STDOUT 标准输出
# 2 STDERR 标准错误
#
# 比如
# 将'hello world'重定向到 1.txt
echo 'hello world' > 1.txt
# 等同于
echo 'hello world' 1> 1.txt

# 标准输出重定向1.txt，标准错误重定向到标准输出
# 最终结果就是标准输出和错误都保存到1.txt
echo 'hello world' 1> 1.txt 2>&1
```

7. sed常用操作

```bash
# 用字符串text2替换1.txt中的字符串text1，然后重定向到2.txt
sed 's/text1/text2' 1.txt > 2.txt
# 打印匹配字符串text1的行
# -n的作用是只打印匹配行，其他不打印，默认是打印的
sed -n '/text1/p' 1.txt
# -i表示直接修改文件内容
sed -i 's/text1/text2/g' *
```
8. awk常用操作

```bash
#
#  虾面用到的引号是单引号，单引号，单引号，双信号无效！
#
# 打印1.txt中每行中用空格分开的第一列数据
awk '{print $1}' 1.txt
# 打印1.txt中每行中用冒号分开的第一列数据
awk -F: '{print $1}' 1.txt
# 可以设置执行脚本前后的操作
awk 'BEGIN {print "begin"} {print $1} END {print "end"}' 1.txt
# 使用变量（也可以使用流程控制语句）
awk 'BEGIN {count=0} {count=count+1} END {print count}' 1.txt
```

9. read

```bash
# -p 表示“File:”为提示
read -p "File:" file
# -a 表示读取一个数组
read -p "Files:" -a files
echo ${files[0]} ${files[1]}
```

10. here document

```bash
# here document是用来显示文档的一种形式
# 如下EOF只是一个标志，可以写成任意名称
cat << EOF
# 这里写文字
# 这里写文字
# 这里写文字
EOF
```

11. 退出码

[more](https://shapeshed.com/unix-exit-codes/)

```bash
cat file.txt
hello world
# $?可以拿到上条命令执行的退出码
echo $?
0
```

12. curl

```bash
# get
curl http://www.xxx.com
# post
curl -X POST http://www.xxx.com
# post 数据
curl -d '这里是数据' http://www.xxx.com
# 设置header
curl -H 'key1: value1' -H 'key2: value2' http://www.xxx.com
# 设置cookie
curl -b 'key1=value1;key2=value2' http://www.xxx.com
```
