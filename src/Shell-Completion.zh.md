
# 自制外壳完成

自制程序附带完成定义`brew`命令.一些包还为自己的程序提供完成定义.

`zsh`,`bash`和`fish`目前支持.(自制)提供`brew`完井`zsh`和`bash`;`fish`提供它自己的`brew`完成.

必须配置外壳才能完成完成支持.这是因为自制的管理完成被存储在下面.`HOMEBREW_PREFIX`,您的系统外壳可能不知道,因为它很难自动配置.`bash`和`zsh`以一种健壮的方式完成,所以家庭安装程序不能为你做.

## 配置完成`bash`

让自制啤酒的完工`bash`必须将定义定义为shell启动的一部分.向您添加以下内容`~/.bashrc`文件:

```sh
if type brew 2&>/dev/null; then
  for completion_file in $(brew --prefix)/etc/bash_completion.d/*; do
    source "$completion_file"
  done
fi
```

## 配置完成`zsh`

让自制啤酒的完工`zsh`您必须在自己的网站上获得自制的ZSH站点功能.`$FPATH`初始化之前`zsh`完成设施.向您添加以下内容`~/.zshrc`文件:

```sh
if type brew &>/dev/null; then
  FPATH=$(brew --prefix)/share/zsh/site-functions:$FPATH
fi
```

这必须先做.`compinit`被称为.(注意:如果你使用OH我的ZSH,它会呼叫`compinit`为了你,所以在你打电话之前必须这样做`oh-my-zsh.sh`)

你也可能需要强行重建.`zcompdump`:

```sh
  rm -f ~/.zcompdump; compinit
```

此外,如果在尝试加载这些完成时收到"zsh compinit:insesafetdirectories"警告,则可能需要运行以下命令:

```sh
  chmod go-w "$(brew --prefix)/share"
```

## 配置完成`fish`

不需要配置`fish`. 友好!
