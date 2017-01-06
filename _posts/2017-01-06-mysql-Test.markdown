---
layout: post
title: "Spring에서 mySQL 세팅 테스트하기" 
category: mySQL
---

이 글은 Spring의 `pom.xml`과 `root-context`파일을 세팅한 후  
문제없이 세팅이 되어서 잘 연결되었는지 테스트하는 코드를 짜는 내용이다.  

## Spring에 JUnit 테스트 세팅하기
  
`pom.xml`에 이하와 같이 세팅한다.
  
{% highlight java %}
<properties>
		<java-version>1.8</java-version>
		<org.springframework-version>4.2.3.RELEASE</org.springframework-version>
		<org.aspectj-version>1.6.10</org.aspectj-version>
		<org.slf4j-version>1.6.6</org.slf4j-version>
	</properties>
{% endhighlight %}
  
{% highlight java %}
<!-- Test -->
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
    <scope>test</scope>
</dependency>
{% endhighlight %}
  
이로써 4.12버전의 JUnit jar파일이 라이브러리에 추가되었다.  
  
{% highlight java %}
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(locations = {"file:src/main/webapp/WEB-INF/spring"
								+ "/**/*-context.xml"})
public class DBConnTest {
	
	@Inject
	private DataSource ds;
	
	@Test
	public void test() throws Exception {
		System.out.println(ds.getConnection());
	} // Test
}// Class
{% endhighlight %}
  
test/java 패키지에 DB 테스트용 class를 만들고 테스트 코드를 입력한다.  
  
![스크린샷](https://icoul.github.io/images/mySQL_Test_01.PNG)
  
코드를 돌렸을 때 이상과 같이 초록색바가 뜬다면 mySQL과 Spring이 문제없이 연결된 것이다.   
