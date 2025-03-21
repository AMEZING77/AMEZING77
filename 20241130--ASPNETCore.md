[TOC]
# ASP.NET Core Beginner

- 创建时间: 2024年11月30日 10:20
- Tag: Website
- [Link to YouTube](https://youtu.be/4IgC2Q5-yDE?si=rIYRFqTV-4lOw_fK)
![alt text](assets/ASP.NETCore/63.png)

##  MVC介绍
###    简单Model的创建思路
![alt text](assets/ASP.NETCore/1.png)
1. 建立Model文件夹，新建类
2. 简历操作Model的接口
3. Mock接口
4. 在Controller中调用接口
###    如何进行依赖注入
![alt text](assets/ASP.NETCore/3.png)
>进行依赖注入的好处是
>1. 构建松耦合的系统；
>2. 便于单元测试
###    三种依赖注入方式的区别
![alt text](assets/ASP.NETCore/2.png)
[stackoverflow的解释](https://stackoverflow.com/questions/38138100/addtransient-addscoped-and-addsingleton-services-differences)
###    定制mvc中View的路径
![alt text](assets/ASP.NETCore/68.jpg)    
1. 默认是Views/Home/Details.cshtml
2. 可修改传参，选择任意目录下的View
##  View传参
###    ViewData
![alt text](assets/ASP.NETCore/67.jpg)
![alt text](assets/ASP.NETCore/64.jpg)
![alt text](assets/ASP.NETCore/66.jpg)
1. 如何通过viewdata传参到界面
2. 参数若是string类型，界面会进行隐式转换，若是其他类型，必须手动进行转化。例如model
3. 传参和使用时的key必须一致
###    ViewBag
![alt text](assets/ASP.NETCore/70.jpg)
![alt text](assets/ASP.NETCore/71.jpg) 
![alt text](assets/ASP.NETCore/72.jpg)
1. 动态类型传参，直接点＝
2. 界面上不需要显示转换对应类型
3. 但是需要手动输入点之后的参数，必须一致
###    Strongly typed View
![alt text](assets/ASP.NETCore/73.jpg) 
![alt text](assets/ASP.NETCore/74.jpg)
1. 视图传参直接传入modeI，在view中引入model类型
2. 具备编译时检查和智能感知
###    View Model
![alt text](assets/ASP.NETCore/77.jpg) 
![alt text](assets/ASP.NETCore/76.jpg)
###    传递list数组
![alt text](assets/ASP.NETCore/78.jpg) 
![alt text](assets/ASP.NETCore/81.jpg)
1. 建立index.cshtml，实现get all方法
2. 建立对应的页面
## View与Layout
### LayoutView
![alt text](assets/ASP.NETCore/83.jpg) 
![alt text](assets/ASP.NETCore/79.jpg) 
![alt text](assets/ASP.NETCore/82.jpg)
1. 默认在同级目录下shared
2. 可以在各个子界面中显示引用和传参
3. 但是每个子界面中都要引用和传参吗？
### Section
![alt text](assets/ASP.NETCore/85.jpg)     
![alt text](assets/ASP.NETCore/86.jpg) 
![alt text](assets/ASP.NETCore/87.jpg) 
![alt text](assets/ASP.NETCore/84.jpg)    
1. 在js文件夹中建立script
2. 在对应的cshtml文件中引用
### ViewStart
1. 每个界面都可以使用Layout，但是每个界面都使用重复代码需要传参吗？
例如Layout="_Layout.cshtml"??
1. **其实是不必要的，可以使用ViewStart来实现共同的功能；**
![alt text](assets/ASP.NETCore/88.PNG)
![alt text](assets/ASP.NETCore/89.png)
### ViewImports
1. 类似于GlobaUsing，为ViewImports所在View目录下的所有文件引入命名空间；
2. 子目录中的ViewImports会Override父目录中的ViewImports；
![alt text](assets/ASP.NETCore/90.png)
![alt text](assets/ASP.NETCore/91.png)

##  Routing
### Default Routing
1. 托管的服务器如何导航到方法内部；
![alt text](assets/ASP.NETCore/92.png)
2. MVC配置的默认路由是Home/Index/id?;
![alt text](assets/ASP.NETCore/93.png)
3. 如何手动配置路由；
![alt text](assets/ASP.NETCore/94.png)
4. 如何配置默认路由，例如只定位到localhost:4415后
![alt text](assets/ASP.NETCore/95.png)
### Attribute Routing
1. 使用UsingMvc空模板,但是通过特性配置单个或多个路由；
![alt text](assets/ASP.NETCore/96.png)
2. 同时可以传递默认参数；
![alt text](assets/ASP.NETCore/97.png)
3. 如何减少路由入口的重复配置，直接定义Controller的路由特性；
![alt text](assets/ASP.NETCore/98.png)
4. 如何一键配置通用路由特性
![alt text](assets/ASP.NETCore/100.png)
5. 特殊符号意义
>[Routed("~/")] 的含义如下：
~ 符号代表应用程序的根目录。
""（空字符串）表示没有额外的路径部分。
因此，[Routed("~/")] 的作用是,
将一个控制器或动作方法**配置为应用程序的默认路由**，
即当用户仅访问网站的根URL,这个控制器或动作方法将会被调用。
![alt text](assets/ASP.NETCore/99.png)


## Bootstrap
### Install
![alt text](assets/ASP.NETCore/101.png)
### TagHelper
![alt text](assets/ASP.NETCore/102.png)
1. 为什么使用TagHelper?
>若修改Route路径前缀或者其他，无需变动
![alt text](assets/ASP.NETCore/103.png)
2. 网页资源的缓存，索引更改（若图像改变则重新下载，反之读取缓存）
实现原理是TagHelper通过计算图像资源的哈希值并附加到url；
![alt text](assets/ASP.NETCore/104.png)
![alt text](assets/ASP.NETCore/105.png)

### Enviroment Tag
1. 在cs.html中标记，确认哪种情况下渲染的界面；
![alt text](assets/ASP.NETCore/106.png)
2. 使用taghelper检测在线资源的合法性；
![alt text](assets/ASP.NETCore/107.png)

### Navigation menu
1. 涉及很多html知识
![alt text](assets/ASP.NETCore/108.png)

### Form Tag Helper
![alt text](assets/ASP.NETCore/109.png)
1. 表单的格式绘制及效果

## Model
### Model Binding
1. MVC自动绑定model
2. 在Create()方法中，默认返回Create.cshtml页面；
3. 在Create.cshtml页面中，若建立表单并点击Create,则默认调用Create(Employee employee)接口；
![alt text](assets/ASP.NETCore/110.png)
### Model Validation
1. 如何将验证绑定model
![alt text](assets/ASP.NETCore/111.png)
2. 如何在MVC中应用验证特性
![alt text](assets/ASP.NETCore/112.png)
3. 如何涉及界面验证信息视图
![alt text](assets/ASP.NETCore/113.png)
### Select List Validation 
1. 如何验证枚举类型
![alt text](assets/ASP.NETCore/114.png)


## EntityFraeworkCore.SqlServer
### 安装Nuget包
1. SQLServer是为了使用DBContext
2. Tools是为了使用程序包管理器控制台指令
![alt text](assets/ASP.NETCore/115.png)
### 建立AppDbContext类，实现DbContext调用
![alt text](assets/ASP.NETCore/116.png)
### 完善Model-DB操作接口
Update(Employee employeeChanges)：更新一个现有的 Employee 实体。
它首先尝试将传入的 employeeChanges 实体附加到 context.Employees 集合中，
（尽管这一步在大多数情况下可能是多余的，因为 Attach 方法通常用于未跟踪的实体），
然后将实体的状态设置为 Modified，最后调用 context.SaveChanges() 方法保存更改。
注意，这里有一个小错误：employee.State = Microsoft.EntityFrameworkCore.EntityState.Modified; 
这行代码是不正确的，因为 employee 是一个 EntityEntry<Employee> 类型（由 Attach 方法返回），而不是 Employee 类型。
正确的做法应该是直接调用 context.Entry(employeeChanges).State = EntityState.Modified;。
```C#
public Employee Update(Employee employeeChanges)
{
    context.Entry(employeeChanges).State = EntityState.Modified;
    context.SaveChanges();
    return employeeChanges;
}
```
![alt text](assets/ASP.NETCore/117.png)

### 使用EFCore.Tools创建Migration【Add-Migration】和创建数据库Update-Database
1. 创建迁移文件
![alt text](assets/ASP.NETCore/118.png)
![alt text](assets/ASP.NETCore/119.png)
2. 更新数据库
![alt text](assets/ASP.NETCore/120.png)

### EntityFraeworkCore seed data
1. 在AppDbContetx是创建SeedMigration ，并更新数据库
![alt text](assets/ASP.NETCore/121.png)
2. 简化SeedMigration
![alt text](assets/ASP.NETCore/122.png)

### Remove-Migration && Undo-Migration
1. 若当前Migration3未Update-Database，则可以直接移除Migration，并回退到上一个Migration;
2. 若当前Migration3已Update-Database，则需要先Update-Database到想要的Migration1，然后移除Migration2/3;
![alt text](assets/ASP.NETCore/123.png)

## 完善界面功能
### 如何上传文件IFormFile，如何显示界面
1. 新增图片链接属性，创建对于的ViewModel，实现IFormFile调用【FileName+CopyTo】
![alt text](assets/ASP.NETCore/124.png)
2. 设计界面，展示文件选择功能
![alt text](assets/ASP.NETCore/125.png)
### 如何设计Edit-View/ViewMode
1. 继承CreateViewModel,在页面中传入两个相关的隐藏属性
![alt text](assets/ASP.NETCore/126.png)
2. 实现Update和Cancel功能(注意本地图片的更新和删除)
![alt text](assets/ASP.NETCore/127.png)
### 设计Delete
![alt text](assets/ASP.NETCore/128.png)


## 异常处理
### 增加HomeController的404NotFound界面
![alt text](assets/ASP.NETCore/129.png)
### 增加Shared NotFound.cshtml
![alt text](assets/ASP.NETCore/130.png)
### 如何处理全局异常
1. Add ExceptionHandler Middleware
![alt text](assets/ASP.NETCore/131.png)
2. Add ErrorController
![alt text](assets/ASP.NETCore/132.png)
3. Add Error.cshtml
![alt text](assets/ASP.NETCore/133.png)


## Logging
### Logging Providers
![alt text](assets/ASP.NETCore/134.png)
### Microsoft.Extensions.Logging
![alt text](assets/ASP.NETCore/135.png)
![alt text](assets/ASP.NETCore/136.png)
### LogLevel
![alt text](assets/ASP.NETCore/137.png)


## Identity-EFCore
### 如何快速应用ASP.NETCore Identity，结合EFCore
1. 实现IdentityDbContext的调用及依赖注入
![alt text](assets/ASP.NETCore/138.png)
2. 使用Add-Migration和Update-Database创建数据库
   1. 注意实现IdentityDbContext的base实现
   ![alt text](assets/ASP.NETCore/139.png)
   2. Service注入的默认IdentityUser，自动创建对应DB
   ![alt text](assets/ASP.NETCore/140.png)

### How to Register new user【HttpGet】
1. 建立AccountController,实现Register方法
2. 建立RegisterViewModel以及对应的Register.cshtml
3. 修改Layout.cshtml，添加Register链接（在布局右侧）
![alt text](assets/ASP.NETCore/141.png)
![alt text](assets/ASP.NETCore/142.png)

### How to Register new user【HttpPost】
1. 两个Manager类的作用 
![alt text](assets/ASP.NETCore/145.png)
2. 实现Register(RegisterViewModel)方法
![alt text](assets/ASP.NETCore/143.png)
1. 注册效果
![alt text](assets/ASP.NETCore/144.png)