# let-us-shell

1. if语句的正确写法，注意空格

```
$input=$1
if [ $input -lt 10 ]; then
  echo 'You should guess a greater number.'
elif [ $input -gt 10 ]; then
  echo 'You should guess a less numer'
else 
  echo 'You win!'
fi
```

2. 如何设置参数默认值
