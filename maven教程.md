## maven介绍
Maven是一个项目管理和综合工具。Maven提供了开发人员构建一个完整的生命周期框架。开发团队可以自动完成项目的基础工具建设，Maven使用标准的目录结构和默认构建生命周期。

在多个开发团队环境时，Maven可以设置按标准在非常短的时间里完成配置工作。由于大部分项目的设置都很简单，并且可重复使用，Maven让开发人员的工作更轻松，同时创建报表，检查，构建和测试自动化设置。

Maven主要目标是提供给开发人员：

- 项目是可重复使用，易维护，更容易理解的一个综合模型。
- 插件或交互的工具，这种声明性的模式。

Maven项目的结构和内容在一个XML文件中声明，pom.xml 项目对象模型（POM），这是整个Maven系统的基本单元

## maven下载
http://maven.apache.org/download.cgi

解压到D盘根目录

配置环境变量  MAVEN_HOME=D:\apache-maven-3.5.3   PATH=...;MAVEN_HOME\bin

验证是否安装成功：mvn -version



## 修改中央仓库地址 ##
maven核心配置文件：
D:\apache-maven-3.5.2\conf\settings.xml

在mirrors节点里加入如下代码：

	<mirror>
      <!--This sends everything else to /public -->
      <id>nexus</id>
      <mirrorOf>*</mirrorOf> 
      <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
    </mirror>
    <mirror>
      <!--This is used to direct the public snapshots repo in the 
          profile below over to a different nexus group -->
      <id>nexus-public-snapshots</id>
      <mirrorOf>public-snapshots</mirrorOf> 
      <url>http://maven.aliyun.com/nexus/content/repositories/snapshots/</url>
    </mirror>


## maven项目创建方式 ##

java项目：maven-archetype-quickstart

javaweb项目：maven-archetype-webapp

###1：命令行创建
	创建java项目
	mvn archetype:generate -DgroupId=com.dayuan.atm -DartifactId=atm -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false -DarchetypeCatalog=internal
	
	创建javaweb项目
	mvn archetype:generate -DgroupId=com.dayuan.atm -DartifactId=atm -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false -DarchetypeCatalog=internal
###2：借助工具，比如idea、eclipse


###Maven项目的目录结构
	MavenProjectRoot(web项目根目录)
	   |----src
	   |     |----main
	   |     |         |----java ——存放项目的.java文件
	   |     |         |----resources ——存放项目资源文件，如spring, hibernate配置文件
	   |     |         |----webapp ——web根目录，存静态文件、jsp、web.xml
	   |     |----test
	   |     |         |----java ——存放所有测试.java文件，如JUnit测试类
	   |     |         |----resources ——存放项目资源文件，如spring, hibernate配置文件
	   |----target ——项目输出位置(编译时自动生成)
	   |----pom.xml ----用于标识该项目是一个Maven项目

注意：如果是web项目需要创建webapp文件夹，否则无需创建

## 本地仓库地址

C:\Users\Administrator\.m2\repository

## 常用命令 ##
编译后的字节码文件目录（自动创建）：项目目录/target/classes

打包后的jar、war文件目录：项目目录/target

- 编译  mvn compile
- 清除编译的文件  mvn  clean
- 可以组合使用 mvn clean compile
- 打包，忽略测试用例 mvn clean package -Dmaven.test.skip=true -U  （-U强制更新jar，忽略本地仓库）
- 安装命令(install包含package命令，install会把项目安装到本地仓库) ，区别：打包后安装到本地库  mvn clean install -Dmaven.test.skip=true -U


## 常用依赖 ##

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<spring.version>4.3.9.RELEASE</spring.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>3.8.1</version>
			<scope>test</scope>
		</dependency>
		<!-- Servlet -->
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>javax.servlet-api</artifactId>
			<version>3.1.0</version>
			<scope>provided</scope>
		</dependency>

		<!-- JSP -->
		<dependency>
			<groupId>javax.servlet.jsp</groupId>
			<artifactId>jsp-api</artifactId>
			<version>2.2</version>
			<scope>provided</scope>
		</dependency>

		<!-- JSTL -->
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>jstl</artifactId>
			<version>1.2</version>
			<scope>runtime</scope>
		</dependency>

		<!--mysql驱动-->
	    <dependency>
	      <groupId>mysql</groupId>
	      <artifactId>mysql-connector-java</artifactId>
	      <version>5.1.46</version>
	    </dependency>
	
	    <!--mybatis-->
	    <dependency>
	      <groupId>org.mybatis</groupId>
	      <artifactId>mybatis</artifactId>
	      <version>3.4.6</version>
	    </dependency>

		<!-- spring 环境 -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-webmvc</artifactId>
			<version>${spring.version}</version>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-web</artifactId>
			<version>${spring.version}</version>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-aop</artifactId>
			<version>${spring.version}</version>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-beans</artifactId>
			<version>${spring.version}</version>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-context</artifactId>
			<version>${spring.version}</version>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-core</artifactId>
			<version>${spring.version}</version>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-jdbc</artifactId>
			<version>${spring.version}</version>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-tx</artifactId>
			<version>${spring.version}</version>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-expression</artifactId>
			<version>${spring.version}</version>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-context-support</artifactId>
			<version>${spring.version}</version>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-orm</artifactId>
			<version>${spring.version}</version>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-aspects</artifactId>
			<version>${spring.version}</version>
		</dependency>
		<!-- spring 环境 -->


	</dependencies>

	<build>
    <finalName>atm07_maven</finalName>

    <plugins>
      <!--编译插件
                source： 源代码编译版本；
                target： 目标平台编译版本；
                encoding： 字符集编码。-->
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <configuration>
          <source>1.8</source>
          <target>1.8</target>
          <encoding>${project.build.sourceEncoding}</encoding>
        </configuration>
      </plugin>
    </plugins>

    <resources>
      <resource>
        <directory>src/main/java</directory>
        <includes>
          <include>**/*.properties</include>
          <include>**/*.xml</include>
        </includes>
        <filtering>false</filtering>
      </resource>
      <resource>
        <directory>src/main/resources</directory>
        <includes>
          <include>**/*.properties</include>
          <include>**/*.xml</include>
        </includes>
        <filtering>false</filtering>
      </resource>
    </resources>
  	</build>



##maven创建的web项目默认web.xml版本是2.3版本，升级版本如下：

	<?xml version="1.0" encoding="UTF-8"?>
	<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
	         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
	         version="4.0">
	
	</web-app>


## Maven依赖中的scope详解 ##

scope的默认值是compile

maven分几个阶段：编译阶段、测试阶段、运行阶段、

###scope的分类
compile

编译阶段+测试阶段+运行阶段

打包会打进去。


provided

编译阶段+测试阶段+运行阶段

打包的时候不会打进去


test

测试阶段：测试代码的编译，执行

打包的时候不会打进去

runntime

测试阶段+运行阶段

runntime表示被依赖项目无需参与项目的编译，不过后期的测试和运行周期需要其参与。

打包会打进去


system （导入maven以外的jar文件）

编译阶段+测试阶段+运行阶段

打包会打进去