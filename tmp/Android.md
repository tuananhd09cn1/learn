- tunnel
- Key MAP
  + https://www.catalysts.cc/en/wissenswertes/intellij-idea-and-eclipse-shortcuts/
- OkHttp Android
- Retrofit Android
files>
		<profile>
			<id>winsw</id>
			<build>
				<finalName>${project.name}</finalName>
				<plugins>
					<plugin>
						<groupId>org.apache.maven.plugins</groupId>
						<artifactId>maven-assembly-plugin</artifactId>
						<version>3.0.0</version>
						<configuration>
							<descriptors>
								<descriptor>${project.basedir}/src/assembly/service-assembly.xml</descriptor>
							</descriptors>
						</configuration>
						<executions>
							<execution>
								<id>service-assembly</id>
								<phase>package</phase>
								<goals>
									<goal>single</goal>
								</goals>
							</execution>
						</executions>
					</plugin>
				</plugins>
			</build>
		</profile>
		
		<profile>
			<id>installer</id>
			<build>
				<finalName>${project.name}</finalName>
				<plugins>
					<plugin>
						<groupId>org.springframework.boot</groupId>
						<artifactId>spring-boot-maven-plugin</artifactId>
		                <configuration>
		                    <excludes>
		                        <exclude>
		                            <groupId>org.springframework.boot</groupId>
		                            <artifactId>spring-boot-loader</artifactId>
		                        </exclude>
		                    </excludes>
		                </configuration>
					</plugin>
					<plugin>
		                <groupId>org.apache.maven.plugins</groupId>
		                <artifactId>maven-antrun-plugin</artifactId>
		                <version>1.7</version>
		                <executions>
		                    <execution>
		                        <id>default-cli</id>
		                     
		                        <configuration>
		                            <target>
		                                <copy todir="${installer.dir}/jre1.8.0_91">
		                                    <fileset dir="${project.basedir}/src/installer/jre1.8.0_71" />
		                                </copy>
		                                <copy todir="${installer.dir}/commons-daemon">
		                                    <fileset dir="${project.basedir}/src/installer/commons-daemon" />
		                                </copy>
		                                <copy file="${project.build.directory}/Ems.jar" todir="${installer.dir}" />
		                                <copy file="${project.basedir}/src/installer/install.bat" todir="${installer.dir}" />
		                                <copy file="${project.basedir}/src/installer/uninstall.bat" todir="${installer.dir}" />
		                                <zip destfile="${project.build.directory}/${project.build.finalName}.jar" update="true" compress="store">
											<fileset dir="${project.build.directory}/classes" includes="com/samsung/svmc/mms/ems/Bootstrap.class"/>
										</zip>
		                            </target>
		                        </configuration>
		                        <goals>
									<goal>run</goal>
								</goals>
		                    </execution>
		                </executions>
		            </plugin>
		            
				</plugins>
			</build>
		</profile>
    https://github.com/francesc79/test-procrun
