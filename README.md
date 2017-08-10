# Spring
## Spring基本特征
- Spring是一个非常活跃的开源框架；它是一个基于Core来构架多层JavaEE系统的框架,它的主要目地是简化企业开发.Spring以一种非侵入式的方式来管理你的代码，
Spring提倡”最少侵入”，这也就意味着你可以适当的时候安装或卸载Spring。
## Spring基本功能详解
### SpringIOC
- Spring的控制反转：把对象的创建、初始化、销毁等工作交给spring容器来做。由spring容器控制对象的生命周期。
- 步骤：
- A. 启动spring容器
1. 在类路径下寻找配置文件来实例化容器 
 - ApplicationContext ctx = new ClassPathXmlApplicationContext(new String[]{"beans.xml"});可以在整个类路径中寻找xml文件
 - 通过这种方式加载。需要将spring的配置文件放到当前项目的classpath路径下
 - classpath路径指的是当前项目的src目录，该目录是java源文件的存放位置。 
2. 在文件系统路径下寻找配置文件来实例化容器 
- ApplicationContext ctx = new FileSystemXmlApplicationContext(new String[]{“d:\\beans.xml“});
- Spring的配置文件可以指定多个，可以通过String数组传入。
- 注：经常用第一种方法启动容器
- B. 从spring容器中提取对象


