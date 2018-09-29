
# 瓶(二元包装)

瓶子是通过安装配方来生产的.`brew install --build-bottle <formula>`然后装瓶`brew bottle <formula>`. 这将输出应该插入公式文件的瓶子DSL.

## 用法

如果一个瓶子是可用的,它将被下载并自动倾倒当你`brew install <formula>`. 如果你想禁用这个,你可以通过指定`--build-from-source`.

如果用户请求它(见上文),如果公式要求它,则不使用瓶子.`pour_bottle?`如果在安装过程中指定了任何选项(瓶子都用默认选项编译),如果瓶子不是最新的(例如,缺少校验和),或者如果瓶子的`cellar`不是`:any`也不等于电流`HOMEBREW_CELLAR`.

## 创造

瓶子是用[酿造试验机器人](Brew-Test-Bot.md). 这主要发生在人们向家庭和家庭提出请求的时候.`bottle do`块维护时更新`brew pull --bottle`拉请求的内容.对于自制软件的龙头,它们被上传到下载.[双托盘](https://bintray.com/homebrew).

默认情况下,瓶子将为您正在构建的OS/体系结构支持的最老的CPU构建(64位OS的核心2).这确保瓶子与所有你可以分发的电脑兼容.如果你*真的?*希望你的瓶子被其他东西优化,你可以通过`--bottle-arch=`构建另一架构的选项——例如,`brew install foo --bottle-arch=penryn`. 请记住,如果您为更新的架构构建,您的一些用户可能会得到他们无法运行的二进制文件,那将是令人遗憾的!

## 格式

瓶子是编译后的二进制文件的简单gpip.任何元数据都存储在公式的瓶子DSL和瓶子文件名(即MACOS版本,修订版)中.

## 瓶DSL(领域特定语言)

瓶子有一个DSL用于公式中,它包含在`bottle do ... end`块.

一个简单的(典型的)例子:

```ruby
bottle do
  sha256 "4921af80137af9cc3d38fd17c9120da882448a090b0a8a3a19af3199b415bfca" => :sierra
  sha256 "c71db15326ee9196cd98602e38d0b7fb2b818cdd48eede4ee8eb827d809e09ba" => :el_capitan
  sha256 "85cc828a96735bdafcf29eb6291ca91bac846579bcef7308536e0c875d6c81d7" => :yosemite
end
```

一个完整的例子:

```ruby
bottle do
  root_url "https://example.com"
  prefix "/opt/homebrew"
  cellar "/opt/homebrew/Cellar"
  rebuild 4
  sha256 "4921af80137af9cc3d38fd17c9120da882448a090b0a8a3a19af3199b415bfca" => :sierra
  sha256 "c71db15326ee9196cd98602e38d0b7fb2b818cdd48eede4ee8eb827d809e09ba" => :el_capitan
  sha256 "85cc828a96735bdafcf29eb6291ca91bac846579bcef7308536e0c875d6c81d7" => :yosemite
end
```

### 根地址`root_url`)

可选地包含用于计算瓶子URL的URL根目录.默认情况下,这将被省略,使用自制的默认瓶子URL根.这可能是有用的抽头,希望提供瓶的公式或迎合非违约.`HOMEBREW_CELLAR`.

### 地窖(地下室)`cellar`)

可选地包含值`HOMEBREW_CELLAR`瓶子是在其中建造的.大多数编译软件包含对其编译位置的引用,因此不能简单地重新定位磁盘上的任何位置.如果这个值是`:any`或`:any_skip_relocation`这意味着瓶子可以安全地安装在任何地窖中,因为它不包含任何关于它的安装地窖的参考.如果一个瓶子被编译(缺省的所有自制程序都是默认的),则可以省略这一点.`HOMEBREW_CELLAR`属于`/usr/local/Cellar`.

### 前缀(前缀)`prefix`)

可选地包含值`HOMEBREW_PREFIX`瓶子是在其中建造的.见描述`cellar`. 什么时候?`cellar`是`:any`或`:any_skip_relocation`前缀应该省略.

### 重建版本`rebuild`)

可选地包含瓶子的重建版本.有时瓶子可能需要更新而不碰撞公式的版本,例如应用了一个新的补丁.在这种情况下,重建将具有1或更多的值.

### 校验和`sha256`)

包含一个特定版本的MACOS的瓶子的SAH256散列.

## 公式DSL

另外,在公式DSL中有一种方法可用.

### 倒瓶`pour_bottle?`)

可选地返回一个布尔值来决定这个公式是否应该使用一个瓶子.例如,如果使用非默认选项编译了另一个公式,则瓶子可能会中断,因此此方法可以检查这种情况并返回`false`.

一个完整的例子:

```ruby
pour_bottle? do
  reason "The bottle needs the Xcode CLT to be installed."
  satisfy { MacOS::CLT.installed? }
end
```
