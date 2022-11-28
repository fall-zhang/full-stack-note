> Create by **fall** on 2022-11-22
> Recently revised in 2022-11-22

## Bash

### 入门

`hello.sh`

```bash
#!/bin/sh
VAR="world"
echo "Hello $VAR"
```

```bash
$ bash hello.sh
```

### 变量

```bash
NAME="Fall"
echo ${NAME}    # => Fall (变量)
echo $NAME      # => Fall (变量)
echo "$NAME"    # => John (变量)
echo '$NAME'    # => $NAME (字符串原样输出)
echo "${NAME}!" # => John! (变量)
NAME = "John"   # => Error (注意不能有空格)
```

### 注释

```bash
# 这是一个内联 Bash 注释。
:'
这是 bash 多行注释
bash echo
'
```

### 参数

| 表示        | 描述                     |
| ----------- | ------------------------ |
| `$1` … `$9` | 参数 1 ... 9             |
| `${10}`     | 位置参数 10              |
| `$0`        | 脚本本身的名称           |
| `$#`        | 参数数量                 |
| `$$`        | shell 的进程 id          |
| `$*`        | 所有参数                 |
| `$@`        | 所有参数，从第一个开始   |
| `$-`        | 当前选项                 |
| `$_`        | 上一个命令的最后一个参数 |

### 函数

```bash
get_nabashme() {
    echo "John"
}
echo "You are $(get_name)"
```

### 条件语句

```bash
if [[ -z "$string" ]]; then
    echo "String is empty"
elif [[ -n "$string" ]]; then
    echo "String is not empty"
fi
```

