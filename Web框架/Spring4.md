### bean的配置

```
<bean id="aa" class="bb">
	//通过属性赋值
	<property name="xx" value="yy" type="zz">
	//通过构造器注入属性值 可以根据index 和value进行更精确的定位
	<constructor-arg value="Mike" index="number"></constructor-arg>
	//若字面值中包含特殊的字符,则可以根据DCDATA来进行赋值
	<constructor-arg>
	   <value><![CDATA[<ATARZA>]]></value>
	</constructor-arg>
</bean>
//集合属性的配置
<bean id="aas" class="bbs">
	<property>
		<list>
			<ref bean="aa"/>
		</list>
	</property>
</bean>

```

```
使用scope属性来配置 bean 的作用域
singleton : 默认值 , 容器初始化时创建 bean 实例,在整个容器的生命周期内只创建这一个bean
prototype : 原型的, 初始化时不创建 bean 实例, 而在每次的请求时创建一个新的 bean 实例, 并返回
<bean id="car" class="beans.Car" scope="prototype"></bean>
    <bean id="car1" class="beans.Car">
        <constructor-arg index="0" type="java.lang.String" value=""/>
        <constructor-arg index="1" type="java.lang.String" value=""/>
        <constructor-arg index="2" type="double" value="2.0"/>
    </bean>
------------------
实现 BeanPostProcessor 接口 , 并具体提供
postProcessBeforeInitialization init-method 之前调用
postProcessAfterInitialization init-method 之后调用

bean:bean 实例本身
beanName: IOC 容器配置的bean的名字
返回值: 是实际上给用户的那个Bean , 注意:可以在以上方法中修改 bean
<bean id="car" class="cycle.Car" init-method="init" destroy-method="destroy">
        <property name="brand" value="Audi"/>
    </bean>
<bean class="cycle.MyBeanPostProcessor"/>
----------dataSource源的配置
 <context:property-placeholder location="classpath:db.properties"/>
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="user" value="${user}"/>
        <property name="password" value="${password}"/>
        <property name="driverClass" value="${driverclass}"/>
        <property name="jdbcUrl" value="${jdbcurl}"/>
    </bean>

```

#### SpringAop
 - #####SpringAop中放入jar包
 - #####在配置文件中加入 aop 的命名空间
 - #####在配置文件中加入以下的配置
    - `<aop:aspectj-autoproxy/> <context:component-scan base-package="aop"/>`
 - 类之前有`@Component` && `@Aspect`
 - 有 `Before` `After` `Around` `AfterReturning` 方法 