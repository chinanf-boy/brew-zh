
# Xcode

## 支持的XCODE版本

HOBBRW支持并推荐最新的XCODE和/或命令行工具可供您的平台使用(参见`OS::Mac::Xcode.latest_version`和`OS::Mac::CLT.latest_version`在里面[`Library/Homebrew/os/mac/xcode.rb`](https://github.com/Homebrew/brew/blob/master/Library/Homebrew/os/mac/xcode.rb))

## XCODE编译器版本

见`OS::Mac::STANDARD_COMPILERS`在里面[`Library/Homebrew/os/mac.rb`](https://github.com/Homebrew/brew/blob/master/Library/Homebrew/os/mac.rb).

## 更新新的XCOP版本

当一个新的XCODE版本被发布时,需要更新以下内容:

-   在[`Library/Homebrew/os/mac/xcode.rb`](https://github.com/Homebrew/brew/blob/master/Library/Homebrew/os/mac/xcode.rb)
    -   `OS::Mac::Xcode.latest_version`
    -   `OS::Mac::CLT.latest_version`
    -   `OS::Mac::Xcode.detect_version_from_clang_version`
-   在[`Library/Homebrew/os/mac.rb`](https://github.com/Homebrew/brew/blob/master/Library/Homebrew/os/mac.rb)
    -   `OS::Mac::STANDARD_COMPILERS`
