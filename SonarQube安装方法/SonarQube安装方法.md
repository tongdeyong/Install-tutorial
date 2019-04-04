# SonarQube安装方法

### 一、配置要求
	1. 安装jDK8
	2. 运行内存RAM >= 2G
	3. PostgreSQL >=9.3 或者 MySql = 5.6或5.7 必须配置为UTF-8字符集

 更多细节参阅：[https://docs.sonarqube.org/latest/requirements/requirements/](https://docs.sonarqube.org/latest/requirements/requirements/)

### 二、配置数据库

	这里已mysql数据库为例，在库中新建库，配置字符集为UTF-8，如：
	库名：sonar
	密码：sonar
	注意：
	1. 账号需要有对表格增删改查的权限，特别使用工具建表的时候要注意检查权限，不然会报被一个服务器拒绝等错误
	2. 不建库也可以直接使用，它默认使用自带的H2数据库，但不能安装插件

### 三、配置参数

	1. 在conf目录下找到sonar.properties文件，并用编辑器打开;
	2. 直接搜索：sonar.jdbc.username和sonar.jdbc.password，去掉前面的“#”，填上库名和密码
	3. 直接搜索：sonar.jdbc.url，去掉前面的“#”，修改数据库的IP和端口号，若要使用其他的库则选择其他URL即可
	4. （可选）sonarQube的IP和端口号默认为localhost:9000，若要修改，则直接搜索sonar.web.host和sonar.web.port进行修改
	5. （可选）若是个人用，建议减小一下内存配置，直接搜索sonar.web.javaOpts、sonar.ce.javaOpts和sonar.search.javaOpts，最小可设置为128M
		sonar.web.javaOpts=-Xmx128m -Xms128m -XX:+HeapDumpOnOutOfMemoryError
		sonar.ce.javaOpts=-Xmx128m -Xms128m -XX:+HeapDumpOnOutOfMemoryError
		sonar.search.javaOpts=-Xms128m -Xmx128m -XX:+HeapDumpOnOutOfMemoryError
		
### 四、启动服务

	1. 在bin目录下，选择对应系统的文件夹
	2. window系统下，点击sonar.bat即可启动服务
	3. 若要设为服务则用“管理员身份”依次运行InstallNTService.bat、StartNTService.bat即可
	4. 在浏览器输入localhost:9000(默认)即可进入到sonar主页，初始登录账号密码为admin
安装服务过程可参阅官网文档：[https://docs.sonarqube.org/latest/setup/install-server/](https://docs.sonarqube.org/latest/setup/install-server/)
