
# 版本

既然[自制/版本](https://github.com/homebrew/homebrew-versions)已经被贬低,[自制/核心](https://github.com/homebrew/homebrew-core)用新的命名格式支持公式的多个版本.

在[自制/版本](https://github.com/homebrew/homebrew-versions)GCC 6的公式命名为`gcc6.rb`然后开始`class Gcc6 < Formula`. 在[自制/核心](https://github.com/homebrew/homebrew-core)这个公式叫做`gcc@6.rb`从开始`class GccAT6 < Formula`.

## 可接受版本公式

我们包含的版本公式[自制/核心](https://github.com/homebrew/homebrew-core)必须符合以下标准:

-   版本化软件应该建立在所有自制的MaOS支持的版本上.
-   版本公式在主/次(非补丁)版本与当前稳定版本中应该有所不同.这是因为补丁版本表示错误或安全更新,我们希望确保应用安全更新.
-   上游应该有一个版本化的公式版本的发布分支,并在必要时仍然对该版本进行安全更新.例如,[PHP 5.5不是支持版本,但PHP 7.2是](http://php.net/supported-versions.php)2018年1月
-   依赖于版本化公式的公式在其递归依赖性中不得两次依赖于两个不同版本的相同公式.例如,如果你依赖`openssl@1.0`和`foo`和`foo`取决于`openssl`那么你必须使用`openssl`.
-   如果上游项目提供支持,例如,使用后缀二进制文件,则版本化的公式应该只能与非版本化的公式同时可链接.如果这是不可能的,使用`keg_only :versioned_formula`允许用户同时安装多个版本.
-   一`keg_only :versioned_formula`不应该`post_install`任何东西`HOMEBREW_PREFIX`与非版本对应的(或其他版本的公式)冲突或复制.例如,A`node@6`公式不应该安装它的`npm`进入之内`HOMEBREW_PREFIX`像`node`公式可以.
-   提交的公式应被许多人预期使用.如果这种情况消失了,它们将被移除.我们的目标是不删除那些[前3000名`install_on_request`公式](https://brew.sh/analytics/install-on-request/).
-   版本化公式不应该有`resource`需要安全更新的S.例如,A`node@6`公式不应该有`npm`资源,而是依赖于`npm`由上游塔球提供.
-   版本化的公式应该尽可能相似,对不可逆公式是敏感的.创建或更新版本化的公式应该是询问未版本化的公式问题的机会,例如,是否可以删除或默认一些未使用或无用的选项?
-   在任何给定时间,无论使用何种方式,都不支持超过五个版本的公式(包括非版本的公式).当删除公式违反这一点,我们将这样做的基础上使用和支持地位,而不是年龄.

HOBBURW的版本不打算用于您个人对项目所需的任何旧版本.你应该创造你自己[水龙头](How-to-Create-and-Maintain-a-Tap.md)对于公式,您或您的组织希望控制不符合上述标准的版本或版本.具有常规API或ABI中断版本的软件仍然需要满足以上所有要求;`brew upgrade`为你打破一些东西并不是我们为你增加和维持一个公式的理由.

如果有一个公式当前存在于Homebrew/homebrew-core存储库中,或者已经存在于过去(即,已经迁移或删除),那么可以通过`brew extract`命令.这将将公式的期望版本复制到自定义抽头中.例如,如果项目依赖于`automake`1.12,而不是最新版本,您可以获得`automake`版本1.12的运行公式`brew extract automake $YOUR_GITHUB_USER/$YOUR_TAP_REPOSITORY_NAME --version=1.12`. 通过这种方式得到的公式可以使用已弃用、禁用或删除的自制语句(例如校验和).`sha1`而不是校验和`sha256`;`brew extract`命令不编辑或更新公式,以满足目前的标准和风格要求.

我们可以暂时为我们自己的需求添加不符合这些标准的版本公式.[自制/核心](https://github.com/homebrew/homebrew-core). 那里存在版本化的公式并不意味着它将被无限期地维护,或者我们愿意接受任何不符合上述要求的版本.
