
# 重命名公式

有时需要重新命名软件和公式.重命名一个你需要的公式:

1.  将公式文件及其类重命名为新公式.新名称必须满足公式命名的所有常规规则.修正由于新公式比现有公式更严格的要求而可能发生的任何测试故障(即:`brew audit --strict`必须通过这个公式.

2.  创建一个拉请求到相应的TAP,删除旧的公式文件,添加新的公式文件,并将其添加到`formula_renames.json`使用提交消息`newack: renamed from ack`. 使用规范名称(例如)`ack`而不是`user/repo/ack`)

一`formula_renames.json`公式重命名的例子:

```json
{
  "ack": "newack"
}
```
