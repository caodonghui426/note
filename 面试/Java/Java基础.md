# 1.Java程序运行的步骤
1. 首先编写Java程序，如HelloWorld.java。
2. 然后使用javac进行编译，得到Helloworld.class。
3. 最后使用java进行运行。
# 2.JDK、JRE、JVM
当谈到Java开发时，以下三个术语经常被提及：JDK（Java Development Kit）、JVM（Java Virtual Machine）和JRE（Java Runtime Environment）。它们在Java开发和执行过程中扮演不同的角色，它们之间的关系如下：
JDK（Java Development Kit）是Java开发工具包。它是开发Java应用程序所需的核心组件集合。JDK包括了Java编译器（javac）、Java运行时环境（JRE）、开发工具和Java类库（Java API）。JDK提供了开发Java应用程序所需的所有工具和资源。
JVM（Java Virtual Machine）是Java虚拟机。它是Java程序的运行环境，负责将Java字节码（由Java源代码编译而来）转换为机器码并执行。JVM是跨平台的关键，它使得Java程序可以在不同的操作系统上运行，只要有相应的JVM实现即可。JVM还提供了内存管理、垃圾回收等功能，使得Java程序具有高度的可移植性和安全性。
JRE（Java Runtime Environment）是Java运行时环境。它是JVM的一部分，包含了JVM和Java类库（Java API）。JRE提供了Java程序运行所需的所有基础类库和运行时支持，但不包括开发工具（如编译器）。如果你只需要运行Java程序而不是进行开发，那么安装JRE就足够了。
它们之间的关系可以用以下方式表示：
JDK = JRE + 开发工具
JRE = JVM + Java类库
简而言之，JDK是开发Java应用程序所需的工具包，包括JRE和开发工具；JRE是运行Java程序所需的运行时环境，包括JVM和Java类库；而JVM是Java程序的执行环境，负责将Java字节码转换为机器码并执行。
