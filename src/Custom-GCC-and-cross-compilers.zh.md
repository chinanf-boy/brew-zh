
# 自定义GCC和交叉编译器

HOBBURW依赖于具有最新版本的XCODE,因为它带有特定版本的构建工具,例如.`clang`.

安装GCC的自定义版本或`autotools`进入`PATH`有可能打破许多编译,所以我们更喜欢苹果或自制的编译器.

基于GCC的交叉编译器通常是"仅KEG",因此默认情况下不链接到路径中.

在这个时候,我们不会把它们合并在一起,而是把它们列在这个页面上.如果你想出了一个新版本的GCC或交叉编译器套件的公式,请把它链接到这里.

-   自制饮料提供了`gcc`公式使用XCODE 4.2 +或当需要C++ 11支持早期版本.
-   家庭酿造提供旧的GCC公式,例如.`gcc@4.9`和`gcc@6`.
-   HybBurw提供LLVM CLAN,它与`llvm`公式.
-   [RISC-V](https://github.com/riscv/homebrew-riscv)提供包括BIUTILS和GCC的RISC-V工具链.
