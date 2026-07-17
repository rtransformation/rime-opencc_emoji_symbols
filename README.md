# Rime输入法Emoji与符号滤镜

## 最新更新（仅记录大更新）

| 日期 | 新增功能 |
|---|---|
| 2026.03.16 | 新增Unicode 17.0新增Emoji。 |
| 2024.07.30 | 新增iOS17.4更新的Emoji表情。 |
| 2023.06.12 | 新增iOS16.4更新的Emoji表情。 |
| 2022.10.17 | 新增Unicode 15.0 新增Emoji。 |
| 2022.03.15 | 新增iOS15.4更新的表情符号。 |
| 2020.04.06 | 新增Emoji13.0更新内容，各操作系统平台还未更新，所以可能会是乱码，不用在意。<br/>增加微信中对一些Emoji的中文释义，带中括号的词条，在微信中就可以直接上屏表情了。 |
| 2019.10.29 | iOS13.2的新增Emoji表情内容更新 |

## 项目介绍

利用OpenCC做的Emoji和特殊符号滤镜，供Rime输入法使用者使用。

基本包含Emoji的所有内容（包括同一人物类Emoji的5个不同肤色版本）。

## 使用方法

1. 下载项目，将`opencc/`目录放到Rime的“用户文件夹”内；

   例如对于小狼毫用户，这个文件夹应该是开始菜单中的“【小狼毫】用户文件夹”

2. 将`es_suggestion.yaml`内的内容(注意保留原始缩进)添加到自己正在使用的输入方案的`custom`文件中；

   例如对于智能ABC双拼方案用户，需要被修改的文件应该是`double_pinyin_abc.custom.yaml`

   *请不要修改方案的`.schema.yaml`文件，这些schema文件不应该用于用户级别自定义功能的用途*；

待文件就位后，使用Rime的“重新部署”功能，(例如对于小狼毫是右键点击托盘区输入法图标，在菜单中点击“重新部署”)，

在Rime输入法启用的情况下，通过`F4`进行管理并确认`es`已经启动，若显示`🈶️😀`就可以使用了。

### 修改`.custom.yaml`遇到问题？

请确认`switches/@next`、`'engine/filters/@before 0'`、`es_conversion`三项正确地归属于唯一的`patch`；

这要求：

此整个`.custom.yaml`文件中存在且仅存在唯一的一个在开头处缩进为0的`patch:`，

此三项上方没有任何此唯一`patch`以外的任何0缩进内容，

此三项自身具有正确的缩进——**2**个空格，

此三项的子项目，如`name` `simplifier@es_conversion`等具有**4**个空格；

## 关于`ocd2`的使用

二进制编译后的`ocd2`相比`txt`提供更好的性能表现，但缺少`txt`在修改方面的灵活性；

如果有性能方面的需求，请移步[OpenCC](https://github.com/BYVoid/OpenCC/releases)下载OpenCC的release package并进行安装；

假设终端处于`opencc`目录通过
```bash
opencc --help
```
获取帮助信息；

简单来说，对于本项目的“txt转ocd2”用途，所需的指令是：
```bash
opencc_dict -i /path/to/es.txt -o /path/to/rime/opencc/es.ocd2 -f text -t ocd2
```
**请将`/path/to/es.txt`与`path/to/rime/opencc/`替换为实际的路径**

之后，需要对Rime用户文件夹中的`opencc/es.json`做出如下修改：
```json
{
  "name": "Chinese to Emoji Symbol",
  "segmentation": {
    "type": "mmseg",
    "dict": {
      "type": "ocd2",
      "file": "es.ocd2"
    }
  },
  "conversion_chain": [{
    "dict": {
      "type": "ocd2",
      "file": "es.ocd2"
    }
  }]
}
```
文件修改完毕之后，使用重新部署功能。
