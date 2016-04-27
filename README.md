# framework
This is a simple framework
这是一个简单的MVC加DAO层的框架，简单实现了Spring中的IOC，AOP，SpringMVC的请求路由已经转发以及Mybatis中的简单的rm功能。
本项目纯属学习过程中的实践项目，其中还有各种不足之处。

# 框架使用指南
本项目暂时未被同步到maven仓库中，用户可以直接下载项目的jar包后将之导入本地项目的路径中即可。
本地项目推荐使用maven进行构建，同时需要在resource目录下添加名为info.properites的配置文件，配置文件中的基本配置属性如下:

info.framework.jdbc.driver=com.mysql.jdbc.Driver
info.framework.jdbc.url=jdbc:mysql://127.0.0.1:3306/demo
info.framework.jdbc.username=root
info.framework.jdbc.password=
info.framework.app.base_package=com.pcncad.lgm
info.framework.app.jsp_path=/WEB-INF/view/
info.framework.app.asset_path=/asset/

info.framework.jdbc.driver表示本项目中数据库驱动的配置信息
info.framework.jdbc.url表示数据库的url
info.framework.jdbc.username表示连接数据库的用户名
info.framework.jdbc.password表示连接数据库的密码
info.framework.app.base_package表示项目扫描Controller,Service,Respority的基本路径，意思等同于SpringMVC配置过程中的Component-Scan的basepackage属性
info.framework.app.jsp_path=/WEB-INF/view/ 表示Controller转向诸如jsp的视图的时候的前缀路径。

# 重要注解说明
@Controller:类级别注解，意思等同于SpringMVC中的Controller
@Action:方法级别的注解，只能被用在被Controller注解的类的方法上，参考如下：

	@Action("get:/customer")
	public View	index(Param param) {
		List<Customer> customers = customerService.getCustomerList();
		return new View("customer.jsp").addModel("customerList", customers);
	}
	
	@Action("get:/insertCustomer")
	public Data	insert(Param param) {
		return new Data(customerService.createCustomer(param.getParamMap()));
	}
如上图所示:Action的default value中的:前的部分表示这个对外暴露的url接口的访问方式，后半部分则表示改url接口的路径。
同时，对于被action注解的方法，如果放回的是View则表示会转到对应的视图，如果返回Data则表示回直接返回json数据。
@Aspect:类级别的注解，表示标注一个切面类
@Inject:属性级别的注解，表示对该属性自动注入
@Respority:类级别的注解：表示一个类是数据仓库
@Transaction:方法级别的注解，被其注解的方法回自动完成事物的控制特性
@Insert:方法级别的注解，需要传入2个参数，clause表示标准的sql语句，且支持?占位，targetClass表示查询的类，被该注解标注的方法的函数签名的参数必须为Object... 且顺序对应sql中？占位的顺序，且返回值默认是List。默认已经实现事务功能
@Delete:方法级别的注解，clause表示标准的sql语句，且支持?占位，，被该注解标注的方法的函数签名的参数必须为Object...且顺序对应sql中？占位的顺序，且返回值默认是boolean。默认已经实现事务功能
@Update:方法级别的注解，clause表示标准的sql语句，且支持?占位，，被该注解标注的方法的函数签名的参数必须为Object...且顺序对应sql中？占位的顺序，且返回值默认是boolean。默认已经实现事务功能
@Insert:方法级别的注解，clause表示标准的sql语句，且支持?占位，，被该注解标注的方法的函数签名的参数必须为Object...且顺序对应sql中？占位的顺序，且返回值默认是boolean。默认已经实现事务功能

domain层的实体属性名称需要和数据库的列名相同





	















