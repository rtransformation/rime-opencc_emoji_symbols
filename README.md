项目介绍
利用OpenCC做的Emoji和特殊符号滤镜，供Rime输入法使用者使用。 基本包含Emoji 11.0的所有内容（同一人物类Emoji的不同肤色仅保留一个）。

使用方法
将es.txt和es.json放入Rime输入法的opencc文件夹下。 在你所使用的方案的xxxx.schema.yaml文件的相应位置加入如下代码（注意缩进）：

`
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
`

加入后重新部署，就可以使用了。
