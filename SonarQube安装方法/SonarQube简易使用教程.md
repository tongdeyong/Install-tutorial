# SonarQube简易使用教程

一、在maven的setting文件中的对应节点中添加如下设置：

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
				  http://47.94.108.58:9000  <!--注意修改此处的localhost-->
				</sonar.host.url>
			</properties>
		</profile>
	 </profiles>
	</settings>
	
二、在pom.xml文件中添加

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
	
三、控制台中输入

	mvn sonar:sonar
	
四、进入网站：[http://dy.luanrzh.xin](http://dy.luanrzh.xin)或者[http://47.94.108.58:9000](http://47.94.108.58:9000)查看结果。