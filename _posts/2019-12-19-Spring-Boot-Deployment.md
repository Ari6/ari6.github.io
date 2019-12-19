---
layout: post
categories: [Java, Spring Boot, Tomcat, Apache]
---

# Spring Boot Deployment on a server

Well, it took longer time than I thought to deploy my Spring Boot application to the server. Deployment itself was easy enough but what I wanted to do brought a little bit complicated tasks.
My goal was all traffic is encrypted by SSL and application can be subdomain becasue there is a website running under SSL.

## TL; DR
* Use Tomcat on a server, not with Spring boot.
* Setup SSL configration with Apache, then use ProxyPass to pass the trafic to tomcat.
* Application class which is annotated @SpringBootApplication needs to extend SpringBootServletInitializer. Look [here](https://docs.spring.io/spring-boot/docs/current/reference/html/howto.html#howto-traditional-deployment).  

## Tools
* Apache 2.4.x
* Tomcat 8.x
* IntelliJ 2019.3
* Gradle 5.6.x 
* CentOS 7
* Java 8


## First, just deployment
To deploy a spring boot application to a server is easy enough. 
\* I will not mentioin how to make Spring applicatioin or gradle configuration here.

Once you create your application with gradle, just run build to make .jar file.

```bash
gradle build   # or gradlew
```

You should be able to get a jar file under build/libs/ directory. You need to copy this jar file to your target server.

Then,

```bash
java -jar yourjar.jar
```

You should be able to access with domain or ip address with port 8080. If you have an index or controller for "/".

```
http://localhost:8080
```

## URL is ugly using port nunber
I think URL using port number is ugly and did not want to a port for that. So I searched a solution.

### ProxyPass with ajp
Tomcat has AJP connector to communicate via AJP protocol. Some website says that you can use mod_proxy to forward traffics to tomcat with ajp.

```apache
ProxyPass / ajp://domain
```

But it did not go through. Some of error message indicated that cannot pass traffic to tomcat properly because of having SSL.

For Spring application configuration, I reffered [this website](https://www.thomasvitale.com/https-spring-boot-ssl-certificate/) to set up my application. I tool so many hours to figure this out but it does not make my web app work. * This website information is kind of old so you need to change some code, such as TomcatEmbeddedServletContainerFactory.

### Gave up using buit-in Tomcat
I gave up using Spring boot built-in Tomcat because I wanted to have more apps to the same server so I had a plan to deploy Tomcat on the server anyway.

To use Tomcat on a server, you should use war file instead of jar file. You can just add these lines below.

```gradle
plugins {
	id 'war'
}
```

and run

```bash
gradle bootWar
```

You should get war file under build/libs/ directory.

I installed Tomcat 9 to my CentOS server. Default CentOS7 yum try to bring Tomcat 7. If you want to have the version you want, just go and check [Tomcat website](http://tomcat.apache.org/) to download files.
[This](https://www.digitalocean.com/community/tutorials/how-to-install-apache-tomcat-8-on-centos-7) was useful.

My server does not have Desktop environment so I did not use GUI management for setting up and deploy war files but these are easy with CUI. References: [#1](https://tomcat.apache.org/tomcat-8.5-doc/config/context.html) [#2](https://tomcat.apache.org/tomcat-9.0-doc/config/host.html)

If you set autoDeploy=true, you just need to copy war file to whereever your configuration under the root directory of applications. usually, webapps.

### Wait, showing 404
Long story short, you need to change your Spring Boot app if you made it for jar file with built-in server.
Please see [here.](https://docs.spring.io/spring-boot/docs/current/reference/html/howto.html#howto-traditional-deployment)

```java
@SpringBootApplication
public class Application extends SpringBootServletInitializer {

    @Override
    protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
        return application.sources(Application.class);
    }

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

Then, your application should run on Tomcat on the server.

### SSL
Since I run apache and tomcat on the same server, I just set up subdomain's all port 80 traffic to 443 and the VirtualHost has

```apache
ProxyPass /appname/ http://localhost:8080/appname/
```
so that these traffic can be passed to Tomcat.
I know this is bad practice but I did not want to build another server for just testing.

If web server and application server are separated, you should not use this because traffic between web server and application server is not encrypted.
