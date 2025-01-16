# crifan版restore-symbol

* 用[crifan版restore-symbol](https://github.com/crifan/restore-symbol)去恢复符号表（导入符号表）
  * 概述
    * 优化符号表=优化变量名
      * 【仅需一次】优化ObjC的Block函数名
        * 使用[Crifan版ida_search_block.py](https://github.com/crifan/restore-symbol/blob/master/tools/IDAScripts/search_oc_block/ida_search_block.py)去恢复ObjC的Block符号表
      * 优化其他函数名
        * 【一般仅需一次】自动
          * 用crifan的IDA脚本[AutoRename](https://github.com/crifan/AutoRename)，自动优化函数名=符号名
        * 【后续多轮操作】手动
          * 经过（静态或动态）分析代码逻辑后，给函数名等重新命名，优化函数名=符号名称
    * 用（[exportIDASymbol.py](https://github.com/crifan/restore-symbol/blob/master/tools/IDAScripts/export_ida_symbol/exportIDASymbol.py)）从IDA中导出符号表
    * 运行`restore-symbol`导入（最新的、全部的）符号表
      ```bash
      restore-symbol -w true -s false -j {exported_IDA_symbols.json} -o {outputFile_RestoredSymbol} {inputMachOFile}
      ```
  * 详解
    * [crifan版restore-symbol](https://github.com/crifan/restore-symbol)
