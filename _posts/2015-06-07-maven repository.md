---
layout: post
title: maven repository
date: 2015-06-07 23:51
categories: []
tags: []
---
##什么是Maven仓库
在不用Maven的时候，比如说以前我们用Ant构建项目，在项目目录下，往往会看到一个名为/lib的子目录，那里存放着各类第三方依赖jar文件，如log4j.jar，junit.jar等等。每建立一个项目，你都需要建立这样的一个/lib目录，然后复制一对jar文件，这是很明显的重复。重复永远是噩梦的起点，多个项目不共用相同的jar文件，不仅会造成磁盘资源的浪费，也使得版本的一致性管理变得困难。此外，如果你使用版本管理工具，如SVN（你没有使用版本管理工具？马上试试SVN吧，它能帮你解决很多头疼的问题），你需要将大量的jar文件提交到代码库里，可是版本管理工具在处理二进制文件方面并不出色。
Maven仓库就是放置所有JAR文件（WAR，ZIP，POM等等）的地方，所有Maven项目可以从同一个Maven仓库中获取自己所需要的依赖JAR，这节省了磁盘资源。此外，由于Maven仓库中所有的JAR都有其自己的坐标，该坐标告诉Maven它的组ID，构件ID，版本，打包方式等等，因此Maven项目可以方便的进行依赖版本管理。你也不在需要提交JAR文件到SCM仓库中，你可以建立一个组织层次的Maven仓库，供所有成员使用。
简言之，Maven仓库能帮助我们管理构件（主要是JAR）。
 
