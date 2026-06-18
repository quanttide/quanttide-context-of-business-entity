# 领域

完全可以。name（短名）、long-name（长名）、label 这三个字段，就是你需要的设计方案。

对应关系非常清晰：

字段 示例 用途
name think 代码仓库、内部枚举、配置文件 key
long-name cognitive-engineering 文档仓库、API 路径、外部系统标识
label 认知工程 UI 展示、用户可见名称

注意事项：

· long-name 在代码中建议写成 LongName（C# 属性命名约定，不用连字符）
· 三个字段都是值对象的相等性组成部分
· 不要设置“默认 name”，让调用方按上下文主动选择 name 或 long-name

这个命名方式比 ShortName/FullName 更直白地表达了“一短一长”的意图，推荐采用。
