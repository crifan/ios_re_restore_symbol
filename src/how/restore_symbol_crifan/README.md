# crifan版restore-symbol

用crifan版restore-symbol恢复符号表：

* 核心步骤
  * 用IDA脚本（[exportIDASymbol.py](https://github.com/crifan/restore-symbol/blob/master/tools/IDAScripts/export_ida_symbol/exportIDASymbol.py)）从IDA中导出符号表
    * 导出之前
      * 优化变量名=符号名称
        * 自动
          * 用crifan的IDA脚本[AutoRename](https://github.com/crifan/AutoRename)，自动优化函数名=符号名
        * 手动
          * 经过（静态或动态）分析代码逻辑后，给函数名等重新命名，优化函数名=符号名称
  * 用[crifan版restore-symbol](https://github.com/crifan/restore-symbol)去恢复符号表（导入符号表）
