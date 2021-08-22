# springBoot

## 1.四大核心

自动配置：

![image-20210418161520888](C:\Users\文文\AppData\Roaming\Typora\typora-user-images\image-20210418161520888.png)

起步依赖:Starter依赖将所需的常见依赖按组聚集在一起，形成单条依赖

![image-20210418163731578](C:\Users\文文\AppData\Roaming\Typora\typora-user-images\image-20210418163731578.png)



Actuator:让你能够深入运行中的spring boot应用程序,查看内部信息

命令行界面:spring boot可选特性,主要针对Groovy

## 2.项目搭建

### 2.1 web项目

> > pom.xml

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.4.4</version>
    <relativePath/>
</parent>


 <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-web</artifactId>
 </dependency>
```

```java
@SpringBootApplication // springboot核心注解，自动配置
public class SpringbootApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringbootApplication.class, args);
    }

}
```

### 2.2 集成MyBatis

> > 添加起步依赖

```xml
<!--集成Mybatis-->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
</dependency>
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>1.3.0</version>
</dependency>
```

> > 核心配置

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/springboot?useUnicode=true&characterEncoding=utf-8&zeroDateTimeBehavior=convertToNull&allowMultiQueries=true
    driver-class-name: com.mysql.cj.jdbc.Driver
    password: 1234
    username: root
mybatis:
  mapperLocations: classpath:mapper/*.xml  #指定mapper.xml位置
  type-aliases-package: com.grapes.springboot.domain #指定映射对象位置
  
```

> > Mybatis基本使用

```java
@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
public class Domain {
    private Integer domainId;
    private String domainName;
    private Date date;
}
```

```java
/**
* Mappper接口
*/
@Mapper  // 也可以在启动类上加注解：@MapperScan("com.grapes.springboot.mapper")，总之是交给      // spring管理即可
public interface IDomainMapper {
    Domain getDomainById(Integer id);
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.grapes.springboot.mapper.IDomainMapper">
    <resultMap id="domainMap" type="com.grapes.springboot.domain.Domain">
        <result property="domainId" column="domain_id"/>
        <result property="domainName" column="domain_name"/>
        <result property="date" column="domain_date"/>
    </resultMap>
    <select id="getDomainById" resultMap="domainMap">
        select *
        from t_domain
        where domain_id=#{id}
    </select>
</mapper>
```

CREATE TABLE t_domain (
  `domain_id` INT(20) NOT NULL AUTO_INCREMENT,
  `domain_name` VARCHAR(25) DEFAULT NULL,
  `domain_date` DATETIME DEFAULT NULL,
  PRIMARY KEY (`domain_id`)
) ENGINE=INNODB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8;

### 2.3 集成Redis



