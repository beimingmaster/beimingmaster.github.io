---
title: thrift生成的java源码，vscode无法识别
---

使用Maven Thrift Plugin生成的java源代码，IDEA可以正常识别，但VSCode无法识别。
后来在网上搜索了一下，发现其他人也有类似问题，需要在POM文件增加另外的Plugin：build-helper-maven-plugin解决； 

### 在POM文件增加Plugin代码

``` pom.xml
<plugin>
					<!-- a hint for IDE's to add the java sources to the classpath -->
					<groupId>org.codehaus.mojo</groupId>
					<artifactId>build-helper-maven-plugin</artifactId>
					<version>3.4.0</version>
					<executions>
					<execution>
						<?m2e execute onConfiguration,onIncremental?>
						<id>add-source</id>
						<phase>generate-sources</phase>
						<goals>
						<goal>add-source</goal>
						</goals>
						<configuration>
						<sources>
							<source>${project.build.directory}/generated-sources/thrift</source>
						</sources>
						</configuration>
					</execution>
					</executions>
				</plugin>
```

刷新VSCode，不能识别的源代码正常了。
