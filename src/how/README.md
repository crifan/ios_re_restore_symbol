# 如何恢复符号表

此处有2种办法：

* 推荐方式
  * [crifan版restore-symbol](../how/restore_symbol_crifan/README.md)
    * 推荐原因：能同时实现 自动给很多函数重命名+恢复ObjC符号表+恢复Block符号+其他优化
* 普通方式
  * [原版restore-symbol](../how/restore_symbol_orig/README.md)
    * 概述：用HeiTanBc版本的restore-symbol
      * 只能恢复ObjC符号表+恢复Block符号，且之前脚本有bug
