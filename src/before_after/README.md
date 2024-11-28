# 恢复符号表前后对比

## 恢复符号表之前

* 效果
  * Xcode调试iOS程序 -》 查看函数调用堆栈 -》只能看到无名函数或错误的函数名 -》 无法看到期望的（ObjC等）函数名
    * ![xcode_backstrace_not_func_name](../assets/img/xcode_backstrace_not_func_name.png)
  * Xcode给iOS的ObjC函数加断点
    * 通过（ObjC的）函数名加断点，加不上
      * ![xcode_add_objc_func_breakpoint_fail](../assets/img/xcode_add_objc_func_breakpoint_fail.png)
    * 给ObjC的函数加断点，只能用
      * lldb无名函数`___lldb_unnamed_symbol1$$AwemeCore`
      * 或（计算出的实际的）地址

## 恢复符号表之后

* 效果
  * Xcode调试iOS程序 -》 查看函数调用堆栈 -》就能看到函数名了
    * ![xcode_bt_see_objc_func_name](../assets/img/xcode_bt_see_objc_func_name.png)
  * Xcode给iOS的ObjC函数加断点 -》断点就能加上了
    * 举例
      * WhatsApp
        * `-[WARootViewController updateOfflineAssignABProperties]`
          * ![xcode_objc_func_trigger](../assets/img/xcode_objc_func_trigger.png)
      * AwemeCore
        * 用ObjC函数名：`+[AWELaunchMainPlaceholder load]`

## 用工具辅助验证

且可以用其他工具辅助验证：的确加上了函数名=符号表了：

* MachOView
  * `Dynamic Symbol Table`->`Indirect Symbols`
    * 之前=没有恢复符号表：`AwemeCore_noSymbol`、`AwemeCore_restoredSymbol`
      * ![machoview_awemecore_no_symbol](../assets/img/machoview_awemecore_no_symbol.png)
   * 之后=已恢复符号表：`AwemeCore_restoredSymbol_HeiTanBc`
      * ![machoview_awemecore_has_symbol](../assets/img/machoview_awemecore_has_symbol.png)
* IDA
  * 之后=已恢复符号表：`AwemeCore_restoredSymbol_HeiTanBc`
    * ![ida_awemecore_has_symbol](../assets/img/ida_awemecore_has_symbol.png)
* (Xcode中)lldb
  * ![xcode_lldb_aweme_has_symbol](../assets/img/xcode_lldb_aweme_has_symbol.png)
