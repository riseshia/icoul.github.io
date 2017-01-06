---
layout: post
title: "Spring에 mySQL 세팅" 
category: mySQL
---

## pom.xml 파일 설정하기  

{% highlight java %}
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.38</version>
</dependency>
<dependency>
    <groupId>org.bgee.log4jdbc-log4j2</groupId>
    <artifactId>log4jdbc-log4j2-jdbc4.1</artifactId>
    <version>1.16</version>
</dependency>
{% endhighlight %}

pom.xml에 mysql세팅을 위한 jar파일을 추가한다.  
log4는 이 후 테스트 시 로그를 표시하기 위한 라이브러리이다.  

## 'root_context' 세팅방법  

{% highlight java %}
<bean id="dataSource"
		class="org.springframework.jdbc.datasource.DriverManagerDataSource">
		<property name="driverClassName" value="net.sf.log4jdbc.sql.jdbcapi.DriverSpy">
		</property>
		<property name="url" value="jdbc:log4jdbc:mysql://127.0.0.1:3306/test"></property>
		<property name="username" value = "root"></property>
		<property name="password" value = ""></property>	
	</bean>
{% endhighlight %}

설치된 mySQL과 Spring을 연결하기 위해 bean을 설정해준다.  
test는 mySQL의 데이터베이스 명이며  
username과 password는 설치 시 설정한 이름, 비밀번호를 적는다.  
기본은 root이다.  
  
여기까지 하면 일단 세팅은 완료. 이후에는 테스트를 통해 잘 세팅되었는지 확인한다.  