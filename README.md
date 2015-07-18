# mybatis-generator-sample
mybatis-generator-sample

# 使用步骤
1.添加mybatis-generator-maven-plugin到pom.xml

``` xml
<build>
    <finalName>mybatis_generator</finalName>
    <plugins>
        <plugin>
            <groupId>org.mybatis.generator</groupId>
            <artifactId>mybatis-generator-maven-plugin</artifactId>
            <version>1.3.2</version>
        </plugin>
    </plugins>
</build>
```

2.添加配置文件`generatorConfig.xml`到目录`src/main/resources/`下

``` xml
 <?xml version="1.0" encoding="UTF-8"?>
 <!DOCTYPE generatorConfiguration
         PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
         "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
 
 
 <generatorConfiguration>
     <!--数据库驱动jar -->
     <classPathEntry location="/home/zhiwen/java/mysql-connector-java-5.1.6.jar" />
 
     <context id="MysqlContext" targetRuntime="MyBatis3" defaultModelType="flat">
         <!--去除注释  -->
         <commentGenerator>
             <property name="suppressAllComments" value="true" />
         </commentGenerator>
 
         <!--数据库连接 -->
         <jdbcConnection driverClass="com.mysql.jdbc.Driver"
                         connectionURL="jdbc:mysql://localhost:3306/mybatis_generator"
                         userId="root"
                         password="zzwzzw">
         </jdbcConnection>
         <!--默认false
            Java type resolver will always use java.math.BigDecimal if the database column is of type DECIMAL or NUMERIC.
          -->
         <javaTypeResolver >
             <property name="forceBigDecimals" value="false" />
         </javaTypeResolver>
 
         <!--生成实体类 指定包名 以及生成的地址 （可以自定义地址，但是路径不存在不会自动创建  使用Maven生成在target目录下，会自动创建） -->
         <javaModelGenerator targetPackage="org.jast.mybatisgenerator.entity" targetProject="/home/zhiwen/IdeaProjects/mybatis-generator-sample/src/main/java">
             <property name="enableSubPackages" value="false" />
             <property name="trimStrings" value="true" />
         </javaModelGenerator>
         <!--生成SQLMAP文件 -->
         <sqlMapGenerator targetPackage="org.jast.mybatisgenerator.mapper"  targetProject="/home/zhiwen/IdeaProjects/mybatis-generator-sample/src/main/resources">
             <property name="enableSubPackages" value="false" />
         </sqlMapGenerator>
         <!--生成Dao文件 可以配置 type="XMLMAPPER"生成xml的dao实现  context id="DB2Tables" 修改targetRuntime="MyBatis3"  -->
         <javaClientGenerator type="XMLMAPPER" targetPackage="org.jast.mybatisgenerator.dao"  targetProject="/home/zhiwen/IdeaProjects/mybatis-generator-sample/src/main/java">
             <property name="enableSubPackages" value="false" />
         </javaClientGenerator>
 
         <!--对应数据库表 mysql可以加入主键自增 字段命名 忽略某字段等-->
         <table tableName="person" />
         <table tableName="pet" />
 
     </context>
 </generatorConfiguration>```

3.运行mybatis-generator-maven-plugin

命令：

```
mvn mybatis-generator:generate
```

运行后就会生成相应的文件了。

4.说明

注重要的还是generatorConfig.xml文件的配置