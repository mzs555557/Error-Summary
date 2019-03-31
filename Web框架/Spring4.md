###bean的配置
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