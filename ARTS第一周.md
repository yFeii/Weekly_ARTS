ARTS第一周，内容如下包括：算法，[Dynamic Linking On OS X](https://www.mikeash.com/pyblog/friday-qa-2012-11-09-dyld-dynamic-linking-on-os-x.html) Mike Ash 写的这篇关于 dyld 的博客, 关于Clang相关的命令，Mach-O格式<!--more-->
## Algorithm
[Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/)
## Review
[Dynamic Linking On OS X](https://www.mikeash.com/pyblog/friday-qa-2012-11-09-dyld-dynamic-linking-on-os-x.html) Mike Ash 写的这篇关于 dyld 的博客
### Static linking（ld）
发生在编译之后，源码转化为机器语言，所有的目标文件（Object File）被链接到一个二进制文件时
静态链接重要的原因：静态链接把符号引用转变成了间接符号查找，后续的dyld才能使用
#### ld has
1. 相似段合并（空间地址分配）
2. 替换所有命令（重定位）
3. 替换符号对应的真实地址（符号解析）  

经过静态链接之后，会生成完整的可执行文件。   
   
### dyld    

1. 通过系统内核，初始化一个简单的原始堆栈来运行自身（app）
2. 通过递归和缓存，加载所有可执行文件链接的动态库，到进程内存空间中
3. 将“non-lazy symbols(非惰性符号)” 链接到可执行文件内，并且为设置lazy表
4. Runs static initializers for the executable
5. 找到可执行文件的 main 函数，准备参数并调用
6. 在执行期间，通过绑定符号处理对 lazily-bound 符号存根的调用提供 runtime 动态加载服务（通过 dl*() 这个 API ），并为gdb和其它调试器提供钩子以获得关键信息
7. 程序main函数 return 后执行 static terminator
8. 某些场景下 main 函数结束后调 libSystem 的 _exit 函数

#### Bootstrap
当可执行文件 执行 <code>LC_LOAD_DYLINKER</code>这个命令时，<code>__dyld_start</code>将会被调用
#### Loading
把二进制文件映射到内存中，解析 <code>mach-o headers</code>，<code>LC_LOAD_DYLIB</code> 会返会 二进制文件的绝对路径，当包含（@executable_path，@loader_path，@rpath）会有相应的特殊处理
#### Linking
<code>lazy  symbols</code>的绑定将推迟到可执行文件首次调用该符号时
<code>non-lazy  symbols</code>的绑定将在其包含库加载后立即绑定。
二者实际的绑定过程是相同的； 唯一的区别在于该过程的触发方式。
#### Static initializers, static terminators, and runtime services
余下的便是一些环境的初始化（C ++对象的构造函数和Objective-C类的+ load方法），及返回main的地址，当app退出时同样由dyld返回终止符号。
## Tip

一些在学习编译需要知道的命令行及工具集
命令：

1. clang，这个都知道吧😸
2. nm，用来显示一个程序包的符号表, 默认会显示入口地址, 符号类型, 符号名
3. otool，针对目标文件的展示工具，用来发现应用中使用到了哪些系统库，调用了其中哪些方法等
4. gobjdump，查看目标文件或者可执行的目标文件的构成的gcc工具。

工具：

1. MachOView
2. hopper

## Share
[苹果机器学习工具](https://www.jianshu.com/p/a5ca26d296ba)
