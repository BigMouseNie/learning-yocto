# =

赋值运算符。将右侧的值赋给左侧的变量。
```bash
VAR = "value"
```


# +=

追加运算符。将右侧的值追加到左侧变量的当前值。
```bash
VAR += "additional_value"
```


# ?=

条件赋值运算符。如果左侧变量没有被赋值，则将右侧的值赋给左侧变量。
```bash
VAR ?= "default_value"
```


# ??=

条件追加运算符。如果左侧变量没有被赋值，则将右侧的值追加到左侧变量。
```bash
VAR ??= "default_value"
```


# :=

延迟赋值运算符。立即求值右侧的表达式，并将结果赋给左侧变量。
```bash
VAR := "value_${PN}"
```


# += (for lists)

列表追加运算符。将右侧的项追加到左侧列表变量。
```bash
VAR += "item"
```


# ^=

前缀追加运算符。将右侧的值追加到左侧变量的前面。
```bash
VAR ^= "prefix_"
```


# = (in append)

```bash
VAR = "new_value"
```


# |=

列表合并运算符。将右侧的列表项合并到左侧列表中，而不会重复。
```bash
VAR |= "new_item"
```


# .=

追加运算符。它会将右侧的值追加到左侧变量的当前值之后。
```bash
# ':' 是路径分割符
BBPATH .= ":${LAYERDIR}"
```

