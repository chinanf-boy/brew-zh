
# 查询`brew`

*在本文档中,我们将使用[jq](https://stedolan.github.io/jq/)解析JSON,可以从自制程序中使用`brew install jq`.*

## 概述

`brew`提供从系统中获取公共信息类型的命令.`brew list`显示安装公式.`brew deps foo`显示依赖关系`foo`需要.

当然,包括外部命令在内的附加命令可以被写入以提供更详细的信息.这里有两个缺点.首先,它意味着编写Ruby反对可能改变的自制代码库.在重构期间会有更多的代码要接触,而自制程序不能保证外部命令继续工作.第二,它意味着设计命令本身,指定输入参数和输出格式.

为了让用户能够在没有上面的问题的情况下进行丰富的查询,自制程序提供了`brew info`命令.

## `brew info --json`

`brew info`输出关于公式的JSON格式化信息.然后可以使用您选择的工具解析此JSON.

从MangPo:

-   `info --json=<version> (--all|--installed|<formulae>)`打印一个JSON表示`<formulae>`. 目前唯一接受的价值`<version>`是`v1`.

    通过`--all`获取所有公式的信息,或`--installed`获取所有安装公式的信息.

当前模式版本是`v1`. 注意,在不增加架构的情况下,可以根据需要将字段添加到架构中.任何重大的更改都会导致架构版本的更改.

架构本身目前不在生成它的代码之外记录:[公式Tyth-THOHASH](https://github.com/Homebrew/brew/blob/master/Library/Homebrew/formula.rb)

## 实例

*JSON输出的顶层元素总是一个数组,所以`map`运算符用于对数据进行操作.*

### 漂亮的打印一个公式的信息

```sh
brew info --json=v1 tig | jq .
```

### 安装公式

显示关于所有已安装公式的完整JSON信息:

```sh
brew info --json=v1 --all | jq "map(select(.installed != []))"
```

你会注意到,处理所有公式都是慢的,让它更快.`brew`这样做:

```sh
brew info --json=v1 --installed
```

### 只连接KEG公式

一些公式被标记为"仅KEG",这意味着已安装的文件没有链接到共享.`bin`,`lib`目录等,这样做会引起冲突.这样的公式可以强制链接到共享目录,但不建议这样做(并且将导致).`brew doctor`抱怨)

只查找链接KEG公式的名称:

```sh
brew info --json=v1 --installed | jq "map(select(.keg_only == true and .linked_keg != null) | .name)"
```

### 非连接正规公式

查找已安装但未链接到共享目录的正常(不含KEG)公式的名称:

```sh
brew info --json=v1 --installed | jq "map(select(.keg_only == false and .linked_keg == null) | .name)"
```

## 啤酒配方

有一个[文档化的JSONAPI](https://formulae.brew.sh/docs/api/)提供访问`brew info --json=v1`输出,不需要进入自制程序.

## 结语

使用JSON输出,可以针对Homebrew进行查询,而不必理解Homebrew的Ruby内部信息,从而减少由于Homebrew代码更改而导致中断的风险.

如果JSON输出没有提供它应该提供的一些信息,请提交一个请求,最好带有一个补丁来添加所需的信息.