##[]()本地仓库 vs. 远程仓库
运行Maven的时候，Maven所需要的任何构件都是直接从本地仓库获取的。如果本地仓库没有，它会首先尝试从远程仓库下载构件至本地仓库，然后再使用本地仓库的构件。
比如说，你的项目配置了junit-3.8的依赖，在你运行**mvn test** 的时候，Maven需要使用junit-3.8的jar文件，它首先根据坐标查找本地仓库，如果找到，就直接使用。如果没有，Maven会检查可用的远程仓库配置，然后逐个尝试这些远程仓库去下载junit-3.8的jar文件，如果远程仓库存在该文件，Maven会将其下载到本地仓库中，继而使用。如果尝试过所有远程仓库之后，Maven还是没能够下载到该文件，它就会报错。
Maven缺省的本地仓库地址为*${user.home}/.m2/repository* 。也就是说，一个用户会对应的拥有一个本地仓库。
你也可以自定义本地仓库的位置，修改*${user.home}/.m2/settings.xml* ：
Xml代码 [![复制代码](http://juvenshun.javaeye.com/images/icon_copy.gif)](http://juvenshun.javaeye.com/blog/359256# "复制代码")1. **<settings>**  
2.   ...   
3.   **<localRepository>**D:/java/repository**</localRepository>**  
4.   ...   
5. **</settings>**  

**[xml]** [view
 plain](http://blog.csdn.net/joewolf/article/details/4876604# "view plain")[copy](http://blog.csdn.net/joewolf/article/details/4876604# "copy")1. <settings>  
2.   ...  
3.   <localRepository>D:/java/repository</localRepository>  
4.   ...  
5. </settings>  

你还可以在运行时指定本地仓库位置：
**mvn clean install -Dmaven.repo.local=/home/juven/myrepo/**
还有一点需要理解的是，当我们运行install的时候，Maven实际上是将项目生成的构件安装到了本地仓库，也就是说，只有install了之后，其它项目才能使用此项目生成的构件。
了解了本地仓库，接着了解一下Maven缺省的远程仓库，即Maven中央仓库。
安装好Maven之后，我们可以建立一个简单的项目，配置一些简单的依赖，然后运行mvn clean install，项目就构建好了。我们没有手工的去下载任何jar文件，这一切都是因为Maven中央仓库的存在，当Maven在本地仓库找不到需要的jar文件时，它会查找远程仓库，而一个原始的Maven安装就自带了一个远程仓库——Maven中央仓库。
这个Maven中央仓库是在哪里定义的呢？在我的机器上，我安装了maven-2.0.10，我可以找到这个文件：*${M2_HOME}/lib/maven-2.0.10-uber.jar* ，打开该文件，能找到超级POM：*/org/apache/maven/project/pom-4.0.0.xml* ，它是所有Maven POM的父POM，所有Maven项目继承该配置，你可以在这个POM中发现如下配置：
Xml代码 [![复制代码](http://juvenshun.javaeye.com/images/icon_copy.gif)](http://juvenshun.javaeye.com/blog/359256# "复制代码")1. **<repositories>**  
2.   **<repository>**  
3.     **<id>**central**</id>**  
4.     **<name>**Maven Repository Switchboard**</name>**  
5.     **<layout>**default**</layout>**  
6.     **<url>**http://repo1.maven.org/maven2**</url>**  
7.     **<snapshots>**  
8.       **<enabled>**false**</enabled>**  
9.     **</snapshots>**  
10.   **</repository>**  
11. **</repositories>**  

**[xml]** [view
 plain](http://blog.csdn.net/joewolf/article/details/4876604# "view plain")[copy](http://blog.csdn.net/joewolf/article/details/4876604# "copy")1. <repositories>  
2.   <repository>  
3.     <id>central</id>  
4.     <name>Maven Repository Switchboard</name>  
5.     <layout>default</layout>  
6.     <url>http://repo1.maven.org/maven2</url>  
7.     <snapshots>  
8.       <enabled>false</enabled>  
9.     </snapshots>  
10.   </repository>  
11. </repositories>  

关于远程仓库的配置，下面的小节我会详细解释，这里我们只要知道，中央仓库的id为central，远程url地址为http://repo1.maven.org/maven2，它关闭了snapshot版本构件下载的支持。
 
##[]()在POM中配置远程仓库
前面我们看到超级POM配置了ID为central的远程仓库，我们可以在POM中配置其它的远程仓库。这样做的原因有很多，比如你有一个局域网的远程仓库，使用该仓库能大大提高下载速度，继而提高构建速度，也有可能你依赖的一个jar在central中找不到，它只存在于某个特定的公共仓库，这样你也不得不添加那个远程仓库的配置。
这里我配置一个远程仓库指向中央仓库的中国镜像：
Xml代码 [![复制代码](http://juvenshun.javaeye.com/images/icon_copy.gif)](http://juvenshun.javaeye.com/blog/359256# "复制代码")1. **<project>**  
2. ...   
3.   **<repositories>**  
4.     **<repository>**  
5.       **<id>**maven-net-cn**</id>**  
6.       **<name>**Maven China Mirror**</name>**  
7.       **<url>**http://maven.net.cn/content/groups/public/**</url>**  
8.       **<releases>**  
9.         **<enabled>**true**</enabled>**  
10.       **</releases>**  
11.       **<snapshots>**  
12.         **<enabled>**false**</enabled>**  
13.       **</snapshots>**  
14.     **</repository>**  
15.   **</repositories>**  
16.   **<pluginRepositories>**  
17.     **<pluginRepository>**  
18.       **<id>**maven-net-cn**</id>**  
19.       **<name>**Maven China Mirror**</name>**  
20.       **<url>**http://maven.net.cn/content/groups/public/**</url>**  
21.       **<releases>**  
22.         **<enabled>**true**</enabled>**  
23.       **</releases>**  
24.       **<snapshots>**  
25.         **<enabled>**false**</enabled>**  
26.       **</snapshots>**    
   
27.     **</pluginRepository>**  
28.   **</pluginRepositories>**  
29. ...   
30. **</project>**  

**[xml]** [view
 plain](http://blog.csdn.net/joewolf/article/details/4876604# "view plain")[copy](http://blog.csdn.net/joewolf/article/details/4876604# "copy")1. <project>  
2. ...  
3.   <repositories>  
4.     <repository>  
5.       <id>maven-net-cn</id>  
6.       <name>Maven China Mirror</name>  
7.       <url>http://maven.net.cn/content/groups/public/</url>  
8.       <releases>  
9.         <enabled>true</enabled>  
10.       </releases>  
11.       <snapshots>  
12.         <enabled>false</enabled>  
13.       </snapshots>  
14.     </repository>  
15.   </repositories>  
16.   <pluginRepositories>  
17.     <pluginRepository>  
18.       <id>maven-net-cn</id>  
19.       <name>Maven China Mirror</name>  
20.       <url>http://maven.net.cn/content/groups/public/</url>  
21.       <releases>  
22.         <enabled>true</enabled>  
23.       </releases>  
24.       <snapshots>  
25.         <enabled>false</enabled>  
26.       </snapshots>      
27.     </pluginRepository>  
28.   </pluginRepositories>  
29. ...  
30. </project>  

我们先看一下<repositories>的配置，你可以在它下面添加多个<repository> ，每个<repository>都有它唯一的ID，一个描述性的name，以及最重要的，远程仓库的url。此外，<releases><enabled>true</enabled></releases>告诉Maven可以从这个仓库下载releases版本的构件，而<snapshots><enabled>false</enabled></snapshots>告诉Maven不要从这个仓库下载snapshot版本的构件。禁止从公共仓库下载snapshot构件是推荐的做法，因为这些构件不稳定，且不受你控制，你应该避免使用。当然，如果你想使用局域网内组织内部的仓库，你可以激活snapshot的支持。
关于<repositories>的更详细的配置及相关解释，请参考：http://www.sonatype.com/books/maven-book/reference_zh/apas02s08.html。
至于<pluginRepositories>，这是配置Maven从什么地方下载插件构件（Maven的所有实际行为都由其插件完成）。该元素的内部配置和<repository>完全一样，不再解释。
 
##[]()在settings.xml中配置远程仓库
我们知道了如何在POM中配置远程仓库，但考虑这样的情况：在一个公司内部，同时进行这3个项目，而且以后随着这几个项目的结束，越来越多的项目会开始；同时，公司内部建立一个Maven仓库。我们统一为所有这些项目配置该仓库，于是不得不为每个项目提供同样的配置。问题出现了，这是*重复* ！
其实我们可以做到只配置一次，在哪里配置呢？就是settings.xml。
不过事情没有那么简单，不是简单的将POM中的<repositories>及<pluginRepositories>元素复制到settings.xml中就可以，setting.xml*不直接支持* 这两个元素。但我们还是有一个并不复杂的解决方案，就是利用profile，如下：
Xml代码 [![复制代码](http://juvenshun.javaeye.com/images/icon_copy.gif)](http://juvenshun.javaeye.com/blog/359256# "复制代码")1. **<settings>**  
2.   ...   
3.   **<profiles>**  
4.     **<profile>**  
5.       **<id>**dev**</id>**  
6.       <!-- repositories and pluginRepositories here-->  
7.     **</profile>**  
8.   **</profiles>**  
9.   **<activeProfiles>**  
10.     **<activeProfile>**dev**</activeProfile>**  
11.   **</activeProfiles>**  
12.   ...   
13. **</settings>**  

**[xml]** [view
 plain](http://blog.csdn.net/joewolf/article/details/4876604# "view plain")[copy](http://blog.csdn.net/joewolf/article/details/4876604# "copy")1. <settings>  
2.   ...  
3.   <profiles>  
4.     <profile>  
5.       <id>dev</id>  
6.       <!-- repositories and pluginRepositories here-->  
7.     </profile>  
8.   </profiles>  
9.   <activeProfiles>  
10.     <activeProfile>dev</activeProfile>  
11.   </activeProfiles>  
12.   ...  
13. </settings>  

这里我们定义一个id为dev的profile，将所有repositories以及pluginRepositories元素放到这个profile中，然后，使用<activeProfiles>元素自动激活该profile。这样，你就不用再为每个POM重复配置仓库。
使用profile为settings.xml添加仓库提供了一种用户全局范围的仓库配置。
 
##[]()镜像
如果你的地理位置附近有一个速度更快的central镜像，或者你想覆盖central仓库配置，或者你想为所有POM使用唯一的一个远程仓库（这个远程仓库代理的所有必要的其它仓库），你可以使用settings.xml中的mirror配置。
以下的mirror配置用maven.net.cn覆盖了Maven自带的central：
Xml代码 [![复制代码](http://juvenshun.javaeye.com/images/icon_copy.gif)](http://juvenshun.javaeye.com/blog/359256# "复制代码")1. **<settings>**  
2. ...   
3.   **<mirrors>**  
4.     **<mirror>**  
5.       **<id>**maven-net-cn**</id>**  
6.       **<name>**Maven China Mirror**</name>**  
7.       **<url>**http://maven.net.cn/content/groups/public/**</url>**  
8.       **<mirrorOf>**central**</mirrorOf>**  
9.     **</mirror>**  
10.   **</mirrors>**  
11. ...   
12. **</settings>**  

**[xml]** [view
 plain](http://blog.csdn.net/joewolf/article/details/4876604# "view plain")[copy](http://blog.csdn.net/joewolf/article/details/4876604# "copy")1. <settings>  
2. ...  
3.   <mirrors>  
4.     <mirror>  
5.       <id>maven-net-cn</id>  
6.       <name>Maven China Mirror</name>  
7.       <url>http://maven.net.cn/content/groups/public/</url>  
8.       <mirrorOf>central</mirrorOf>  
9.     </mirror>  
10.   </mirrors>  
11. ...  
12. </settings>  

 
这里唯一需要解释的是<mirrorOf>，这里我们配置central的镜像，我们也可以配置一个所有仓库的镜像，以保证该镜像是Maven唯一使用的仓库：
Xml代码 [![复制代码](http://juvenshun.javaeye.com/images/icon_copy.gif)](http://juvenshun.javaeye.com/blog/359256# "复制代码")1. **<settings>**  
2. ...   
3.   **<mirrors>**  
4.     **<mirror>**  
5.       **<id>**my-org-repo**</id>**  
6.       **<name>**Repository in My Orgnization**</name>**  
7.       **<url>**http://192.168.1.100/maven2**</url>**  
8.       **<mirrorOf>*****</mirrorOf>**  
9.     **</mirror>**  
10.   **</mirrors>**  
11. ...   
12. **</settings>**  

**[xml]** [view
 plain](http://blog.csdn.net/joewolf/article/details/4876604# "view plain")[copy](http://blog.csdn.net/joewolf/article/details/4876604# "copy")1. <settings>  
2. ...  
3.   <mirrors>  
4.     <mirror>  
5.       <id>my-org-repo</id>  
6.       <name>Repository in My Orgnization</name>  
7.       <url>http://192.168.1.100/maven2</url>  
8.       <mirrorOf>*</mirrorOf>  
9.     </mirror>  
10.   </mirrors>  
11. ...  
12. </settings>  

关于更加高级的镜像配置，可以参考：http://maven.apache.org/guides/mini/guide-mirror-settings.html。
 
##[]()分发构件至远程仓库
**mvn install** 会将项目生成的构件安装到本地Maven仓库，**mvn deploy** 用来将项目生成的构件分发到远程Maven仓库。本地Maven仓库的构件只能供当前用户使用，在分发到远程Maven仓库之后，所有能访问该仓库的用户都能使用你的构件。
我们需要配置POM的distributionManagement来指定Maven分发构件的位置，如下：
Xml代码 [![复制代码](http://juvenshun.javaeye.com/images/icon_copy.gif)](http://juvenshun.javaeye.com/blog/359256# "复制代码")1. **<project>**  
   
2.   ...     
3.   **<distributionManagement>**  
   
4.     **<repository>**  
   
5.       **<id>**nexus-releases**</id>**  
   
6.       **<name>**Nexus Release Repository**</name>**  
   
7.       **<url>**http://127.0.0.1:8080/nexus/content/repositories/releases/**</url>**  
   
8.     **</repository>**  
   
9.     **<snapshotRepository>**  
   
10.       **<id>**nexus-snapshots**</id>**  
   
11.       **<name>**Nexus Snapshot Repository**</name>**  
   
12.       **<url>**http://127.0.0.1:8080/nexus/content/repositories/snapshots/**</url>**  
   
13.     **</snapshotRepository>**  
   
14.   **</distributionManagement>**  
   
15.   ...     
16. **</project>**    

**[xml]** [view
 plain](http://blog.csdn.net/joewolf/article/details/4876604# "view plain")[copy](http://blog.csdn.net/joewolf/article/details/4876604# "copy")1. <project>    
2.   ...    
3.   <distributionManagement>    
4.     <repository>    
5.       <id>nexus-releases</id>    
6.       <name>Nexus Release Repository</name>    
7.       <url>http://127.0.0.1:8080/nexus/content/repositories/releases/</url>    
8.     </repository>    
9.     <snapshotRepository>    
10.       <id>nexus-snapshots</id>    
11.       <name>Nexus Snapshot Repository</name>    
12.       <url>http://127.0.0.1:8080/nexus/content/repositories/snapshots/</url>    
13.     </snapshotRepository>    
14.   </distributionManagement>    
15.   ...    
16. </project>    

Maven区别对待release版本的构件和snapshot版本的构件，snapshot为开发过程中的版本，实时，但不稳定，release版本则比较稳定。Maven会根据你项目的版本来判断将构件分发到哪个仓库。
一般来说，分发构件到远程仓库需要认证，如果你没有配置任何认证信息，你往往会得到401错误。这个时候，如下在settings.xml中配置认证信息：
Xml代码 [![复制代码](http://juvenshun.javaeye.com/images/icon_copy.gif)](http://juvenshun.javaeye.com/blog/359256# "复制代码")1. **<settings>**  
   
2.   ...     
3.   **<servers>**  
   
4.     **<server>**  
   
5.       **<id>**nexus-releases**</id>**  
   
6.       **<username>**admin**</username>**  
   
7.       **<password>**admin123**</password>**  
   
8.     **</server>**  
   
9.     **<server>**  
   
10.       **<id>**nexus-snapshots**</id>**  
   
11.       **<username>**admin**</username>**  
   
12.       **<password>**admin123**</password>**  
   
13.     **</server>**    
   
14.   **</servers>**  
   
15.   ...     
16. **</settings>**  

**[xml]** [view
 plain](http://blog.csdn.net/joewolf/article/details/4876604# "view plain")[copy](http://blog.csdn.net/joewolf/article/details/4876604# "copy")1. <settings>    
2.   ...    
3.   <servers>    
4.     <server>    
5.       <id>nexus-releases</id>    
6.       <username>admin</username>    
7.       <password>admin123</password>    
8.     </server>    
9.     <server>    
10.       <id>nexus-snapshots</id>    
11.       <username>admin</username>    
12.       <password>admin123</password>    
13.     </server>      
14.   </servers>    
15.   ...    
16. </settings>  

需要注意的是，settings.xml中server元素下id的值必须与POM中repository或snapshotRepository下id的值完全一致。将认证信息放到settings下而非POM中，是因为POM往往是它人可见的，而settings.xml是本地的。
 
##[]()小结
本文介绍了Maven仓库，它是什么？本地仓库，远程仓库，中央仓库具体是指什么？并介绍了如何在POM中配置项目层次的仓库，在settings中配置用户层次的仓库，以及mirror。本文还介绍了如何安装构件到本地仓库，如何分发构件至仓库。
