# Spring
## 1.spring 的简介
     Spring 其实就是项目中所有对象的容器！装什么对象，就有什么功能（所以是一个一站式开源框架）
两个重要思想：IOC 和AOP

 docs:API 和开发规范.
        lib:jar 包和源码
        schema：约束
   ps：框架和对象交流---是通过配置文件

## 2.spring的两个概念：
 * 控制反转（Inversion of Control，英文缩写为IoC）把创建对象的权利交给框架,是包括依赖关系也是自己注入,对象由spring创建以及注入
 * DI： dependency injection 依赖注入， 实现IOC 需要DI 支持


ApplicationContext接口，每次容器启动时就会创建容器中配置的所有对象
两个实现类：从类路径下加载 配置文件：ClassPathXmlApplicationContext
                       从绝对路径下加载文件：FileSystemXmlApplicationContext

# Spring的搭建：

1）导包：4+2
2）创建要放入容器的对象
3）书写配置文件，导入约束：位置任意(建议放到src下) ，配置文件名任意(建议applicationContext.xml)
4）代码测试



# Spring的配置：
1.bean元素: 使用该元素描述需要spring容器管理的对象
 （1） 两个属性： class属性和name属性
 （2）scope属性： singleton（在spring容器中只存在一个对象）和prototype（获得对象的时候就会创建新对象）
                      （strusts2每次请求的时候都会创建一个新的action，所以spring和struts2整合时，action对象 bean必须配置成prototype，其他情况一般都是singleton   ）
（3）生命周期属性：init-method 和 destor-0method（基本不用）

2.spring 创建对象的方式：
1）.空参构造创建（主要）
2）静态工厂
3）实例工厂

3.spring的分模块配置：
<!-- 导入其他spring的配置文件>
<import resource = "相对路径">

4.spring的属性注入
1）set方法注入：
 <!-- 值类型的set注入 >
<bean name ="user"  class = "bean.User">

<property name = "name" value = "Tom"><property>
<property name = "age" value = "21"><property>

</bean>
 <!-- 对象类型的set注入 -->
<bean name ="user"  class = "bean.User">

<property name = "name" value = "Tom"><property>
<property name = "age" value = "21"><property>
<property name = "car" ref = "car"></property>
</bean>
<!-- 先将car对象 配置到容器中-->
<bean name = "car" class = "bean.Car">
  <property name = "name" value ="Honda"></property>
  <property name = "color" value ="yellow"></property>
</bean>
2）构造函数注入
 前提是类有相应的构造函数
<!--user中的构造方法-->
public User（Stirng name， Car car）{.....}
public User（Car car， String name）{.....}
public User（Integer name， Car car）{.....}
<bean name ="user"  class = "bean.User">
<constructor-arg name = "name"  value = "jerry" index = "0" type="java.lang.Integer"></constructor-arg>
<constructor-arg name = "car"  ref = "car"></constructor-arg>

3）p名称空间注入
4)spel注入


5.复杂类型的注入
<!-- 复杂类型注入 -->
  <bean name="cb" class="cn.itcast.c_injection.CollectionBean" >

       <!-- 如果数组中只准备注入一个值(对象),直接使用value|ref即可
      <property name="arr" value="tom" ></property>

     <!-- array注入,多个元素注入 -->
     <property name="arr">
        <array>
            <value>tom</value>
            <value>jerry</value>
            <ref bean="user4" /> // 在数组中注入对象
      </array>
    </property>

    <!-- 如果List中只准备注入一个值(对象),直接使用value|ref即可
    <property name="list" value="jack" ></property>-->
    <property name="list"  >
        <list>
            <value>jack</value>
            <value>rose</value>
            <ref bean="user3" />
        </list>
    </property>


<!-- map类型注入 -->
    <property name="map"  >
        <map>
            <entry key="url" value="jdbc:mysql:///crm" ></entry>
            <entry key="user" value-ref="user4"  ></entry>  // value为对象的情况
            <entry key-ref="user3" value-ref="user2"  ></entry>  // key为对象的情况
        </map>
    </property>


<!-- prperties 类型注入 -->
    <property name="prop"  >
        <props>
            <prop key="driverClass">com.jdbc.mysql.Driver</prop>
            <prop key="userName">root</prop>
            <prop key="password">1234</prop>
        </props>
    </property>
</bean>
