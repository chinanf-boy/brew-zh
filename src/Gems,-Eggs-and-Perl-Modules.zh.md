
# 宝石、蛋和Perl模块

在一个新的MACOS安装上,有三个空目录供所有用户使用:

```
/Library/Ruby
/Library/Python
/Library/Perl
```

从OS X狮子(10.7)开始,你需要`sudo`像这样安装到:`sudo gem install`,`sudo easy_install`或`sudo cpan -i`.

避免SUDO的选项是使用访问控制列表:`chmod +a 'user:YOUR_NAME_HERE allow add_subdirectory,add_file,delete_child,directory_inherit' /Library/Python/3.y/site-packages`例如,将允许您将包添加到Python 3.Y作为自己.这可能比更改目录的组所有权更安全.

### 那我为什么要使用SUDO呢?

习惯也许?

原因之一是可执行文件进入`/usr/local/bin`. 通常这不是可写的位置.但是如果你按照我们的建议安装自制软件,`/usr/local`将没有SUDO可写.所以现在你可以在不使用SUDO的情况下安装你需要的开发工具.

## 没有SUDO的Python软件包(蛋)

而不是改变权利`/Library/Python`我们建议以下选项:

### 用酿造的蟒蛇

注:`easy_install`被贬低.我们安装`pip`(或)`pip2`对于Python 2)以及Python/Python 2.

我们建立了这样的ditutul`pip install`总是将模块放入`$(brew --prefix)/lib/pythonX.Y/site-packages`和脚本`$(brew --prefix)/share/python`. 所以,你不需要SUDO!

做`brew info python`或`brew info python@2`有关路径的精确信息.注意,一个酿造的Python仍然在搜索模块.`/Library/Python/X.Y/site-packages`而且在`~/Library/Python/X.Y/lib/python/site-packages`.

### 使用系统的Python

*这只是建议如果你**不要**使用酿造的蟒蛇.*

关于MaOS,任何[Python版本X.Y也在搜索`~/Library/Python/X.Y/lib/python/site-packages`对于模块](https://docs.python.org/2/install/index.html#inst-alt-install-user). DIR可能还不存在,但你可以创建它:

```sh
mkdir -p ~/Library/Python/2.7/lib/python/site-packages
```

教`easy_install`和`pip`要在那里安装,请使用`--user`切换或创建`~/.pydistutils.cfg`文件内容如下:

```
[install]
install_lib = ~/Library/Python/$py_version_short/lib/python/site-packages
```

### 使用VimaLeNV——与Burw和Python的Python一起工作

[虚拟现实](http://www.virtualenv.org/en/latest/)船舶`pip`并使用单独的站点包创建孤立的Python环境,因此不需要SUDO.

## 无SUDO的RuuGyMS

**如果你使用RBEV或RVM,那么你应该忽略这些东西.**

酿造的Ruby安装可执行文件`$(brew --prefix)/opt/ruby/bin`没有SUDO.你应该把这个添加到你的路径中.请参阅`ruby`最新信息公式.

### 随着系统的红宝石

使红宝石安装到`/usr/local`我们需要补充`gem: -n/usr/local/bin`对你`~/.gemrc`. 它是YAML,所以手动或使用它:

```sh
echo "gem: -n/usr/local/bin" >> ~/.gemrc
```

**然而,1.3.6之前的所有版本的RuGuEMS都是马车.**并且忽略上述设置.遗憾的是,Snow Leopard的新安装有1.3.5.目前唯一已知的方法是将RuuGEMS升级为根:

```sh
sudo gem update --system
```

### 另一种选择

只需将所有东西安装到自制程序的前缀中:

```sh
echo "export GEM_HOME=\"$(brew --prefix)\"" >> ~/.bashrc
```

### 不管用!当我尝试安装东西时,我得到一些"权限"错误!

*注意,也许你不应该在狮子身上这样做,因为苹果公司已经确定它不是一个好的默认.*

如果你曾经做过`sudo gem`等之前,许多文件将被创建的根拥有.固定:

```sh
sudo chown -R $USER /Library/Ruby /Library/Perl /Library/Python
```

## 没有SUDO的Perl CPAN模块

Perl模块`local::lib`与RBEV/RVM类似(虽然仅用于模块,而不是Perl安装).只会污染你的简单解决方案`/Library/Perl`稍加安装[`local::lib`](https://metacpan.org/pod/local::lib)与SUDO:

```sh
sudo cpan local::lib
```

注意,这将安装一些其他类似的依赖项.`Module::Install`. 然后在你的壳牌的启动中放置适当的咒语,例如`.bash_profile`你插入下面,其他人看到[`local::lib`](https://metacpan.org/pod/local::lib)博士学位.

```sh
eval $(perl -I$HOME/perl5/lib/perl5 -Mlocal::lib)
```

现在(在重新启动外壳之后)`cpan`或`perl -MCPAN -eshell`等将安装模块和二进制文件`~/perl5`相关子目录将在您的`PATH`和`PERL5LIB`等.

### Perl完全避免SUDO

如果你甚至不想(或不能)使用SUDO进行引导`local::lib`只需手动安装即可`local::lib`在里面`~/perl5`并添加相关路径`PERL5LIB`在巴斯克王朝的咒语之前.

另一种选择是使用.`perlbrew`在你的家庭目录中安装一个单独的Perl拷贝,或者在任何你喜欢的地方安装:

```sh
curl -L https://install.perlbrew.pl | bash
perlbrew install perl-5.16.2
echo ".~/perl5/perlbrew/etc/bashrc" >> ~/.bashrc
```
