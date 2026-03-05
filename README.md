# CSIS Format

> Common Student Information Structure 通用学生信息结构
>
> 版本 v0.1.0 | API 版本 1

CSIS 是一个基于 JSON 的 DSL，旨在为随机抽名、排位、积分等教学适用的与学生数据有交集的软件提供一个统一的交换格式。

CSIS 分为多个子语言，每个子语言都适用一类特定软件。它还提供一个通用格式，便于识别。

## CSIS Unified File

- 后缀名 | CSIS

对于以下子语言全部适配

## Common Student List Structure - 通用学生列表结构 CSLS

- 后缀名 | CSLS
- 适用
  - 随机抽名软件
  - 积分软件
  - 值日表软件
- 特性
  - 存储多个班级
  - 小组信息
  - 性别包容
  - 对于每个学生的额外信息
  
### 格式范例

> 注：没有标为必填的项目均为选填。

```json5
{
  "version": 1  // API 版本
  "students" :[
    {
      "name": str,  // 必填，学生名称
      "nickname": str,  // 昵称
      "group": str,  // 组别
      "gender": str,  // 性别（建议为'male', 'female'之一）
      // CSIS 格式制定组支持 LGBTQIA+ 群体，这就是为什么我们没有规定性别必须为这两个值之一。
      "number": int,  // 学号（大于 0 的整数（建议为连续的））
      "extra" : {...}  // 额外信息：您可以基于 CSLS 为您的应用程序制定信息存储格式
      // 若要添加更多信息，我们建议使用 CSAIS 作为格式。它具有更强的扩展性。
    },  // 单个学生
    ...
  ]
}
```

## Common Student Placing Structure - 通用学生座位表 CSPS

[TO BE COMPLETED]

## Common Student Additional Information Structure - 通用学生额外信息结构 CSAIS

[TO BE COMPLETED]