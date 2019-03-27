# SEUITE 文档格式快速指南

本指南对于所有SEUITE文档均起效，对于文档内的特殊要求，以文档内为准。

- 关键字 "必须"，"禁止"，"被要求"，"应当"，"不应"，"推荐"，"可以"，"可选" 均遵循[RFC 2119](http://tools.ietf.org/html/rfc2119)要求：

    - 必须, or "被要求"：表示绝对要求这样做

    - 禁止：表示绝对不要求这样做

    - 应当, or "推荐"：表示一般情况下应该这样做，但是在某些特定情况下可以忽视这个要求

    - 不应, or "不推荐"： 表示一般情况下不应该这样做，但是在某些特定情况下可以忽视这个要求
    
    - 可以, or "可选的"：表示这个要求完全是可选的，你可以这样做，也可以不这样做

    - 详情参考[SEUITE文档格式规范](https://docs.seu.services/#/Reference/SEUITEDocReference#)中对[RFC2119](https://docs.seu.services/#/Reference/SEUITEDocReference#SEUITE中对RFC2119使用的解释)的相关说明

- 标点符号的使用

    - 以下标点符号**必须**使用半角符号
        - 单引号 ' 和双引号 "
        - 中括号 [ ]

    - 标点符号之间不应加上空格

    - 同一内容块中的同一标点符号应格式一致

    - 代码块中**禁止**使用全角符号，其余部分参考[代码规范]中的内容

    - 详情参考[SEUITE文档格式规范](https://docs.seu.services/#/Reference/SEUITEDocReference#)中对[标点符号使用](https://docs.seu.services/#/Reference/SEUITEDocReference#标点符号的使用)的相关说明

- 版本号的使用与版本控制均遵循[语义化版本控制规范2.0](/Reference/SemVerReference)的要求
    - 版本号由 `主版本号.次版本号.修订号(补充信息)` 构成，其中

        - 主版本号：当你做了不兼容的 API 修改

        - 次版本号：当你做了向下兼容的功能性新增

        - 修订号：当你做了向下兼容的问题修正

        - 先行版本号及版本编译信息将加到版本号的末尾，作为延伸及补充信息

    - 标记版本号的软件发行后，**禁止**改变该版本软件的内容，任何修改都**必须**以新版本发行

    - 主版本号为零（0.y.z）的软件处于开发初始阶段，一切都可能随时被改变

    - 详情参考[SEUITE文档格式规范](https://docs.seu.services/#/Reference/SEUITEDocReference#)中对[版本管理](https://docs.seu.services/#/Reference/SEUITEDocReference#版本管理)的相关说明