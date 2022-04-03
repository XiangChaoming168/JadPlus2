# JadPlus2
first commit

# 设置选项
除 mpm 和 urc 外，值 1 表示该选项已激活，0 - 禁用。默认值（如果有）在括号之间给出。

通常，以下选项将由用户更改（如果有）：hes、hdc、dgs、mpm、ren、urc 其余选项可以保持不变：它们针对专业逆向工程师。

- rbr (1): 隐藏桥接方法
- rsy (0): 隐藏合成类成员
- din(1)：反编译内部类
- dc4 (1): 折叠 1.4 类引用
- das (1): 反编译断言
- hes (1): 隐藏空的超级调用
- hdc(1)：隐藏空的默认构造函数
dgs (0): 反编译通用签名
ner (1): 假设 return 不抛出异常
den (1): 反编译枚举
rgn (1): 删除 getClass() 调用，当它是合格的新语句的一部分时
lit（0）：输出数字文字“as-it原样”
asc (0)：将字符串和字符文字中的非 ASCII 字符编码为 Unicode 转义
bto (1): 将 int 1 解释为 boolean true（编译器错误的解决方法）
nns (0)：允许不设置合成属性（编译器错误的解决方法）
uto (1)：将无名类型视为 java.lang.Object（编译器架构缺陷的解决方法）
udv (1)：根据调试信息重建变量名，如果存在的话
ump (1): 从对应的属性中重构参数名称，如果存在的话
rer (1): 删除空异常范围
fdi (1): de-inline finally 结构
mpm (0)：每个反编译方法允许的最大处理时间，以秒为单位。0 表示没有上限
ren (0)：重命名模棱两可的（或混淆的）类和类元素
urc (-)：用户提供的实现 IIdentifierRenamer 接口的类的全名。它用于确定应该重命名哪些类标识符并提供新的标识符名称（请参阅“重命名标识符”）
inn (1)：检查 IntelliJ IDEA 特定的 @NotNull 注释，如果找到则删除插入的代码
lac (0): 将 lambda 表达式反编译为匿名类
nls (0)：定义用于输出的换行符。0 - '\r\n' (Windows)，1 - '\n' (Unix)，默认取决于操作系统
ind：缩进字符串（默认为 3 个空格）
log (INFO)：一个日志级别，可能的值是 TRACE、INFO、WARN、ERROR

重命名标识符
一些混淆器给类及其成员元素提供简短、无意义且最重要的是模棱两可的名称。重新编译此类代码会导致大量冲突。因此，建议让反编译器轮流重命名元素，确保每个标识符的唯一性。

选项“ren”（即 -ren=1）激活重命名功能。默认重命名策略如下：

如果元素名称是保留字或短于 3 个字符，则重命名元素
新名称是根据一个简单的模式构建的： (class|method|field)_<consecutive unique number>
您可以通过提供您自己的实现来覆盖此规则，方法是在重命名时提供反编译器调用的 4 个关键方法。只需将在选项“urc”（例如 -urc=com.example.MyRenamer）中实现 org.jetbrains.java.decompiler.main.extern.IIdentifierRenamer 的类传递给 Fernflower。该类必须在应用程序类路径上可用。
从命名上应该清楚每个方法的含义：toBeRenamed 决定元素是否会被重命名，而其他三个分别为类、方法和字段提供新的名称。
