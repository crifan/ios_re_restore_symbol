# Address not found in the image

* 现象

去用：

```bash
/Users/crifan/dev/DevSrc/iOS/symbol/restore-symbol/HeiTanBc/restore-symbol/restore-symbol YouTube -o YouTube_objcBlockSymbol -j
 block_symbol.json
```

去恢复Block符号表，但报错：

```bash
2022-04-20 20:35:09.565 restore-symbol[17780:328585] Address(100eaf5a8) not found in the image
```

* 原因

block的符号表的输入文件中，包含无效的地址的条目

```json
{
  "name": "-[YTYouTubeUserDefaultsKeysProvider userSpecificSettingKeys]_block", 
  "address": "0x100EAF5A8"
 },
```

其中的：`0x100EAF5A8`无法识别

解决办法：

删除这个条目，另存为新的json文件，（比如`block_symbol_removedInvalid.json`）再重新执行

```bash
/Users/crifan/dev/DevSrc/iOS/symbol/restore-symbol/HeiTanBc/restore-symbol/restore-symbol YouTube -o YouTube_objcBlockSymbol -j block_symbol_removedInvalid.json
```
