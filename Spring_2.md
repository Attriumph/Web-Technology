# Use comment to configure spring

1)Import package：4+2+spring-aop
2)为主配置文件引入新的命名空间（约束）
3)开启，使用注解代理配置文件

      <?xml version="1.0" encoding="UTF-8"?>
     <beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"; xmlns="http://www.springframework.org/schema/beans"; xmlns:context="http://www.springframework.org/schema/context"; xsi:schemaLocation="http://www.springframework.org/schema/beanshttp://www.springframework.org/schema/beans/spring-beans-4.2.xsdhttp://www.springframework.org/schema/contexthttp://www.springframework.org/schema/context/spring-context-4.2.xsd ">
<--!指定扫描bean包下的所有类中的注解。
      注意扫描会扫描指定包下的所有子孙包-->
<context:component-scan base-package="bean"></context:component-scan>

</beans>
4)在类中使用注解完成配置

在要配置的类中加入意思下代码
@Ccompon("user")
// 相当于 <bean name = "user" class = "beans" ></bean>

@Service("") //注解service层对象
@Contriller("") // 注解web层对象
@Repository("")//注解dao层

@Scope(scopeName = "prototype") // modeify the scope of object

//Indejection of Attributes
//can put right before the filed or right before setter method
@Vaule("Tom")  // = <propeirety></propeirety>

//Injection of Object---method 1
@Autowired //problem: if find several ojects, cannot choose which one
//Injection of Object---method 2
@Autowired
@Qualifer("car2") //tell which one should be injected
//Resource(name = "car")// manually injected

@PostConstruct // call the method after calling constructor

@ PreDestory // call the method before destrcution




#Install STS plugin (Spring Tool Suite)
     http://hao.jobbole.com/springsource-tool-suite/

#The Integration of  Spring and JUnit
Firstly, we need to import necessary passage(4+2+aop+spring-test-.jar )

//help us to create container
@RunWith(SpringJUnit4ClassRunner.class)

//point out which Configuartion files will be used
@ContextConfiguration("classpath: applicationContext.xml")
public class Demo{

   @Resource(name = "user")
   private User u;
   //we do not need to create container in every func  test
  @Test
  public void fun1(){}
  public void fun2( ) { }
    public void fun3( ){ }
}

# AOP in Spring

1) Function: Spring could generate dynamic proxy objects for managed objects in container . We do not need to write
Proxy.newProxyInstance(classLoader, Interface[], InvocationHander hander)
2) the method of Implementation of AOP in Spring
  a. dynamic proxy ：被代理对象必须实现接口，才能产生代理对象
  b. cglib proxy：could generate proxy for any objects
3) concepts about AOP:
   jointpoint: all method in Target will be added advice
   pointcut: successfully added methods
   advice: code will be added jointpoint
   target: 被代理对象
   weaving: verb， put advice into jointpoint to form pointcut
   proxy: the proxy object after Target object finish weaving,
   aspect: pointcut + advice


# Use AOP in Spring
1) import package :4+2+2(spring-aspects,spring-aop)+2(com.springsource.org.aopalliance，(com.springsource.org.aspectj.weaver--the third
    party)
2）prepare Target
3) prepare Advice

ublic class MyAdvice {
      //前置通知
    public void before(){
        System.out.println("这是前置通知!!");
    }
    //后置通知
    public void afterReturning(){
        System.out.println("这是后置通知(如果出现异常不会调用)!!");
    }
    //环绕通知
    public Object around(ProceedingJoinPoint pjp) throws Throwable {
        System.out.println("这是环绕通知之前的部分!!");
        Object proceed = pjp.proceed();//调用目标方法
        System.out.println("这是环绕通知之后的部分!!");
        return proceed;
    }
    //异常通知
    public void afterException(){
        System.out.println("出事啦!出现异常了!!");
    }
    //后置通知
    public void after(){
        System.out.println("这是后置通知(出现异常也会调用)!!");
    }
}
4) configure to weaving

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"; xmlns="http://www.springframework.org/schema/beans"; xmlns:context="http://www.springframework.org/schema/context"; xmlns:aop="http://www.springframework.org/schema/aop"; xsi:schemaLocation="http://www.springframework.org/schema/beanshttp://www.springframework.org/schema/beans/spring-beans-4.2.xsdhttp://www.springframework.org/schema/contexthttp://www.springframework.org/schema/context/spring-context-4.2.xsdhttp://www.springframework.org/schema/aophttp://www.springframework.org/schema/aop/spring-aop-4.2.xsd ">
<!--firstly，we need import aop constraint -->
<!-- 1.configure Target -->
      <bean name="userService" class="cn.itcast.service.UserServiceImpl" ></bean>
<!-- 2.configure Advice -->
      <bean name="myAdvice" class="cn.itcast.d_springaop.MyAdvice" ></bean>
<!-- 3.weave Advice into Target -->
      <aop:config>
            <!-- configure pointcut
                  * cn.itcast.service.*ServiceImpl.*(..)
                  * cn.itcast.service..*ServiceImpl.*(..)
            -->
            <aop:pointcut expression="execution(* cn.itcast.service.*ServiceImpl.*(..))" id="pc"/>
            <aop:aspect ref="myAdvice" >
                  <!-- 指定名为before方法作为前置通知 -->
                  <aop:before method="before" pointcut-ref="pc" />
                  <!-- 后置 -->
                  <aop:after-returning method="afterReturning" pointcut-ref="pc" />
                  <!-- 环绕通知 -->
                  <aop:around method="around" pointcut-ref="pc" />
                  <!-- 异常拦截通知 -->
                  <aop:after-throwing method="afterException" pointcut-ref="pc"/>
                  <!-- 后置 -->
                  <aop:after method="after" pointcut-ref="pc"/>
            </aop:aspect>
      </aop:config>
</beans>
