
# 核心贡献者的共同问题

## 概述

这是维护人员诊断某些生成错误的页面.

## 问题

### `ld: internal error: atom not found in symbolIndex(__ZN10SQInstance3GetERK11SQObjectPtrRS0_) for architecture x86_64`

确切的原子可能是不同的.

这可能是由于过时的原因造成的.`-s`标记到链接器,并且可以像[这](https://github.com/Homebrew/legacy-homebrew/commit/7c9a9334631dc84d59131ca57419e8c828b1574b).
