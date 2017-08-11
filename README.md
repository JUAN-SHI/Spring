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
### Spring容器内部对象的创建
1. 使用类构造器实例化(默认无参数)
<bean id=" " class=" "/>
2. 使用静态工厂方法实例化(简单工厂模式)
<bean id="personService"  class="com.itcast.factory.PersonServiceFactory"    factory-method="createPersonService" />
public class PersonServiceFactory {
      public  static PersonService createPersonService(){
                return new PersonServiceImpl();
      }
}
3. 使用实例工厂方法实例化
<bean id="personServiceFactory"  class="com.itcast.factory.PersonServiceFactory"  />
<bean id="personService"  class="com.itcast.factory.PersonServiceFactory" factory-bean="personServiceFactory"  factory-method="createPersonService" />
public class PersonServiceFactory {
      public  static PersonService createPersonService(){
                return new PersonServiceImpl();
      }
}
### 初始化bean时机
- Spring默认在启动时将所有singleton bean提前进行实例化。提前实例化意味着作为初始化的一部分，ApplicationContext会自动创建并配置所有的singleton bean.通常情况下这是件好事。因为这样在配置中有任何错误能立即发现。Lazy-init=”true or  false”;Lazy-init 为false,spring容器将在启动的时候报错（比较好的一种方式）;Lazy-init 为true,spring容器将在调用该类的时候出错。
### Bean的作用域
1. singleton(默认值) :
- 在每个Spring IoC容器中一个bean定义只有一个对象实例(共享)。默认情况下会在容器启动时初始化bean，但我们可以指定Bean节点的lazy-init=“true”来延迟初始化bean，这时候，只有第一次获取bean会才初始化bean。如： <bean id="xxx" class="cn.itcast.OrderServiceBean" lazy-init="true"/>;
如果想对所有bean都应用延迟初始化，可以在根节点beans设置default-lazy-init=“true“，如下： 
<beans default-lazy-init="true“ ...> 
 2. prototype :
 - 允许bean可以被多次实例化(使用一次就创建一个实例) . Spring不能对一个prototype bean的整个生命周期负责.这就意味着清楚prototype作用域的对象并释放任何prototype bean所持有的昂贵资源都是客户端的责任。
### 依赖注入(DI)
1. 使用构造器注入
- 使用xml的注入方式
- A.	通过参数的顺序
<constructor-arg index="0">
      <value>张三</value>
</constructor-arg>
<constructor-arg index="1">
       <value>56</value>
 </constructor-arg> 
- B.	通过参数的类型
<constructor-arg type="java.lang.Integer">
              <value>56</value>
       </constructor-arg>
       <constructor-arg type="java.lang.String">
              <value>张三</value>
       </constructor-arg>
2. 使用属性setting方法进行注入
- 使用xml的注入方式：
- A.	简单Bean的注入
简单Bean包括两种类型：包装类型和String
<bean id="personService"   class="com.itcast.bean.impl.PersonServiceImpl">
<!-- 基本类型,string类型 -->
<property name="age" value="20"></property>
<property name="name" value="张无忌"></property>                       
</bean>
- B.	引用其他Bean
<bean id="person" class="com.itcast.bean.Person" />
 <bean id="personService"  class="com.itcast.bean.impl.PersonServiceImpl">
 <property name="person" ref="person" />
</bean>
1. 装配list集合 
<property name="lists">
     <list>
         <value>list1</value>
         <value>list2</value>
         <value>list3</value>
     </list>
 </property> 
2. 装配set集合
<property name="sets">
   <set>
           <value>set1</value>
           <value>set2</value>
           <value>set3</value>
   </set>
</property>

3. 装配map
<property name="maps">
       <map>
            <entry key="01">
                    <value>map01</value>
            </entry>
            <entry key="02">
                    <value>map02</value>
            </entry>	
       </map>
</property>
map中的<entry>的数值和<list>以及<set>的一样，可以使任何有效的属性元
素，需要注意的是key值必须是String的。
4. 装配Properties
<property name="props">
           <props>
             <prop key="01">prop1</prop>
             <prop key="02">prop2</prop>
           </props>
        </property>  

