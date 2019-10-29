最新更新
2019.10.29 iOS13.2新增Emoji内容更新

项目介绍
利用OpenCC做的Emoji和特殊符号滤镜，供Rime输入法使用者使用。 基本包含Emoji 12.0的所有内容（包括同一人物类Emoji的5个不同肤色版本）。

使用方法
将es.txt和es.json放入Rime输入法的opencc文件夹下。 在你所使用的方案的xxxx.schema.yaml文件的相应位置加入如下代码（注意缩进）：

```
switches:
  - name: show_es
    reset: 1
    states: [ 😔, 😀 ]

engine:
  filters:
    - simplifier@es_conversion

es_conversion:
  opencc_config: es.json
  option_name: show_es
```

加入后重新部署，就可以使用了。
