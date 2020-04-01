### 搭建框架是出现的一些错误，记录一下

````
spring-boot-starter-web
spring-boot-starter-gateway
两个包之间会冲突

````

````
项目的打包类型：pom、jar、war
packaging 默认是jar类型，
pom  父类型都为pom类型
jar 内部调用或者是作服务使用
war 需要部署的项目
 
<packaging>pom</packaging> 找不到配置文件
````


````
SpringBoot对应SpringCloud版本号
https://start.spring.io/actuator/info
[spring-cloud]内容对照

Spring IO Platform与SpringBoot版本对应关系
https://blog.csdn.net/nnsword/article/details/86979647
https://spring.io/projects/platform#learn
````

````
Exception in thread "main" java.lang.NoClassDefFoundError: org/springframework/util/unit/DataSize
maven compile 
pom版本问题
````

````
ERROR 27915 --- [0.0-8081-exec-1] o.a.c.c.C.[.[.[/].[dispatcherServlet]    : 
Servlet.service() for servlet [dispatcherServlet] in context with path [] threw exception [Request processing failed; nested exception is feign.RetryableException: Operation timed out (Connection timed out) executing GET http://spring-cloud-producer/hello?name=dfdsf] with root cause
新项目出现问题，先查看服务端口是否被占用
localhost:8080 访问没有问题
192.168.1.101:8080 访问有问题， 就改项目端口
````


````
Cannot load driver class: com.mysql.cj.jdbc.Driver
检查数据库版本
mysql 
select version()

com.mysql.jdbc.Driver是mysql-connector-java 5中的，而com.mysql.cj.jdbc.Driver是mysql-connector-java 6中的。

1、JDBC连接Mysql5需用com.mysql.jdbc.Driver，例如：
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/test?useUnicode=true&characterEncoding=utf8&useSSL=false
username=root
password=root

2、JDBC连接Mysql6需用com.mysql.cj.jdbc.Driver，同时需要指定时区serverTimezone，例如：
driverClassName=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://localhost:3306/test?serverTimezone=UTC&?useUnicode=true&characterEncoding=utf8&useSSL=false
username=root
password=root

3、设定时区时，serverTimezone=UTC比中国时间早8个小时，若在中国，可设置serverTimezone=Asia/Shanghai或者serverTimezone=Hongkong，例如：
driverClassName=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://localhost:3306/test?serverTimezone=Asia/Shanghai&?useUnicode=true&characterEncoding=utf8&useSSL=false
username=root
password=root

4、如果mysql-connector-java用的6.0以上的，如：
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>6.0.6</version>
</dependency>
但是你的driver用的还是com.mysql.jdbc.Driver就会报错，此时需要把com.mysql.jdbc.Driver改为com.mysql.cj.jdbc.Driver。

```