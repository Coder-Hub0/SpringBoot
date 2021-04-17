# Spring Security
we need to provide a security for spring-web project

1. we mostly concern about the **login** and **logout** pages but in between those pages mostly we have lots of pages only registered user able to login instead of un-register

2. we can enchance the security mechanism using <u><b>encryption of password</u></b> but we developers know we can decrypt those encryptions as well
      new encryption tech  <b><u><i>Bcrypt</i></u></b>
 <dl>
    <dt><b><u><i>Bcrypt</i></u></b>
    </dt>
    <dd>    is one the way to encrypt the password instead of Sha or md
    </dd>
    <dt> <u><b>   OAuth2</b></u>
    </dt>
    <dd>
    Its new way of signin with google its google library.
    </dd>
 </dl>

 We need to configure for enchance the web application Security
 Spring Security provides <b>Authentication & Authorization</b>

 Let's Start Step By Step

 1. Create a spring-boot web application with dependency of 
    <b><u>Spring-Web</u></b>
    and <b><u>Spring-devtools</u></b>
 
 2. create a Home <b>Controller</b> into Web Application

 3. Create a <b>JSP</b> for view in Browser.

4. we need to add one more dependency for render the JSP page instead of downloading those render file.
<B><U>Tomcat-Jasper</U></b> is dependency name.
> 
		<!-- https://mvnrepository.com/artifact/org.apache.tomcat/tomcat-jasper -->
		<dependency>
			<groupId>org.apache.tomcat</groupId>
			<artifactId>tomcat-jasper</artifactId>
			<version>9.0.31</version>
		</dependency>

5. Now we start secure this page instead of move futher
we add One Dependency i.e. <B><U>Spring-Started Boot Security</U></B>

> 	<!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-security -->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-security</artifactId>

		</dependency>
After  adding Spring Security we need to login and password available on console. username is user

6. Now we not wanna to be like that we wanna static user able to access websites.For that we need to Configure Spring Web Security
So we need to create a class in <u><b>config</u></b> package. We can name that class <u>ApplicationSecurityConfig </u> and need to extend that class to <u><b>WebSecurityConfigurerAdapter</b></u>
>package com.demo.config;<br/>
import org.springframework.context.annotation.Configuration;<br/>
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;<br/>
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;<br/>
@Configuration<br/>
@EnableWebSecurity
<br/>public class <b>ApplicationSecurityConfig</b> extends <b>WebSecurityConfigurerAdapter</b>{<br/>
}

7. after creating a class we need to override one method of WebSecurity class i.e <b><u>UserDeatilsService()</u></b>

> public class ApplicationSecurityConfig extends WebSecurityConfigurerAdapter{<br/>
	@Bean
	@Override
	protected UserDetailsService userDetailsService() {	
	}
}

8. Inside this method we need to create those users list how able to login for now I just add one user
> protected UserDetailsService userDetailsService() {
		List<UserDetails> users=new ArrayList<>();
		users.add(User.withDefaultPasswordEncoder().username("deepanshu").password("1234").roles("USER").build());
		return new InMemoryUserDetailsManager(users);
	}
    
Note : <b>InMemoryUserDeatilsManager</u> class is used for save data inMemory and we not create any class <u>it's all classes provided by Spring-Security</u> but soon when we connect our application with Database then we need to work on those things.