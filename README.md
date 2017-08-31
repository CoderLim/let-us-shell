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
