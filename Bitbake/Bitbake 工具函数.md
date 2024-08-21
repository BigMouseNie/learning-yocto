# bb.utils.contains()

```bash
SPLASH ?= "${@bb.utils.contains('MACHINE_FEATURES', 'screen', 'psplash', '', d)}"
```

- **功能**: 用于检查某个变量中是否包含某个值。它的具体语法是
- **参数 1**: 要检查的变量名（这里是 `"MACHINE_FEATURES"`）。
- **参数 2**: 要查找的值（这里是 `"screen"`）。
- **参数 3**: 如果找到这个值，就返回的字符串（这里是 `"psplash"`）。
- **参数 4**: 如果没有找到这个值，就返回的字符串（这里是 `""`，即空字符串）。
- **参数 5**: `d` 是当前的 BitBake 数据对象，用于在函数中访问和操作其他变量。


# bb.utils.contains_any()

```bash
PACKAGE_EXCLUDE_COMPLEMENTARY:append = "${@bb.utils.contains_any('PACKAGE_INSTALL', 'packagegroup-core-ssh-dropbear dropbear', ' openssh', '' , d)}"
```

- **功能**: 检查一个变量中是否包含任意一个指定的值，并根据结果返回不同的字符串。
- **参数 1**: `'PACKAGE_INSTALL'` — 要检查的变量名。
- **参数 2**: `'packagegroup-core-ssh-dropbear dropbear'` — 要检查的值列表，函数会检查 `PACKAGE_INSTALL` 变量中是否包含这些值中的任意一个。
- **参数 3**: `' openssh'` — 如果在 `PACKAGE_INSTALL` 中找到上述值中的任意一个，则返回这个值（注意前面有一个空格，以便与现有值分隔开）。
- **参数 4**: `''` — 如果没有找到任何值，则返回空字符串。
- **参数 5**: `d` — 当前的 BitBake 数据对象，用于在函数中访问和操作变量。

