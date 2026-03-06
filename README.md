# CSIS Format

> Common Student Information Structure 通用学生信息结构
>
> 版本 v0.1.0 | API 版本 1

CSIS 是一个基于 JSON 的 DSL，旨在为随机抽名、排位、积分等教学适用的与学生数据有交集的软件提供一个统一的交换格式。

CSIS 分为多个子语言，每个子语言都适用一类特定软件。它还提供一个通用格式，便于识别。

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
  "version": 1,  // API 版本
  "classes": [
    {
      "name": str,  // 必填，班级名称
      "class": int,  // 必填，班级号（如七 (1) 班的 1）
      "grade": int,  // 必填，年级
      "floor": int,  // 楼层 (从1开始)
      "building": str,  // 楼号
      "room": str,  // 房间号
      // 若您的班级房间号包括楼层/楼号信息，我们建议只填写房间号。
      "groups": [  // 组别
        {
          "name": str,  // 必填，小组名
          "tags": [str, ...],  // 标签（如荣誉获得等）
          "extra": {...}  // 额外信息
        }, ...
      ],
      "students": [  // 单个学生
        {
          "name": str,  // 必填，学生名称
          "nickname": str,  // 昵称
          "group": str,  // 组别，为外部 groups 字段中 name 之一
          "tags": [str, ...],  // 标签（如荣誉获得等）
          "gender": str,  // 性别（建议为'male', 'female'之一）
          // CSIS 格式制定组支持 LGBTQIA+ 群体，这就是为什么我们没有规定性别必须为这两个值之一。
          "number": int,  // 学号（大于 0 的整数（建议为连续的））
          "extra" : {...}  // 额外信息：您可以基于 CSLS 为您的应用程序制定信息存储格式
          // 若要添加更多信息，我们建议使用 CSAIS 作为格式。它具有更强的扩展性。
        }, ...
      ],
    }, ...
  ]
}
```

## Common Student Placing Structure - 通用学生座位表 CSPS

- 后缀名 | CSPS
- 适用
  - 座位排放软件
- 特性
  - 存储座位信息
  - 单个班级
  - 支持轮换设置
  - 支持“同桌”机制与同桌同时轮换

### 格式范例

> 当启用"同桌"时，每组同桌算为一个单元 (一列、一行)，同时在每个学生的单独配置中填写"deskmate_pos"项目

```json5
{
  "version": int,  // 必填，API 版本
  "rotation": {  // 轮换配置
    "enabled": bool,  // 必填，是否启用轮换
    "to_left": bool,  // 若启用轮换必填，(讲台为前) 是否是向左方轮换
    "cycle_days": int,  // 若启用轮换必填，轮换周期 (以天为单位)
    "cycle_in_columns": bool  // 若启用轮换必填，是否基于列轮换
  },
  "deskmate": bool,  // 启用同桌功能
  "students":[
    {
      "name": str,  // 必填，姓名
      "gender": str,  // 性别
      "deskmate_pos": str,  // 若启用同桌必填，同桌中的位置，必须为 "left"/"right" 之一
      "position": [int, int]  // 必填，以教师最左最靠近讲台的单位为原点，以向右为 +x 轴，以向远离讲台方向为 +y 轴，建立坐标系，并分别填写 x, y 坐标
    }, ...
  ]
}
```

## Common Student Additional Information Structure - 通用学生额外信息结构 CSAIS

[TO BE COMPLETED]
