# 恢复符号表并自动打包ipa

如果想要（像我一样，需要），把恢复符号表，并打包ipa的整个过程，自动化，用脚本实现，则可以参考：

[crifan/AutoRepackIpa: Auto repack ipa](https://github.com/crifan/AutoRepackIpa)

如此，后续：

* 每次，IDA中优化了代码（改动了新的函数名等）后，就可以：
  * （针对每个二进制）IDA中去运行[exportIDASymbol.py](https://github.com/crifan/restore-symbol/blob/master/tools/IDAScripts/export_ida_symbol/exportIDASymbol.py)
  * 然后再去运行[autoRepackIpa.py](https://github.com/crifan/AutoRepackIpa/blob/main/autoRepackIpa.py)

即可实现： 恢复符号表+自动打包ipa，的自动化了 -》从而提高效率，省掉很多手动的重复工作。

接着只需要：

* （iPhone中）卸载原先app
* （用scp等工具）把新的（带最新的符号表=函数名等的）ipa传输到iPhone中
* （用Filza等）安装新的ipa

即可实现：

被调试的app，内置最新的符号表，方便后续调试。
