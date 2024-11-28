# 原版restore-symbol

## restore-symbol的版本

此处所说的原始版本的`restore-symbol`，是相对于我自己修改的版本来说的。

而演示版本的`restore-symbol`，又分几个版本：

* 最原始版本： `tobefuturer`的`restore-symbol`
  * https://github.com/tobefuturer/restore-symbol
* 改进版本：`HeiTanBc`的`restore-symbol`
  * https://github.com/HeiTanBc/restore-symbol

但是总体用法是一样的，下面以

* [HeiTanBc版本的restore-symbol](https://github.com/HeiTanBc/restore-symbol)

为例，来说明如何去恢复符号表：

## 准备

下载、编译、确认：

```bash
git clone --recursive https://github.com/HeiTanBc/restore-symbol.git
cd restore-symbol
make
./restore-symbol
```

## 用restore-symbol恢复ObjC符号表

语法：

```bash
restore-symbol MachOFile_orig -o MachOFile_restoredSymbol_HeiTanBc
```

## 用`ida_search_block.py`恢复Block符号表

想要继续额外恢复iOS的Block的符号表，则可以借助IDA插件：`ida_search_block.py`

### 下载ida_search_block.py

* 概述
  * 下载[Crifan版ida_search_block.py](https://github.com/crifan/restore-symbol/blob/master/tools/IDAScripts/search_oc_block/ida_search_block.py)
* 详解
  * 而关于`ida_search_block.py`的文件，此处代码仓库中是有的：
    * https://github.com/HeiTanBc/restore-symbol/blob/master/search_oc_block/ida_search_block.py
      * 但该版本有些bug
    * 而我Crifan修改后的：修复该bug+额外优化后的最新版本是
      * https://github.com/crifan/restore-symbol/blob/master/tools/IDAScripts/search_oc_block/ida_search_block.py
        * 推荐用此最新版

### 用ida_search_block.py导出Block符号表

* 去用IDA打开分析你的Mach-O文件：`MachOFile_restoredSymbol_HeiTanBc`
* IDA中加载插件：`IDA`->`File`->`Script File`->选择`ida_search_block.py`
  * 输出结果：（同目录下新增block符号表文件）`block_symbol.json`

### 恢复Block符号表

此处，在本身已恢复了ObjC符号表后，再想要额外恢复=导入Block符号表，可以用`-j`参数：

```bash
restore-symbol MachOFile_restoredSymbol_HeiTanBc -o MachOFile_objcBlockSymbol -j block_symbol.json
```
