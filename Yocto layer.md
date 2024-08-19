# layer.conf 示例

```bash
# We have a conf and classes directory, add to BBPATH
BBPATH .= ":${LAYERDIR}"

# We have recipes-* directories, add to BBFILES
BBFILES += "${LAYERDIR}/recipes-*/*/*.bb \
            ${LAYERDIR}/recipes-*/*/*.bbappend"

BBFILE_COLLECTIONS += "yoctobsp"
BBFILE_PATTERN_yoctobsp = "^${LAYERDIR}/"
BBFILE_PRIORITY_yoctobsp = "5"
LAYERVERSION_yoctobsp = "4"
LAYERSERIES_COMPAT_yoctobsp = "scarthgap"
```


## BBPATH

`BBPATH .= ":${LAYERDIR}"`
- **解释**: `BBPATH` 是 BitBake 搜索层的路径变量。这里通过 `.` 表示在现有路径的基础上添加 `:${LAYERDIR}`（通常表示当前层的目录路径）。
- **作用**: 把当前层的目录（`${LAYERDIR}`）添加到 BitBake 搜索路径中，这样 BitBake 在构建时可以找到这个层。


## BBFILES

`BBFILES += "${LAYERDIR}/recipes-*/*/*.bb \ ${LAYERDIR}/recipes-*/*/*.bbappend"`
- **解释**: `BBFILES` 是 BitBake 用来查找配方文件（`.bb` 文件）和 `.bbappend` 文件的变量。
- **作用**: 这里将 `recipes-*` 目录下的所有 `.bb` 和 `.bbappend` 文件路径添加到 `BBFILES` 中，这样 BitBake 能找到该层中的配方和补丁文件。


## BBFILE_COLLECTIONS

`BBFILE_COLLECTIONS += "yoctobsp"`
- **解释**: `BBFILE_COLLECTIONS` 是一个变量，用于定义当前层的集合名。在这里，将这个层命名为 `yoctobsp`。
- **作用**: 通过命名该层为 `yoctobsp`，BitBake 可以识别并管理这个层。


## BBFILE_PATTERN_\<layername\>

`BBFILE_PATTERN_yoctobsp = "^${LAYERDIR}/"`
- **解释**: `BBFILE_PATTERN_yoctobsp` 用于设置 BitBake 在 `yoctobsp` 层中查找文件的模式。
- **作用**: 定义 BitBake 只会在该层的路径（`${LAYERDIR}/`）中查找与该层相关的配方文件。


## BBFILE_PRIORITY_\<layername\>

`BBFILE_PRIORITY_yoctobsp = "5"`
- **解释**: `BBFILE_PRIORITY_yoctobsp` 定义了这个层的优先级。数值越高，优先级越高。
- **作用**: 这里设置的优先级为 5，表示这个层在多个层中有中等的优先级。


## LAYERVERSION_\<layername\>

`LAYERVERSION_yoctobsp = "4"`
- **解释**: `LAYERVERSION_yoctobsp` 定义了该层的版本。
- **作用**: 这里将该层的版本设置为 `4`。


## LAYERSERIES_COMPAT_\<layername\>

`LAYERSERIES_COMPAT_yoctobsp = "dunfell"`
- **解释**: `LAYERSERIES_COMPAT_yoctobsp` 指定了该层与哪一个 Yocto 系列版本兼容。
- **作用**: 这里指定了该层与 Yocto 的 `dunfell` 版本兼容。


## NOTE

```text
layer.conf 中设置的所有变量都不是强制性的，除非 BBFILE_COLLECTIONS 存在。在这种情况下，还必须定义 LAYERSERIES_COMPAT 和 BBFILE_PATTERN。
```


# linux-yocto.inc 示例

```bash
DEPENDS:append:aarch64 = " libgcc"
KERNEL_CC:append:aarch64 = " ${TOOLCHAIN_OPTIONS}"
KERNEL_LD:append:aarch64 = " ${TOOLCHAIN_OPTIONS}"

DEPENDS:append:nios2 = " libgcc"
KERNEL_CC:append:nios2 = " ${TOOLCHAIN_OPTIONS}"
KERNEL_LD:append:nios2 = " ${TOOLCHAIN_OPTIONS}"

DEPENDS:append:arc = " libgcc"
KERNEL_CC:append:arc = " ${TOOLCHAIN_OPTIONS}"
KERNEL_LD:append:arc = " ${TOOLCHAIN_OPTIONS}"

KERNEL_FEATURES:append:qemuall=" features/debug/printk.scc"
```


## DEPENDS:append:\<arch\>

- **解释**: `DEPENDS` 变量定义了当前配方的依赖包。`:append:<arch>` 表示为特定架构追加依赖。
- **含义**:
    - `DEPENDS:append:aarch64 = " libgcc"` 表示对于 `aarch64` 架构，追加 `libgcc` 作为依赖。
    - `DEPENDS:append:nios2 = " libgcc"` 和 `DEPENDS:append:arc = " libgcc"` 对于 `nios2` 和 `arc` 架构，做同样的处理。
- **作用**: 这将确保在构建时，为这些特定架构添加 `libgcc` 作为依赖库。


## KERNEL_CC:append:\<arch\>

- **解释**: `KERNEL_CC` 是用于指定内核编译器选项的变量。`:append:<arch>` 表示为特定架构追加选项。
- **含义**:
    - `KERNEL_CC:append:aarch64 = " ${TOOLCHAIN_OPTIONS}"` 表示对于 `aarch64` 架构，追加 `${TOOLCHAIN_OPTIONS}`（表示工具链选项，可能定义在其他地方）到内核编译器选项中。
    - 同理，`KERNEL_CC:append:nios2` 和 `KERNEL_CC:append:arc` 对应的是为 `nios2` 和 `arc` 架构添加相同的工具链选项。


## KERNEL_LD:append:\<arch\>

- **解释**: `KERNEL_LD` 是用于指定内核链接器选项的变量。`:append:<arch>` 表示为特定架构追加选项。
- **含义**:
    - `KERNEL_LD:append:aarch64 = " ${TOOLCHAIN_OPTIONS}"` 表示对于 `aarch64` 架构，追加 `${TOOLCHAIN_OPTIONS}` 到内核链接器选项中。
    - 同理，`KERNEL_LD:append:nios2` 和 `KERNEL_LD:append:arc` 对应的是为 `nios2` 和 `arc` 架构添加相同的工具链选项。


## KERNEL_FEATURES:append:\<feature\>

- **解释**: `KERNEL_FEATURES` 用来定义内核的特性或配置。`:append:qemuall` 表示针对 `qemuall` 架构追加特性。
- **含义**:
    - `KERNEL_FEATURES:append:qemuall = " features/debug/printk.scc"` 表示对于 `qemuall`，追加 `printk` 特性，该特性通常用于调试内核信息。
    - `printk.scc` 是一个内核配置文件，可能用于启用内核中的 `printk` 功能，用于输出调试信息。


## DEPENDS:prepend:\<arch>
- **解释:** `DEPENDS:append:<arch>` 是将变量添加到末尾，而 `DEPENDS:prepend:<arch>` 则是相反，会将内容添加到变量的开头。

