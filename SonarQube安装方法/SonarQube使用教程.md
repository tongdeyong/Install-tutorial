# SonarQube使用教程--“MAVEN项目”

### 一、配置要求
	1. maven 3.x
	2. sonarQube 已安装
	3. 已安装java8或更高版本
	4. 已在sonarQube安装您要分析的相对应的语言插件
	5. （可选）您已阅读"Analyzing Code Source"
Analyzing Code Source: [https://docs.sonarqube.org/latest/analysis/overview/](https://docs.sonarqube.org/latest/analysis/overview/)

### 二、全局设置
	1. 编辑位于$ MAVEN_HOME / conf或〜/ .m2中的  settings.xml文件，以设置插件前缀和可选的SonarQube服务器URL。
	2. 在maven设置文件setting文件中的对应节点添加如下内容：

		<settings>
		<pluginGroups>
			<pluginGroup>org.sonarsource.scanner.maven</pluginGroup>
		</pluginGroups>
		<profiles>
			<profile>
				<id>sonar</id>
				<activation>
					<activeByDefault>true</activeByDefault>
				</activation>
				<properties>
					<!-- Optional URL to server. Default value is http://localhost:9000 -->
					<sonar.host.url>  
					  http://localhost:9000  <!--注意修改此处的localhost-->
					</sonar.host.url>
				</properties>
			</profile>
		 </profiles>
		</settings>

### 三、分析maven项目

分析Maven项目包括运行Maven目标：sonar:sonar在pom.xml文件所在的目录中。

	mvn clean verify sonar:sonar
  
	#In some situation you may want to run sonar:sonar goal as a dedicated step. Be sure to use install as first step 
	#for multi-module projects
	mvn clean install
	mvn sonar:sonar
 
	#Specify the version of sonar-maven-plugin instead of using the latest. See also 'How to Fix Version of Maven 
	#Plugin' below.
	mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar
	
其实只需要运行mvn sonar:sonar就可以了

### 四、配置SonarQube分析(可选)

分析参数列在[“分析参数”](https://docs.sonarqube.org/latest/analysis/analysis-parameters/)页面上。你必须在pom.xml的properties部分配置它们，如下所示：

	<properties>
	<sonar.exclusions> [...] </sonar.exclusions>
	</properties>
	
### 五、安全

	任何被授予执行分析权限的用户都可以运行分析。
	如果任何人或组未被授予执行分析 权限，或者SonarQube实例受到保护（该  sonar.forceAuthentication 属性设置为true)，
	则必须通过该属性提供具有执行分析权限的用户的分析令牌  sonar.login。
	示例： sonar-scanner -Dsonar.login=[my analysis token]

### 六、从SonarQube分析中排除模块

你可以：

* 在要排除的模块的pom.xml中定义属性<sonar.skip> true </sonar.skip>
* 使用构建配置文件来排除某些模块（如集成测试）
* 使用Advanced Reactor Options（例如“-pl”）。例如mvn声纳：sonar -pl！module2

### 七、如何修复Maven插件的版本
	
	<build>
	  <pluginManagement>
		<plugins>
		  <plugin>
			<groupId>org.sonarsource.scanner.maven</groupId>
			<artifactId>sonar-maven-plugin</artifactId>
			<version>3.6.0.1398</version>
		  </plugin>
		</plugins>
	  </pluginManagement>
	</build>

官网安装文档：[https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner+for+Maven](https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner+for+Maven)
	
### 八：总结：

	1.按步骤一，设置全局配置
	2.安装maven插件版本（可不安）
	3.在含有pom.xml文件夹内运行maven命令：mvn sonar:sonar