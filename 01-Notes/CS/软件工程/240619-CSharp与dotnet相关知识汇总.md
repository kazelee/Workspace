### ASP.NET

（菜鸟教程部分）

Web Pages（Web 页面）、MVC（Model View Controller 模型-视图-控制器）、Web Forms（Web 窗体）

【Web Pages 单页面模式】
- 最简单的 ASP.NET 模式。  
- **与 PHP 和经典 ASP 相似**。  
- 内置了数据库、视频、图形、社交媒体等模板和帮助器。

🔺Razor 帮助器（`@`引导关键字等代码；`@{}`包裹代码块）

⭐【MVC 模型-视图-控制器】
- MVC 将 Web 应用程序分成 3 个不同的组成部分：  
	- 模型负责数据  
	- 视图负责显示 
	- 控制器负责输入  

【Web Forms 事件驱动模式】（大致略过）
- 传统的 ASP.NET 事件驱动开发模式：  
- 带有服务器控件、服务器事件和服务器代码的网页。

其他参考：[ASP.NET Core 基础教程 - ASP.NET Core 基础教程 - 简单教程，简单编程](https://www.twle.cn/l/yufei/aspnetcore/dotnet-aspnet-index.html)（本站的 [ASP.NET](https://www.twle.cn/l/yufei/aspnet/aspnet-basic-index.html) 有些凌乱，也随着 .NET Core 的发布而变得越来越过时了；从 .NET Core 发布那刹那开始，就开始宣告 ASP.NET 已经迈入了尾声）

### ASP.NET Core

- [ASP.NET Core 基础教程 - ASP.NET Core 基础教程 - 简单教程，简单编程](https://www.twle.cn/l/yufei/aspnetcore/dotnet-aspnet-index.html)
- ⭐[AspNetCore-Developer-Roadmap/ReadMe.zh-Hans.md at master · MoienTajik/AspNetCore-Developer-Roadmap](https://github.com/MoienTajik/AspNetCore-Developer-Roadmap/blob/master/ReadMe.zh-Hans.md)

ASP.NET Core 允许我们优化应用程序，只包含必要的 NuGet 包

进阶参考：[ASP.NET Core 基础教程总结 - ASP.NET Core 基础教程 - 简单教程，简单编程](https://www.twle.cn/l/yufei/aspnetcore/dotnet-aspnet-summary.html)（推荐《ASP.NET Core 跨平台开发从入门到实战》这本书）

[.NET Core 资料精选：入门篇 - 滴答的雨 - 博客园](https://www.cnblogs.com/heyuquan/p/dotnet-basic-learning-resource.html)（部分链接遗失）

微软官方文档相关：
- [ASP.NET 文档 | Microsoft Learn](https://learn.microsoft.com/zh-cn/aspnet/core/?view=aspnetcore-8.0)
- [浏览所有课程、学习路径和模块 - Training | Microsoft Learn](https://learn.microsoft.com/zh-cn/training/browse/)
- [总结 - Training | Microsoft Learn](https://learn.microsoft.com/zh-cn/training/modules/create-razor-pages-aspnet-core/7-summary)（ASP.NET示例）
- [总结 - Training | Microsoft Learn](https://learn.microsoft.com/zh-cn/training/modules/get-started-with-web-development/7-summary)（Web UI相关）

### LINQ（略）

官方文档：[System.Linq 命名空间 | Microsoft Learn](https://learn.microsoft.com/zh-cn/dotnet/api/system.linq?view=net-8.0)
过去常用：All、Any、Select、Where；ToArray、Reverse、Distinct

强调：Select是对每个元素做变换，Where才是根据布尔表达式做筛选
吐槽：语法糖，简化代码编写，对于项目开发/宏观视角而言意义不大
补充：[F#奇妙游（1）：F#浅尝 - 知乎](https://zhuanlan.zhihu.com/p/640311160)（02年就开始研发的奇葩语言）

### SOLID

链接：[单一责任原则 （C#） |DotNetCurry的](https://www.dotnetcurry.com/software-gardening/1148/solid-single-responsibility-principle)

- 单一责任原则（SRP，**S**ingle Responsibility）
	- 一个类只做一件事
	- 示例：CsvFileProcessor
		- 初版：1个CsvFileProcessor类，1个Process方法
			- 实际做了三件事：①读取 CSV 文件；②解析 CSV 文件；③存储数据
		- 改进1：将Process方法细分为①ReadCsv；②ParseCsv；③StoreCsv
			- 这三个方法分别完成不同工作，在Process方法中依次调用
			- 问题：StoreCsvData引入了额外的解析
			- 解决：为数据添加DTO（Store部分无需解析，直接访问属性）
		- 改进2：使用接口和DTO类重构代码
			- 声明三个接口，分别处理读取、解析、存储模块
			- ContactProcessor的Process函数参数接收三个接口
			- 编写三个类实现接口，编写DTO类属性
			- 实际使用时，调用Process函数并调用具体的接口
			- 好处：后续其他格式文件解析也可以复用此逻辑
- 开放封闭原则（OCP，[**O**pen/Closed](https://www.dotnetcurry.com/software-gardening/1176/solid-open-closed-principle)）
	- 扩展模块的行为不会影响原代码修改
	- 使用SRP的接口方法，用接口实现类替代switch条件判断语句
- 里氏替换原则（LSP，[**L**iskov Substitution](https://www.dotnetcurry.com/software-gardening/1235/liskov-substitution-principle-lsp-solid-patterns)）
	- _子类型必须可替代其基本类型_
	- 参考：[设计模式—里氏替换原则 - 知乎](https://zhuanlan.zhihu.com/p/668593015)
	- **子类可以扩展父类的功能，但不能改变父类原有的功能**（继承有较大限制）
	- 参考2：[七大原则——里氏替换原则\_里氏原则-CSDN博客](https://blog.csdn.net/m0_37654408/article/details/105423543)
- 接口隔离原则（ISP，[**I**nterface Segregation](https://www.dotnetcurry.com/software-gardening/1257/interface-segregation-principle-isp-solid-principle)）
	- 多接口细分功能，针对不同的类选择需要的接口实现
- 依赖反转原则（DIP，[**D**ependency Inversion](https://www.dotnetcurry.com/software-gardening/1284/dependency-injection-solid-principles)）
	- **依赖关系注入**（DI）：代码中不要有太多依赖项
	- 通过接口分离BC：A(B), B(C) => A(B(C)), B(IC), C:IC
	- 案例：把对 _InjectionContext_ 的依赖换成了对 _CustomerService_ 的依赖

### JSON

System.Text.Json：[如何在 C# 中序列化 JSON - .NET | Microsoft Learn](https://learn.microsoft.com/zh-cn/dotnet/standard/serialization/system-text-json/how-to)
Newtonsoft.Json：[C# 读写 JSON 文件全攻略：详尽代码示例与注释解析\_c# json-CSDN博客](https://blog.csdn.net/z_344791576/article/details/137854878)

序列化：建立结构类可以设置【属性】实现json字段与变量名不同等功能）
反序列化：利用数据类和泛型Deserialize（依赖数据类的方法）

不依赖类的方法：动态组装与动态解析
- [如何在 System.Text.Json 中使用 JSON DOM - .NET | Microsoft Learn](https://learn.microsoft.com/zh-cn/dotnet/standard/serialization/system-text-json/use-dom)
- [c#： Newtonsoft.Json 高级用法一（不创建类，动态解析和构造json、JObject/JArray）\_c# newtonsoft.json-CSDN博客](https://blog.csdn.net/u010476739/article/details/120240346)

补充：Json.Net就是Newtonsoft.Json，但后者在Godot中使用会有问题

### EF Core

[Entity Framework Core 概述 - EF Core | Microsoft Learn](https://learn.microsoft.com/zh-cn/ef/core/)
用作对象关系映射程序 (O/RM)

参考：[EFCore 6.0入门看这篇就够了 - Mamba24⁸ - 博客园](https://www.cnblogs.com/Mamba8-24/p/16098812.html)
[.NETCore Entity Framework（ef）学这一篇就够了 - 基础知识（上篇）\_netcore ef-CSDN博客](https://blog.csdn.net/yiquan_yang/article/details/111589972)；[不会使用 EF Core 的 Code First 模式？来看看这篇文章，手把手地教你 - 代码掌控者 - 博客园](https://www.cnblogs.com/JackyGz/p/17931042.html)；[EF Core 筆記 1 - 概論-黑暗執行緒](https://blog.darkthread.net/blog/efcore-notes-1/)

### 其他补充

- Swagger：[C#Swagger的创建和使用\_c# swagger-CSDN博客]；[.NET Core WebAPI中使用Swagger（完整教程） - 西瓜程序猿 - 博客园 (cnblogs.com)](https://www.cnblogs.com/kimiliucn/p/17602073.html);[Swashbuckle 和 ASP.NET Core 入门 | Microsoft Learn](https://learn.microsoft.com/zh-cn/aspnet/core/tutorials/getting-started-with-swashbuckle?view=aspnetcore-8.0&tabs=visual-studio)
- RESTful API：[RESTful 架构详解 | 菜鸟教程](https://www.runoob.com/w3cnote/restful-architecture.html)；[RESTful API 最佳实践 - 阮一峰的网络日志](https://www.ruanyifeng.com/blog/2018/10/restful-api-best-practices.html)；[What is REST?: REST API Tutorial](https://restfulapi.net/)

一些 C# 相关的优秀项目和框架参考：
1. [**Furion**：基于 ASP.NET Core 的快速开发框架，具有强大的功能](https://www.cnblogs.com/Can-daydayup/p/17610367.html)
2. [**ABP Framework**：专注于基于 ASP.NET Core 的 Web 应用程序开发，同时也支持其他类型的应用程序开发](https://www.cnblogs.com/Can-daydayup/p/17610367.html)
3. [**MASA Framework**：.NET 下一代微服务开发框架，支持分布式、微服务、DDD、SaaS 等现代应用开发，基于分布式应用运行时 Dapr](https://www.cnblogs.com/Can-daydayup/p/17610367.html)
4. [**ASP.NET Core**：跨平台开源框架，用于构建基于云的现代互联网连接应用程序，例如 Web 应用程序、IoT 应用程序和移动后端](https://www.cnblogs.com/Can-daydayup/p/17610367.html)

实际上都摘自同一篇文章：[C#/.NET/.NET Core优秀项目和框架精选（坑已挖，欢迎大家踊跃提交PR或者Issues中留言） - 追逐时光者 - 博客园](https://www.cnblogs.com/Can-daydayup/p/17610367.html)

（240624：暂时搁置）
