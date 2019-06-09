## CI/CD using Google Cloud Platform



![image](https://user-images.githubusercontent.com/33985509/59151479-25493d00-8a34-11e9-9cff-90a50130124c.png)






# Create a vm instance in Google cloud account and create external ip 



![image](https://user-images.githubusercontent.com/33985509/59151716-5af02500-8a38-11e9-8210-1edfa9209c38.png)



# Create a firewall port for each application



![image](https://user-images.githubusercontent.com/33985509/59151728-9a1e7600-8a38-11e9-9aca-803ce4c15b6e.png)



# Create a specific port for jira application to run



![image](https://user-images.githubusercontent.com/33985509/59151745-db168a80-8a38-11e9-9d22-ff02006b9b2f.png)



# SSH


![image](https://user-images.githubusercontent.com/33985509/59151763-27fa6100-8a39-11e9-91df-36d99394965c.png)



# Docker  Jira #


docker pull cptactionhank/atlassian-jira   ( pulling image from docker hub )


[root@dockerdemo ~]# docker images
REPOSITORY                     TAG                 IMAGE ID            CREATED             SIZE
cptactionhank/atlassian-jira   latest              4c56f19283ae        4 days ago          507MB



docker run --detach --publish 8080:8081 cptactionhank/atlassian-jira:latest     ( running the image)

Go to GCP firewall rules and specify  tcp - 8081

http//:35.237.64.4:8081


Jira Core

Server ID - BGIX-SJ2L-FSB3-MZA5

Li35.237.64.4

email - manishalankala1@gmail.com
username - manishalankala1
Password - Welcome@1234

Url: http://35.237.64.4:8081/secure/WelcomeToJIRA.jspa




![image](https://user-images.githubusercontent.com/33985509/59152112-15365b00-8a3e-11e9-9806-dea47514d5ee.png)



Name : AIR
Key : AIR
Project management


Create two tasks



# Integrate jira with git


Go to manage apps in jira 



Click on free



Pop up on new Evaluation license & click on generate license
Apply license

we can see Your trial is expiring on 30/Jun/19. Buy a license for this app.



![image](https://user-images.githubusercontent.com/33985509/59152168-2fbd0400-8a3f-11e9-9bdc-772ed76dd758.png)




# Git integration for JIRA



Go to applications tab on in administration


click on Git repositories tab and click on connect to git repository


![image](https://user-images.githubusercontent.com/33985509/59152190-9fcb8a00-8a3f-11e9-9d13-cb7355f85bce.png)


Go to git hub and change your pom.xml file and scroll below

https://github.com/manishalankala/helloworld-java-maven/blob/master/pom.xml



Commit changes fix for AIR-1(which is key of the task created )



open the task in dashboard you can see on the tab git commits(reindexing takes a bit moment)



Go to Git repositories tab in application in administration click on actions and reindex(if you find reindexing is slow this for manual process)





# Docker sonarqube   (Setting Up sonarqube)

sonar src code - 
sonar runner or scanner - 2.6.1

docker pull sonarqube

docker run -d --name sonarqube -p 8082:9000 sonarqube

#(docker run -d --name sonarqube -p 9000:9000 sonarqube -p 9092:9092 sonarqube)#

http://35.237.64.4:8082/about

Login sonarqube

username - admin
password - admin


![image](https://user-images.githubusercontent.com/33985509/59152150-b58c7f80-8a3e-11e9-8ae7-f6bafd5d1c01.png)



https://github.com/manishalankala/java-sonar-runner-simple


took src folder copied to my ops folder remaining files deleted


go to cmd 


L:\ops\sonarsrc


then


L:\ops\sonar-scanner-cli-3.3.0.1492-windows\sonar-scanner-3.3.0.1492-windows\bin\sonar-scanner.bat


Its need to tell the scanner to know its path in conf folder (sonar-scanner-properties)


L:\ops\sonarsrc contains (sonar-project.properties)



![image](https://user-images.githubusercontent.com/33985509/59152360-98f24680-8a42-11e9-8cd9-b9f01a226ffa.png)





# Docker nexus (Setting up Nexus)

ocker pull sonatype/nexus

docker run -d -p 8083:8081 --name nexus sonatype/nexus:oss

![image](https://user-images.githubusercontent.com/33985509/59152239-63e4f480-8a40-11e9-9656-68dc857880d9.png)



http://35.237.64.4:8083/nexus/

Credentials
admin / admin123


![image](https://user-images.githubusercontent.com/33985509/59152258-c4743180-8a40-11e9-91de-ac6a3446776c.png)



# Imprtant nexus modification on the below files



pom.xml 
settings.xml 



provide the url in pom.xml after the creating the repository in nexus



java install on jdk-8u92-linux-x64.tar.gz



mv jdk1.8.0_92 jdk1.8




export JAVA_HOME="/opt/jdk1.8
export PATH=$JAVA_HOME/bin:$PATH



Two things we need to change pom.xml and settings.xml




Created two repositories Release and snapshot in nexus and add in pom.xml after download from https://github.com/manishalankala/helloworld-java-maven




http://35.237.64.4:8083/nexus/content/repositories/airsnapshot/
http://35.237.64.4:8083/nexus/content/repositories/apache-snapshots/





In settings.xml under C:\Tools\apache-maven-3.6.1\conf

<server>
      <id>deployment</id>
      <username>admin</username>
      <password>admin123</password>
    </server>
    





changing the Id to deploymentRepo from sym in pom.xml

<repository>
        <id>deployment</id>
        <name>release softx</name>
        <url>http://35.237.64.4:8083/nexus/content/repositories/airrelease/</url>
    </repository>
    <snapshotRepository>
        <id>deployment</id>
        <name>snapshot softx</name>
        <url>http://35.237.64.4:8083/nexus/content/repositories/airsnapshot/</url>
    </snapshotRepository>
</distributionManagement>





![image](https://user-images.githubusercontent.com/33985509/59152295-482e1e00-8a41-11e9-87fa-17fbaa63366c.png)





Go to secruity tab and click on users and right click on deployment --- set password  = repopwd repopwd





go to cmd and go to the specified path (L:\ops\tonexus) and type mvn deploy



mvn release:clean release:prepare



Error :Missing required setting: scm connection or developerConnection must be specified.




Go to secruity tab and click on users and right click on deployment --- set password  = repopwd repopwd



L:\ops\tonexus>mvn deploy -X



After mvn deploy -X in Windows cmd



Below the execution results



L:\ops\tonexus>mvn deploy -X
Apache Maven 3.6.1 (d66c9c0b3152b2e69ee9bac180bb8fcc8e6af555; 2019-04-04T21:00:29+02:00)
Maven home: C:\Tools\apache-maven-3.6.1\bin\..
Java version: 1.8.0_212, vendor: AdoptOpenJDK, runtime: C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre
Default locale: en_US, platform encoding: Cp1252
OS name: "windows 10", version: "10.0", arch: "amd64", family: "windows"
[DEBUG] Created new class realm maven.api
[DEBUG] Importing foreign packages into class realm maven.api
[DEBUG]   Imported: javax.annotation.* < plexus.core
[DEBUG]   Imported: javax.annotation.security.* < plexus.core
[DEBUG]   Imported: javax.enterprise.inject.* < plexus.core
[DEBUG]   Imported: javax.enterprise.util.* < plexus.core
[DEBUG]   Imported: javax.inject.* < plexus.core
[DEBUG]   Imported: org.apache.maven.* < plexus.core
[DEBUG]   Imported: org.apache.maven.artifact < plexus.core
[DEBUG]   Imported: org.apache.maven.classrealm < plexus.core
[DEBUG]   Imported: org.apache.maven.cli < plexus.core
[DEBUG]   Imported: org.apache.maven.configuration < plexus.core
[DEBUG]   Imported: org.apache.maven.exception < plexus.core
[DEBUG]   Imported: org.apache.maven.execution < plexus.core
[DEBUG]   Imported: org.apache.maven.execution.scope < plexus.core
[DEBUG]   Imported: org.apache.maven.lifecycle < plexus.core
[DEBUG]   Imported: org.apache.maven.model < plexus.core
[DEBUG]   Imported: org.apache.maven.monitor < plexus.core
[DEBUG]   Imported: org.apache.maven.plugin < plexus.core
[DEBUG]   Imported: org.apache.maven.profiles < plexus.core
[DEBUG]   Imported: org.apache.maven.project < plexus.core
[DEBUG]   Imported: org.apache.maven.reporting < plexus.core
[DEBUG]   Imported: org.apache.maven.repository < plexus.core
[DEBUG]   Imported: org.apache.maven.rtinfo < plexus.core
[DEBUG]   Imported: org.apache.maven.settings < plexus.core
[DEBUG]   Imported: org.apache.maven.toolchain < plexus.core
[DEBUG]   Imported: org.apache.maven.usability < plexus.core
[DEBUG]   Imported: org.apache.maven.wagon.* < plexus.core
[DEBUG]   Imported: org.apache.maven.wagon.authentication < plexus.core
[DEBUG]   Imported: org.apache.maven.wagon.authorization < plexus.core
[DEBUG]   Imported: org.apache.maven.wagon.events < plexus.core
[DEBUG]   Imported: org.apache.maven.wagon.observers < plexus.core
[DEBUG]   Imported: org.apache.maven.wagon.proxy < plexus.core
[DEBUG]   Imported: org.apache.maven.wagon.repository < plexus.core
[DEBUG]   Imported: org.apache.maven.wagon.resource < plexus.core
[DEBUG]   Imported: org.codehaus.classworlds < plexus.core
[DEBUG]   Imported: org.codehaus.plexus.* < plexus.core
[DEBUG]   Imported: org.codehaus.plexus.classworlds < plexus.core
[DEBUG]   Imported: org.codehaus.plexus.component < plexus.core
[DEBUG]   Imported: org.codehaus.plexus.configuration < plexus.core
[DEBUG]   Imported: org.codehaus.plexus.container < plexus.core
[DEBUG]   Imported: org.codehaus.plexus.context < plexus.core
[DEBUG]   Imported: org.codehaus.plexus.lifecycle < plexus.core
[DEBUG]   Imported: org.codehaus.plexus.logging < plexus.core
[DEBUG]   Imported: org.codehaus.plexus.personality < plexus.core
[DEBUG]   Imported: org.codehaus.plexus.util.xml.Xpp3Dom < plexus.core
[DEBUG]   Imported: org.codehaus.plexus.util.xml.pull.XmlPullParser < plexus.core
[DEBUG]   Imported: org.codehaus.plexus.util.xml.pull.XmlPullParserException < plexus.core
[DEBUG]   Imported: org.codehaus.plexus.util.xml.pull.XmlSerializer < plexus.core
[DEBUG]   Imported: org.eclipse.aether.* < plexus.core
[DEBUG]   Imported: org.eclipse.aether.artifact < plexus.core
[DEBUG]   Imported: org.eclipse.aether.collection < plexus.core
[DEBUG]   Imported: org.eclipse.aether.deployment < plexus.core
[DEBUG]   Imported: org.eclipse.aether.graph < plexus.core
[DEBUG]   Imported: org.eclipse.aether.impl < plexus.core
[DEBUG]   Imported: org.eclipse.aether.installation < plexus.core
[DEBUG]   Imported: org.eclipse.aether.internal.impl < plexus.core
[DEBUG]   Imported: org.eclipse.aether.metadata < plexus.core
[DEBUG]   Imported: org.eclipse.aether.repository < plexus.core
[DEBUG]   Imported: org.eclipse.aether.resolution < plexus.core
[DEBUG]   Imported: org.eclipse.aether.spi < plexus.core
[DEBUG]   Imported: org.eclipse.aether.transfer < plexus.core
[DEBUG]   Imported: org.eclipse.aether.version < plexus.core
[DEBUG]   Imported: org.fusesource.jansi.* < plexus.core
[DEBUG]   Imported: org.slf4j.* < plexus.core
[DEBUG]   Imported: org.slf4j.event.* < plexus.core
[DEBUG]   Imported: org.slf4j.helpers.* < plexus.core
[DEBUG]   Imported: org.slf4j.spi.* < plexus.core
[DEBUG] Populating class realm maven.api
[INFO] Error stacktraces are turned on.
[DEBUG] Message scheme: color
[DEBUG] Message styles: debug info warning error success failure strong mojo project
[DEBUG] Reading global settings from C:\Tools\apache-maven-3.6.1\bin\..\conf\settings.xml
[DEBUG] Reading user settings from C:\Users\chintu\.m2\settings.xml
[DEBUG] Reading global toolchains from C:\Tools\apache-maven-3.6.1\bin\..\conf\toolchains.xml
[DEBUG] Reading user toolchains from C:\Users\chintu\.m2\toolchains.xml
[DEBUG] Using local repository at C:\Users\chintu\.m2\repository
[DEBUG] Using manager EnhancedLocalRepositoryManager with priority 10.0 for C:\Users\chintu\.m2\repository
[INFO] Scanning for projects...
[DEBUG] Extension realms for project com.scmgalaxy.mavensample:yoodle:jar:5.0.0: (none)
[DEBUG] Looking up lifecycle mappings for packaging jar from ClassRealm[plexus.core, parent: null]
[WARNING]
[WARNING] Some problems were encountered while building the effective model for com.scmgalaxy.mavensample:yoodle:jar:5.0.0
[WARNING] 'build.plugins.plugin.version' for org.apache.maven.plugins:maven-javadoc-plugin is missing. @ line 26, column 11
[WARNING]
[WARNING] It is highly recommended to fix these problems because they threaten the stability of your build.
[WARNING]
[WARNING] For this reason, future Maven versions might no longer support building such malformed projects.
[WARNING]
[DEBUG] === REACTOR BUILD PLAN ================================================
[DEBUG] Project: com.scmgalaxy.mavensample:yoodle:jar:5.0.0
[DEBUG] Tasks:   [deploy]
[DEBUG] Style:   Regular
[DEBUG] =======================================================================
[INFO]
[INFO] ------------------< com.scmgalaxy.mavensample:yoodle >------------------
[INFO] Building my-maven 5.0.0
[INFO] --------------------------------[ jar ]---------------------------------
[DEBUG] Could not find metadata org.apache.maven.plugins:maven-javadoc-plugin/maven-metadata.xml in local (C:\Users\chintu\.m2\repository)
[DEBUG] Skipped remote request for org.apache.maven.plugins:maven-javadoc-plugin/maven-metadata.xml, locally cached metadata up-to-date.
[DEBUG] Resolved plugin version for org.apache.maven.plugins:maven-javadoc-plugin to 3.1.0 from repository central (https://repo.maven.apache.org/maven2, default, releases)
[DEBUG] Lifecycle default -> [validate, initialize, generate-sources, process-sources, generate-resources, process-resources, compile, process-classes, generate-test-sources, process-test-sources, generate-test-resources, process-test-resources, test-compile, process-test-classes, test, prepare-package, package, pre-integration-test, integration-test, post-integration-test, verify, install, deploy]
[DEBUG] Lifecycle clean -> [pre-clean, clean, post-clean]
[DEBUG] Lifecycle site -> [pre-site, site, post-site, site-deploy]
[DEBUG] Lifecycle default -> [validate, initialize, generate-sources, process-sources, generate-resources, process-resources, compile, process-classes, generate-test-sources, process-test-sources, generate-test-resources, process-test-resources, test-compile, process-test-classes, test, prepare-package, package, pre-integration-test, integration-test, post-integration-test, verify, install, deploy]
[DEBUG] Lifecycle clean -> [pre-clean, clean, post-clean]
[DEBUG] Lifecycle site -> [pre-site, site, post-site, site-deploy]
[DEBUG] Lifecycle default -> [validate, initialize, generate-sources, process-sources, generate-resources, process-resources, compile, process-classes, generate-test-sources, process-test-sources, generate-test-resources, process-test-resources, test-compile, process-test-classes, test, prepare-package, package, pre-integration-test, integration-test, post-integration-test, verify, install, deploy]
[DEBUG] Lifecycle clean -> [pre-clean, clean, post-clean]
[DEBUG] Lifecycle site -> [pre-site, site, post-site, site-deploy]
[DEBUG] Lifecycle default -> [validate, initialize, generate-sources, process-sources, generate-resources, process-resources, compile, process-classes, generate-test-sources, process-test-sources, generate-test-resources, process-test-resources, test-compile, process-test-classes, test, prepare-package, package, pre-integration-test, integration-test, post-integration-test, verify, install, deploy]
[DEBUG] Lifecycle clean -> [pre-clean, clean, post-clean]
[DEBUG] Lifecycle site -> [pre-site, site, post-site, site-deploy]
[DEBUG] Lifecycle default -> [validate, initialize, generate-sources, process-sources, generate-resources, process-resources, compile, process-classes, generate-test-sources, process-test-sources, generate-test-resources, process-test-resources, test-compile, process-test-classes, test, prepare-package, package, pre-integration-test, integration-test, post-integration-test, verify, install, deploy]
[DEBUG] Lifecycle clean -> [pre-clean, clean, post-clean]
[DEBUG] Lifecycle site -> [pre-site, site, post-site, site-deploy]
[DEBUG] Lifecycle default -> [validate, initialize, generate-sources, process-sources, generate-resources, process-resources, compile, process-classes, generate-test-sources, process-test-sources, generate-test-resources, process-test-resources, test-compile, process-test-classes, test, prepare-package, package, pre-integration-test, integration-test, post-integration-test, verify, install, deploy]
[DEBUG] Lifecycle clean -> [pre-clean, clean, post-clean]
[DEBUG] Lifecycle site -> [pre-site, site, post-site, site-deploy]
[DEBUG] Lifecycle default -> [validate, initialize, generate-sources, process-sources, generate-resources, process-resources, compile, process-classes, generate-test-sources, process-test-sources, generate-test-resources, process-test-resources, test-compile, process-test-classes, test, prepare-package, package, pre-integration-test, integration-test, post-integration-test, verify, install, deploy]
[DEBUG] Lifecycle clean -> [pre-clean, clean, post-clean]
[DEBUG] Lifecycle site -> [pre-site, site, post-site, site-deploy]
[DEBUG] Lifecycle default -> [validate, initialize, generate-sources, process-sources, generate-resources, process-resources, compile, process-classes, generate-test-sources, process-test-sources, generate-test-resources, process-test-resources, test-compile, process-test-classes, test, prepare-package, package, pre-integration-test, integration-test, post-integration-test, verify, install, deploy]
[DEBUG] Lifecycle clean -> [pre-clean, clean, post-clean]
[DEBUG] Lifecycle site -> [pre-site, site, post-site, site-deploy]
[DEBUG] Lifecycle default -> [validate, initialize, generate-sources, process-sources, generate-resources, process-resources, compile, process-classes, generate-test-sources, process-test-sources, generate-test-resources, process-test-resources, test-compile, process-test-classes, test, prepare-package, package, pre-integration-test, integration-test, post-integration-test, verify, install, deploy]
[DEBUG] Lifecycle clean -> [pre-clean, clean, post-clean]
[DEBUG] Lifecycle site -> [pre-site, site, post-site, site-deploy]
[DEBUG] === PROJECT BUILD PLAN ================================================
[DEBUG] Project:       com.scmgalaxy.mavensample:yoodle:5.0.0
[DEBUG] Dependencies (collect): []
[DEBUG] Dependencies (resolve): [compile, runtime, test]
[DEBUG] Repositories (dependencies): [central (https://repo.maven.apache.org/maven2, default, releases)]
[DEBUG] Repositories (plugins)     : [central (https://repo.maven.apache.org/maven2, default, releases)]
[DEBUG] -----------------------------------------------------------------------
[DEBUG] Goal:          org.apache.maven.plugins:maven-resources-plugin:2.6:resources (default-resources)
[DEBUG] Style:         Regular
[DEBUG] Configuration: <?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <buildFilters default-value="${project.build.filters}"/>
  <encoding default-value="${project.build.sourceEncoding}">${encoding}</encoding>
  <escapeString>${maven.resources.escapeString}</escapeString>
  <escapeWindowsPaths default-value="true">${maven.resources.escapeWindowsPaths}</escapeWindowsPaths>
  <includeEmptyDirs default-value="false">${maven.resources.includeEmptyDirs}</includeEmptyDirs>
  <outputDirectory default-value="${project.build.outputDirectory}"/>
  <overwrite default-value="false">${maven.resources.overwrite}</overwrite>
  <project default-value="${project}"/>
  <resources default-value="${project.resources}"/>
  <session default-value="${session}"/>
  <supportMultiLineFiltering default-value="false">${maven.resources.supportMultiLineFiltering}</supportMultiLineFiltering>
  <useBuildFilters default-value="true"/>
  <useDefaultDelimiters default-value="true"/>
</configuration>
[DEBUG] -----------------------------------------------------------------------
[DEBUG] Goal:          org.apache.maven.plugins:maven-compiler-plugin:3.1:compile (default-compile)
[DEBUG] Style:         Regular
[DEBUG] Configuration: <?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <basedir default-value="${basedir}"/>
  <buildDirectory default-value="${project.build.directory}"/>
  <classpathElements default-value="${project.compileClasspathElements}"/>
  <compileSourceRoots default-value="${project.compileSourceRoots}"/>
  <compilerId default-value="javac">${maven.compiler.compilerId}</compilerId>
  <compilerReuseStrategy default-value="${reuseCreated}">${maven.compiler.compilerReuseStrategy}</compilerReuseStrategy>
  <compilerVersion>${maven.compiler.compilerVersion}</compilerVersion>
  <debug default-value="true">${maven.compiler.debug}</debug>
  <debuglevel>${maven.compiler.debuglevel}</debuglevel>
  <encoding default-value="${project.build.sourceEncoding}">${encoding}</encoding>
  <executable>${maven.compiler.executable}</executable>
  <failOnError default-value="true">${maven.compiler.failOnError}</failOnError>
  <forceJavacCompilerUse default-value="false">${maven.compiler.forceJavacCompilerUse}</forceJavacCompilerUse>
  <fork default-value="false">${maven.compiler.fork}</fork>
  <generatedSourcesDirectory default-value="${project.build.directory}/generated-sources/annotations"/>
  <maxmem>${maven.compiler.maxmem}</maxmem>
  <meminitial>${maven.compiler.meminitial}</meminitial>
  <mojoExecution>${mojoExecution}</mojoExecution>
  <optimize default-value="false">${maven.compiler.optimize}</optimize>
  <outputDirectory default-value="${project.build.outputDirectory}"/>
  <projectArtifact default-value="${project.artifact}"/>
  <showDeprecation default-value="false">${maven.compiler.showDeprecation}</showDeprecation>
  <showWarnings default-value="false">${maven.compiler.showWarnings}</showWarnings>
  <skipMain>${maven.main.skip}</skipMain>
  <skipMultiThreadWarning default-value="false">${maven.compiler.skipMultiThreadWarning}</skipMultiThreadWarning>
  <source default-value="1.5">${maven.compiler.source}</source>
  <staleMillis default-value="0">${lastModGranularityMs}</staleMillis>
  <target default-value="1.5">${maven.compiler.target}</target>
  <useIncrementalCompilation default-value="true">${maven.compiler.useIncrementalCompilation}</useIncrementalCompilation>
  <verbose default-value="false">${maven.compiler.verbose}</verbose>
  <mavenSession default-value="${session}"/>
  <session default-value="${session}"/>
</configuration>
[DEBUG] -----------------------------------------------------------------------
[DEBUG] Goal:          org.apache.maven.plugins:maven-resources-plugin:2.6:testResources (default-testResources)
[DEBUG] Style:         Regular
[DEBUG] Configuration: <?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <buildFilters default-value="${project.build.filters}"/>
  <encoding default-value="${project.build.sourceEncoding}">${encoding}</encoding>
  <escapeString>${maven.resources.escapeString}</escapeString>
  <escapeWindowsPaths default-value="true">${maven.resources.escapeWindowsPaths}</escapeWindowsPaths>
  <includeEmptyDirs default-value="false">${maven.resources.includeEmptyDirs}</includeEmptyDirs>
  <outputDirectory default-value="${project.build.testOutputDirectory}"/>
  <overwrite default-value="false">${maven.resources.overwrite}</overwrite>
  <project default-value="${project}"/>
  <resources default-value="${project.testResources}"/>
  <session default-value="${session}"/>
  <skip>${maven.test.skip}</skip>
  <supportMultiLineFiltering default-value="false">${maven.resources.supportMultiLineFiltering}</supportMultiLineFiltering>
  <useBuildFilters default-value="true"/>
  <useDefaultDelimiters default-value="true"/>
</configuration>
[DEBUG] -----------------------------------------------------------------------
[DEBUG] Goal:          org.apache.maven.plugins:maven-compiler-plugin:3.1:testCompile (default-testCompile)
[DEBUG] Style:         Regular
[DEBUG] Configuration: <?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <basedir default-value="${basedir}"/>
  <buildDirectory default-value="${project.build.directory}"/>
  <classpathElements default-value="${project.testClasspathElements}"/>
  <compileSourceRoots default-value="${project.testCompileSourceRoots}"/>
  <compilerId default-value="javac">${maven.compiler.compilerId}</compilerId>
  <compilerReuseStrategy default-value="${reuseCreated}">${maven.compiler.compilerReuseStrategy}</compilerReuseStrategy>
  <compilerVersion>${maven.compiler.compilerVersion}</compilerVersion>
  <debug default-value="true">${maven.compiler.debug}</debug>
  <debuglevel>${maven.compiler.debuglevel}</debuglevel>
  <encoding default-value="${project.build.sourceEncoding}">${encoding}</encoding>
  <executable>${maven.compiler.executable}</executable>
  <failOnError default-value="true">${maven.compiler.failOnError}</failOnError>
  <forceJavacCompilerUse default-value="false">${maven.compiler.forceJavacCompilerUse}</forceJavacCompilerUse>
  <fork default-value="false">${maven.compiler.fork}</fork>
  <generatedTestSourcesDirectory default-value="${project.build.directory}/generated-test-sources/test-annotations"/>
  <maxmem>${maven.compiler.maxmem}</maxmem>
  <meminitial>${maven.compiler.meminitial}</meminitial>
  <mojoExecution>${mojoExecution}</mojoExecution>
  <optimize default-value="false">${maven.compiler.optimize}</optimize>
  <outputDirectory default-value="${project.build.testOutputDirectory}"/>
  <showDeprecation default-value="false">${maven.compiler.showDeprecation}</showDeprecation>
  <showWarnings default-value="false">${maven.compiler.showWarnings}</showWarnings>
  <skip>${maven.test.skip}</skip>
  <skipMultiThreadWarning default-value="false">${maven.compiler.skipMultiThreadWarning}</skipMultiThreadWarning>
  <source default-value="1.5">${maven.compiler.source}</source>
  <staleMillis default-value="0">${lastModGranularityMs}</staleMillis>
  <target default-value="1.5">${maven.compiler.target}</target>
  <testSource>${maven.compiler.testSource}</testSource>
  <testTarget>${maven.compiler.testTarget}</testTarget>
  <useIncrementalCompilation default-value="true">${maven.compiler.useIncrementalCompilation}</useIncrementalCompilation>
  <verbose default-value="false">${maven.compiler.verbose}</verbose>
  <mavenSession default-value="${session}"/>
  <session default-value="${session}"/>
</configuration>
[DEBUG] -----------------------------------------------------------------------
[DEBUG] Goal:          org.apache.maven.plugins:maven-surefire-plugin:2.12.4:test (default-test)
[DEBUG] Style:         Regular
[DEBUG] Configuration: <?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <argLine>${argLine}</argLine>
  <basedir default-value="${basedir}"/>
  <childDelegation default-value="false">${childDelegation}</childDelegation>
  <classesDirectory default-value="${project.build.outputDirectory}"/>
  <debugForkedProcess>${maven.surefire.debug}</debugForkedProcess>
  <disableXmlReport default-value="false">${disableXmlReport}</disableXmlReport>
  <enableAssertions default-value="true">${enableAssertions}</enableAssertions>
  <excludedGroups>${excludedGroups}</excludedGroups>
  <failIfNoSpecifiedTests>${surefire.failIfNoSpecifiedTests}</failIfNoSpecifiedTests>
  <failIfNoTests>${failIfNoTests}</failIfNoTests>
  <forkMode default-value="once">${forkMode}</forkMode>
  <forkedProcessTimeoutInSeconds>${surefire.timeout}</forkedProcessTimeoutInSeconds>
  <groups>${groups}</groups>
  <junitArtifactName default-value="junit:junit">${junitArtifactName}</junitArtifactName>
  <jvm>${jvm}</jvm>
  <localRepository default-value="${localRepository}"/>
  <objectFactory>${objectFactory}</objectFactory>
  <parallel>${parallel}</parallel>
  <parallelMavenExecution default-value="${session.parallel}"/>
  <perCoreThreadCount default-value="true">${perCoreThreadCount}</perCoreThreadCount>
  <pluginArtifactMap>${plugin.artifactMap}</pluginArtifactMap>
  <pluginDescriptor default-value="${plugin}"/>
  <printSummary default-value="true">${surefire.printSummary}</printSummary>
  <projectArtifactMap>${project.artifactMap}</projectArtifactMap>
  <redirectTestOutputToFile default-value="false">${maven.test.redirectTestOutputToFile}</redirectTestOutputToFile>
  <remoteRepositories default-value="${project.pluginArtifactRepositories}"/>
  <reportFormat default-value="brief">${surefire.reportFormat}</reportFormat>
  <reportNameSuffix default-value="">${surefire.reportNameSuffix}</reportNameSuffix>
  <reportsDirectory default-value="${project.build.directory}/surefire-reports"/>
  <runOrder default-value="filesystem"/>
  <skip default-value="false">${maven.test.skip}</skip>
  <skipExec>${maven.test.skip.exec}</skipExec>
  <skipTests default-value="false">${skipTests}</skipTests>
  <test>${test}</test>
  <testClassesDirectory default-value="${project.build.testOutputDirectory}"/>
  <testFailureIgnore default-value="false">${maven.test.failure.ignore}</testFailureIgnore>
  <testNGArtifactName default-value="org.testng:testng">${testNGArtifactName}</testNGArtifactName>
  <testSourceDirectory default-value="${project.build.testSourceDirectory}"/>
  <threadCount>${threadCount}</threadCount>
  <trimStackTrace default-value="true">${trimStackTrace}</trimStackTrace>
  <useFile default-value="true">${surefire.useFile}</useFile>
  <useManifestOnlyJar default-value="true">${surefire.useManifestOnlyJar}</useManifestOnlyJar>
  <useSystemClassLoader default-value="true">${surefire.useSystemClassLoader}</useSystemClassLoader>
  <useUnlimitedThreads default-value="false">${useUnlimitedThreads}</useUnlimitedThreads>
  <workingDirectory>${basedir}</workingDirectory>
  <project default-value="${project}"/>
  <session default-value="${session}"/>
</configuration>
[DEBUG] -----------------------------------------------------------------------
[DEBUG] Goal:          org.apache.maven.plugins:maven-jar-plugin:2.4:jar (default-jar)
[DEBUG] Style:         Regular
[DEBUG] Configuration: <?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <classesDirectory default-value="${project.build.outputDirectory}"/>
  <defaultManifestFile default-value="${project.build.outputDirectory}/META-INF/MANIFEST.MF"/>
  <finalName default-value="${project.build.finalName}">${jar.finalName}</finalName>
  <forceCreation default-value="false">${jar.forceCreation}</forceCreation>
  <outputDirectory default-value="${project.build.directory}"/>
  <project default-value="${project}"/>
  <session default-value="${session}"/>
  <skipIfEmpty default-value="false">${jar.skipIfEmpty}</skipIfEmpty>
  <useDefaultManifestFile default-value="false">${jar.useDefaultManifestFile}</useDefaultManifestFile>
</configuration>
[DEBUG] -----------------------------------------------------------------------
[DEBUG] Goal:          org.apache.maven.plugins:maven-javadoc-plugin:3.1.0:jar (attach-javadocs)
[DEBUG] Style:         Regular
[DEBUG] Configuration: <?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <additionalJOption>${additionalJOption}</additionalJOption>
  <applyJavadocSecurityFix default-value="true">${maven.javadoc.applyJavadocSecurityFix}</applyJavadocSecurityFix>
  <attach default-value="true">${attach}</attach>
  <author default-value="true">${author}</author>
  <bootclasspath>${bootclasspath}</bootclasspath>
  <bootclasspathArtifacts>${bootclasspathArtifacts}</bootclasspathArtifacts>
  <bottom default-value="Copyright &amp;#169; {inceptionYear}&amp;#x2013;{currentYear} {organizationName}. All rights reserved.">${bottom}</bottom>
  <breakiterator default-value="false">${breakiterator}</breakiterator>
  <charset>${charset}</charset>
  <classifier default-value="javadoc">${maven.javadoc.classifier}</classifier>
  <debug default-value="false">${debug}</debug>
  <defaultManifestFile default-value="${project.build.outputDirectory}/META-INF/MANIFEST.MF"/>
  <destDir>${destDir}</destDir>
  <detectJavaApiLink default-value="true">${detectJavaApiLink}</detectJavaApiLink>
  <detectLinks default-value="false">${detectLinks}</detectLinks>
  <detectOfflineLinks default-value="true">${detectOfflineLinks}</detectOfflineLinks>
  <docencoding default-value="${project.reporting.outputEncoding}">${docencoding}</docencoding>
  <docfilessubdirs default-value="false">${docfilessubdirs}</docfilessubdirs>
  <doclet>${doclet}</doclet>
  <docletArtifact>${docletArtifact}</docletArtifact>
  <docletArtifacts>${docletArtifacts}</docletArtifacts>
  <docletPath>${docletPath}</docletPath>
  <doclint>${doclint}</doclint>
  <doctitle default-value="${project.name} ${project.version} API">${doctitle}</doctitle>
  <encoding default-value="${project.build.sourceEncoding}">${encoding}</encoding>
  <excludePackageNames>${excludePackageNames}</excludePackageNames>
  <excludedocfilessubdir>${excludedocfilessubdir}</excludedocfilessubdir>
  <extdirs>${extdirs}</extdirs>
  <failOnError default-value="true">${maven.javadoc.failOnError}</failOnError>
  <failOnWarnings default-value="false">${maven.javadoc.failOnWarnings}</failOnWarnings>
  <finalName>${project.build.finalName}</finalName>
  <footer>${footer}</footer>
  <header>${header}</header>
  <helpfile>${helpfile}</helpfile>
  <includeDependencySources default-value="false"/>
  <includeTransitiveDependencySources default-value="false"/>
  <isOffline default-value="${settings.offline}"/>
  <jarOutputDirectory>${project.build.directory}</jarOutputDirectory>
  <javaApiLinks>${javaApiLinks}</javaApiLinks>
  <javadocDirectory default-value="${basedir}/src/main/javadoc"/>
  <javadocExecutable>${javadocExecutable}</javadocExecutable>
  <javadocOptionsDir default-value="${project.build.directory}/javadoc-bundle-options"/>
  <javadocVersion>${javadocVersion}</javadocVersion>
  <keywords default-value="false">${keywords}</keywords>
  <links>${links}</links>
  <linksource default-value="false">${linksource}</linksource>
  <localRepository>${localRepository}</localRepository>
  <locale>${locale}</locale>
  <maxmemory>${maxmemory}</maxmemory>
  <minmemory>${minmemory}</minmemory>
  <mojo default-value="${mojoExecution}"/>
  <nocomment default-value="false">${nocomment}</nocomment>
  <nodeprecated default-value="false">${nodeprecated}</nodeprecated>
  <nodeprecatedlist default-value="false">${nodeprecatedlist}</nodeprecatedlist>
  <nohelp default-value="false">${nohelp}</nohelp>
  <noindex default-value="false">${noindex}</noindex>
  <nonavbar default-value="false">${nonavbar}</nonavbar>
  <nooverview default-value="false">${nooverview}</nooverview>
  <noqualifier>${noqualifier}</noqualifier>
  <nosince default-value="false">${nosince}</nosince>
  <notimestamp default-value="false">${notimestamp}</notimestamp>
  <notree default-value="false">${notree}</notree>
  <offlineLinks>${offlineLinks}</offlineLinks>
  <old default-value="false">${old}</old>
  <outputDirectory default-value="${project.build.directory}/apidocs">${destDir}</outputDirectory>
  <overview default-value="${basedir}/src/main/javadoc/overview.html">${overview}</overview>
  <packagesheader>${packagesheader}</packagesheader>
  <project default-value="${project}"/>
  <quiet default-value="false">${quiet}</quiet>
  <reactorProjects>${reactorProjects}</reactorProjects>
  <release default-value="${maven.compiler.release}"/>
  <resourcesArtifacts>${resourcesArtifacts}</resourcesArtifacts>
  <serialwarn default-value="false">${serialwarn}</serialwarn>
  <session default-value="${session}"/>
  <settings default-value="${settings}"/>
  <show default-value="protected">${show}</show>
  <skip default-value="false">${maven.javadoc.skip}</skip>
  <source>${source}</source>
  <sourceDependencyCacheDir default-value="${project.build.directory}/distro-javadoc-sources"/>
  <sourcepath>${sourcepath}</sourcepath>
  <sourcetab>${sourcetab}</sourcetab>
  <splitindex default-value="false">${splitindex}</splitindex>
  <stylesheet default-value="java">${stylesheet}</stylesheet>
  <stylesheetfile>${stylesheetfile}</stylesheetfile>
  <subpackages>${subpackages}</subpackages>
  <taglet>${taglet}</taglet>
  <tagletArtifact>${tagletArtifact}</tagletArtifact>
  <tagletArtifacts>${tagletArtifacts}</tagletArtifacts>
  <tagletpath>${tagletpath}</tagletpath>
  <taglets>${taglets}</taglets>
  <tags>${tags}</tags>
  <top>${top}</top>
  <use default-value="true">${use}</use>
  <useDefaultManifestFile default-value="false"/>
  <useStandardDocletOptions default-value="true">${useStandardDocletOptions}</useStandardDocletOptions>
  <validateLinks default-value="false">${validateLinks}</validateLinks>
  <verbose default-value="false">${verbose}</verbose>
  <version default-value="true">${version}</version>
  <windowtitle default-value="${project.name} ${project.version} API">${windowtitle}</windowtitle>
</configuration>
[DEBUG] -----------------------------------------------------------------------
[DEBUG] Goal:          org.apache.maven.plugins:maven-install-plugin:2.4:install (default-install)
[DEBUG] Style:         Regular
[DEBUG] Configuration: <?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <artifact default-value="${project.artifact}"/>
  <attachedArtifacts default-value="${project.attachedArtifacts}"/>
  <createChecksum default-value="false">${createChecksum}</createChecksum>
  <localRepository>${localRepository}</localRepository>
  <packaging default-value="${project.packaging}"/>
  <pomFile default-value="${project.file}"/>
  <skip default-value="false">${maven.install.skip}</skip>
  <updateReleaseInfo default-value="false">${updateReleaseInfo}</updateReleaseInfo>
</configuration>
[DEBUG] -----------------------------------------------------------------------
[DEBUG] Goal:          org.apache.maven.plugins:maven-deploy-plugin:2.7:deploy (default-deploy)
[DEBUG] Style:         Regular
[DEBUG] Configuration: <?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <altDeploymentRepository>${altDeploymentRepository}</altDeploymentRepository>
  <artifact default-value="${project.artifact}"/>
  <attachedArtifacts default-value="${project.attachedArtifacts}"/>
  <localRepository default-value="${localRepository}"/>
  <offline default-value="${settings.offline}"/>
  <packaging default-value="${project.packaging}"/>
  <pomFile default-value="${project.file}"/>
  <project default-value="${project}"/>
  <retryFailedDeploymentCount default-value="1">${retryFailedDeploymentCount}</retryFailedDeploymentCount>
  <skip default-value="false">${maven.deploy.skip}</skip>
  <updateReleaseInfo default-value="false">${updateReleaseInfo}</updateReleaseInfo>
</configuration>
[DEBUG] =======================================================================
[DEBUG] Dependency collection stats: {ConflictMarker.analyzeTime=506345, ConflictMarker.markTime=315117, ConflictMarker.nodeCount=2, ConflictIdSorter.graphTime=285816, ConflictIdSorter.topsortTime=261654, ConflictIdSorter.conflictIdCount=1, ConflictIdSorter.conflictIdCycleCount=0, ConflictResolver.totalTime=2064964, ConflictResolver.conflictItemCount=1, DefaultDependencyCollector.collectTime=5350298, DefaultDependencyCollector.transformTime=4789977}
[DEBUG] com.scmgalaxy.mavensample:yoodle:jar:5.0.0
[DEBUG]    junit:junit:jar:3.8.1:test
[INFO]
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ yoodle ---
[DEBUG] Dependency collection stats: {ConflictMarker.analyzeTime=283245, ConflictMarker.markTime=99727, ConflictMarker.nodeCount=77, ConflictIdSorter.graphTime=148049, ConflictIdSorter.topsortTime=23132, ConflictIdSorter.conflictIdCount=26, ConflictIdSorter.conflictIdCycleCount=0, ConflictResolver.totalTime=1577639, ConflictResolver.conflictItemCount=74, DefaultDependencyCollector.collectTime=150414432, DefaultDependencyCollector.transformTime=2178057}
[DEBUG] org.apache.maven.plugins:maven-resources-plugin:jar:2.6:
[DEBUG]    org.apache.maven:maven-plugin-api:jar:2.0.6:compile
[DEBUG]    org.apache.maven:maven-project:jar:2.0.6:compile
[DEBUG]       org.apache.maven:maven-profile:jar:2.0.6:compile
[DEBUG]       org.apache.maven:maven-artifact-manager:jar:2.0.6:compile
[DEBUG]       org.apache.maven:maven-plugin-registry:jar:2.0.6:compile
[DEBUG]    org.apache.maven:maven-core:jar:2.0.6:compile
[DEBUG]       org.apache.maven:maven-plugin-parameter-documenter:jar:2.0.6:compile
[DEBUG]       org.apache.maven.reporting:maven-reporting-api:jar:2.0.6:compile
[DEBUG]          org.apache.maven.doxia:doxia-sink-api:jar:1.0-alpha-7:compile
[DEBUG]       org.apache.maven:maven-repository-metadata:jar:2.0.6:compile
[DEBUG]       org.apache.maven:maven-error-diagnostics:jar:2.0.6:compile
[DEBUG]       commons-cli:commons-cli:jar:1.0:compile
[DEBUG]       org.apache.maven:maven-plugin-descriptor:jar:2.0.6:compile
[DEBUG]       org.codehaus.plexus:plexus-interactivity-api:jar:1.0-alpha-4:compile
[DEBUG]       classworlds:classworlds:jar:1.1:compile
[DEBUG]    org.apache.maven:maven-artifact:jar:2.0.6:compile
[DEBUG]    org.apache.maven:maven-settings:jar:2.0.6:compile
[DEBUG]    org.apache.maven:maven-model:jar:2.0.6:compile
[DEBUG]    org.apache.maven:maven-monitor:jar:2.0.6:compile
[DEBUG]    org.codehaus.plexus:plexus-container-default:jar:1.0-alpha-9-stable-1:compile
[DEBUG]       junit:junit:jar:3.8.1:compile
[DEBUG]    org.codehaus.plexus:plexus-utils:jar:2.0.5:compile
[DEBUG]    org.apache.maven.shared:maven-filtering:jar:1.1:compile
[DEBUG]       org.sonatype.plexus:plexus-build-api:jar:0.0.4:compile
[DEBUG]    org.codehaus.plexus:plexus-interpolation:jar:1.13:compile
[DEBUG] Created new class realm plugin>org.apache.maven.plugins:maven-resources-plugin:2.6
[DEBUG] Importing foreign packages into class realm plugin>org.apache.maven.plugins:maven-resources-plugin:2.6
[DEBUG]   Imported:  < maven.api
[DEBUG] Populating class realm plugin>org.apache.maven.plugins:maven-resources-plugin:2.6
[DEBUG]   Included: org.apache.maven.plugins:maven-resources-plugin:jar:2.6
[DEBUG]   Included: org.apache.maven.reporting:maven-reporting-api:jar:2.0.6
[DEBUG]   Included: org.apache.maven.doxia:doxia-sink-api:jar:1.0-alpha-7
[DEBUG]   Included: commons-cli:commons-cli:jar:1.0
[DEBUG]   Included: org.codehaus.plexus:plexus-interactivity-api:jar:1.0-alpha-4
[DEBUG]   Included: junit:junit:jar:3.8.1
[DEBUG]   Included: org.codehaus.plexus:plexus-utils:jar:2.0.5
[DEBUG]   Included: org.apache.maven.shared:maven-filtering:jar:1.1
[DEBUG]   Included: org.sonatype.plexus:plexus-build-api:jar:0.0.4
[DEBUG]   Included: org.codehaus.plexus:plexus-interpolation:jar:1.13
[DEBUG] Configuring mojo org.apache.maven.plugins:maven-resources-plugin:2.6:resources from plugin realm ClassRealm[plugin>org.apache.maven.plugins:maven-resources-plugin:2.6, parent: sun.misc.Launcher$AppClassLoader@7852e922]
[DEBUG] Configuring mojo 'org.apache.maven.plugins:maven-resources-plugin:2.6:resources' with basic configurator -->
[DEBUG]   (f) buildFilters = []
[DEBUG]   (f) encoding = UTF-8
[DEBUG]   (f) escapeWindowsPaths = true
[DEBUG]   (s) includeEmptyDirs = false
[DEBUG]   (s) outputDirectory = L:\ops\tonexus\target\classes
[DEBUG]   (s) overwrite = false
[DEBUG]   (f) project = MavenProject: com.scmgalaxy.mavensample:yoodle:5.0.0 @ L:\ops\tonexus\pom.xml
[DEBUG]   (s) resources = [Resource {targetPath: null, filtering: false, FileSet {directory: L:\ops\tonexus\src\main\resources, PatternSet [includes: {}, excludes: {}]}}]
[DEBUG]   (f) session = org.apache.maven.execution.MavenSession@59aa20b3
[DEBUG]   (f) supportMultiLineFiltering = false
[DEBUG]   (f) useBuildFilters = true
[DEBUG]   (s) useDefaultDelimiters = true
[DEBUG] -- end configuration --
[DEBUG] properties used {java.vendor=AdoptOpenJDK, env.SYSTEMROOT=C:\WINDOWS, env.USERDOMAIN_ROAMINGPROFILE=MANISHALANKALA, sun.java.launcher=SUN_STANDARD, sun.management.compiler=HotSpot 64-Bit Tiered Compilers, env.ONEDRIVE=C:\Users\chintu\OneDrive, env.PROMPT=$P$G, env.WDIR=L:\, os.name=Windows 10, sun.boot.class.path=C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\lib\resources.jar;C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\lib\rt.jar;C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\lib\sunrsasign.jar;C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\lib\jsse.jar;C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\lib\jce.jar;C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\lib\charsets.jar;C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\lib\jfr.jar;C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\classes, env.COMPUTERNAME=MANISHALANKALA, env.ALLUSERSPROFILE=C:\ProgramData, sun.desktop=windows, java.vm.specification.vendor=Oracle Corporation, env.PLATFORMCODE=KV, java.runtime.version=1.8.0_212-b03, env.HOMEPATH=\Users\chintu, project.build.sourceEncoding=UTF-8, user.name=chintu, maven.build.version=Apache Maven 3.6.1 (d66c9c0b3152b2e69ee9bac180bb8fcc8e6af555; 2019-04-04T21:00:29+02:00), env.DRIVERDATA=C:\Windows\System32\Drivers\DriverData, env.ONLINESERVICES=Online Services, env.PATH=C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\bin;C:\Program Files (x86)\Intel\iCLS Client\;C:\Program Files\Intel\iCLS Client\;C:\WINDOWS\system32;C:\WINDOWS;C:\WINDOWS\System32\Wbem;C:\WINDOWS\System32\WindowsPowerShell\v1.0\;C:\Program Files (x86)\Intel\Intel(R) Management Engine Components\DAL;C:\Program Files\Intel\Intel(R) Management Engine Components\DAL;C:\Program Files (x86)\Intel\Intel(R) Management Engine Components\IPT;C:\Program Files\Intel\Intel(R) Management Engine Components\IPT;C:\WINDOWS\System32\OpenSSH\;C:\Program Files\Java\jdk1.8.0_171\bin;C:\Program Files\Java\jdk1.8.0_171\lib;C:\Program Files\Intel\WiFi\bin\;C:\Program Files\Common Files\Intel\WirelessCommon\;C:\Program Files\nodejs\;C:\Users\chintu\AppData\Local\Android\Sdk\platform-tools;C:\Tools\apache-maven-3.6.1\bin;C:\Users\chintu\AppData\Local\Programs\Python\Python37\Scripts\;C:\Users\chintu\AppData\Local\Programs\Python\Python37\;C:\Users\chintu\AppData\Local\Microsoft\WindowsApps;C:\Program Files\JetBrains\PyCharm Community Edition 2019.1.2\bin;C:\Users\chintu\AppData\Local\GitHubDesktop\bin;C:\Program Files\Java\jdk-12.0.1\bin;C:\Program Files\Java\jdk-12.0.1\lib;C:\Program Files\Java\jdk-12.0.1;C:\Users\chintu\AppData\Roaming\npm, user.language=en, env.JVMCONFIG=\.mvn\jvm.config, env.WINDIR=C:\WINDOWS, sun.boot.library.path=C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\bin, classworlds.conf=C:\Tools\apache-maven-3.6.1\bin\..\bin\m2.conf, env.REGIONCODE=NA, java.version=1.8.0_212, env.PROCESSOR_IDENTIFIER=Intel64 Family 6 Model 142 Stepping 10, GenuineIntel, user.timezone=, env.TEMP=C:\Users\chintu\AppData\Local\Temp, sun.arch.data.model=64, env.EXEC_DIR=L:\ops\tonexus, java.endorsed.dirs=C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\lib\endorsed, sun.cpu.isalist=amd64, env.HOMEDRIVE=C:, sun.jnu.encoding=Cp1252, file.encoding.pkg=sun.io, env.SYSTEMDRIVE=C:, file.separator=\, java.specification.name=Java Platform API Specification, maven.conf=C:\Tools\apache-maven-3.6.1\bin\../conf, env.JAVACMD=C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\\bin\java.exe, java.class.version=52.0, user.country=US, java.home=C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre, env.ANDROID_HOME=C:\Users\chintu\AppData\Local\Android\Sdk, env.APPDATA=C:\Users\chintu\AppData\Roaming, env.PUBLIC=C:\Users\Public, java.vm.info=mixed mode, env.OS=Windows_NT, os.version=10.0, path.separator=;, java.vm.version=25.212-b03, user.variant=, env.USERPROFILE=C:\Users\chintu, env.JAVA_HOME=C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\, java.awt.printerjob=sun.awt.windows.WPrinterJob, env.TMP=C:\Users\chintu\AppData\Local\Temp, env.=L:=L:\ops\tonexus, env.PROGRAMFILES=C:\Program Files, sun.io.unicode.encoding=UnicodeLittle, awt.toolkit=sun.awt.windows.WToolkit, sun.stdout.encoding=cp437, user.script=, user.home=C:\Users\chintu, env.COMMONPROGRAMFILES=C:\Program Files\Common Files, env.=EXITCODE=00000001, env.SESSIONNAME=Console, java.specification.vendor=Oracle Corporation, library.jansi.path=C:\Tools\apache-maven-3.6.1\bin\..\lib\jansi-native, java.library.path=C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\bin;C:\WINDOWS\Sun\Java\bin;C:\WINDOWS\system32;C:\WINDOWS;C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\bin;C:\Program Files (x86)\Intel\iCLS Client\;C:\Program Files\Intel\iCLS Client\;C:\WINDOWS\system32;C:\WINDOWS;C:\WINDOWS\System32\Wbem;C:\WINDOWS\System32\WindowsPowerShell\v1.0\;C:\Program Files (x86)\Intel\Intel(R) Management Engine Components\DAL;C:\Program Files\Intel\Intel(R) Management Engine Components\DAL;C:\Program Files (x86)\Intel\Intel(R) Management Engine Components\IPT;C:\Program Files\Intel\Intel(R) Management Engine Components\IPT;C:\WINDOWS\System32\OpenSSH\;C:\Program Files\Java\jdk1.8.0_171\bin;C:\Program Files\Java\jdk1.8.0_171\lib;C:\Program Files\Intel\WiFi\bin\;C:\Program Files\Common Files\Intel\WirelessCommon\;C:\Program Files\nodejs\;C:\Users\chintu\AppData\Local\Android\Sdk\platform-tools;C:\Tools\apache-maven-3.6.1\bin;C:\Users\chintu\AppData\Local\Programs\Python\Python37\Scripts\;C:\Users\chintu\AppData\Local\Programs\Python\Python37\;C:\Users\chintu\AppData\Local\Microsoft\WindowsApps;C:\Program Files\JetBrains\PyCharm Community Edition 2019.1.2\bin;C:\Users\chintu\AppData\Local\GitHubDesktop\bin;C:\Program Files\Java\jdk-12.0.1\bin;C:\Program Files\Java\jdk-12.0.1\lib;C:\Program Files\Java\jdk-12.0.1;C:\Users\chintu\AppData\Roaming\npm;., env.NUMBER_OF_PROCESSORS=8, java.vendor.url=http://java.oracle.com/, env.COMMONPROGRAMFILES(X86)=C:\Program Files (x86)\Common Files, env.PSMODULEPATH=C:\Program Files\WindowsPowerShell\Modules;C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules, env.CLASSWORLDS_LAUNCHER=org.codehaus.plexus.classworlds.launcher.Launcher, env.MAVEN_CMD_LINE_ARGS=deploy -X, java.vm.vendor=, maven.home=C:\Tools\apache-maven-3.6.1\bin\.., java.runtime.name=OpenJDK Runtime Environment, sun.java.command=org.codehaus.plexus.classworlds.launcher.Launcher deploy -X, java.class.path=C:\Tools\apache-maven-3.6.1\bin\..\boot\plexus-classworlds-2.6.0.jar, env.PROGRAMW6432=C:\Program Files, maven.version=3.6.1, env.PROGRAMFILES(X86)=C:\Program Files (x86), java.vm.specification.name=Java Virtual Machine Specification, env.LOGONSERVER=\\MANISHALANKALA, java.vm.specification.version=1.8, env.PROCESSOR_ARCHITECTURE=AMD64, env.COMMONPROGRAMW6432=C:\Program Files\Common Files, sun.cpu.endian=little, sun.os.patch.level=, java.io.tmpdir=C:\Users\chintu\AppData\Local\Temp\, env.PROCESSOR_REVISION=8e0a, java.vendor.url.bug=http://bugreport.sun.com/bugreport/, maven.multiModuleProjectDirectory=L:\ops\tonexus, env.PROGRAMDATA=C:\ProgramData, env.COMSPEC=C:\WINDOWS\system32\cmd.exe, os.arch=amd64, java.awt.graphicsenv=sun.awt.Win32GraphicsEnvironment, java.ext.dirs=C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\lib\ext;C:\WINDOWS\Sun\Java\lib\ext, user.dir=L:\ops\tonexus, env.MAVEN_HOME=C:\Tools\apache-maven-3.6.1\bin\.., env.LOCALAPPDATA=C:\Users\chintu\AppData\Local, env.PYCHARM COMMUNITY EDITION=C:\Program Files\JetBrains\PyCharm Community Edition 2019.1.2\bin;, line.separator=
, env.CLASSWORLDS_JAR="C:\Tools\apache-maven-3.6.1\bin\..\boot\plexus-classworlds-2.6.0.jar", java.vm.name=OpenJDK 64-Bit Server VM, env.PATHEXT=.COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC, env.ERROR_CODE=0, env.USERNAME=chintu, sun.stderr.encoding=cp437, file.encoding=Cp1252, env.USERDOMAIN=MANISHALANKALA, java.specification.version=1.8, env.=C:=C:\Users\chintu, env.PROCESSOR_LEVEL=6, env.MAVEN_PROJECTBASEDIR=L:\ops\tonexus, env.VBOX_MSI_INSTALL_PATH=C:\Program Files\Oracle\VirtualBox\}
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[DEBUG] resource with targetPath null
directory L:\ops\tonexus\src\main\resources
excludes []
includes []
[INFO] skip non existing resourceDirectory L:\ops\tonexus\src\main\resources
[DEBUG] no use filter components
[INFO]
[INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ yoodle ---
[DEBUG] Dependency collection stats: {ConflictMarker.analyzeTime=294554, ConflictMarker.markTime=166041, ConflictMarker.nodeCount=160, ConflictIdSorter.graphTime=108980, ConflictIdSorter.topsortTime=37012, ConflictIdSorter.conflictIdCount=43, ConflictIdSorter.conflictIdCycleCount=0, ConflictResolver.totalTime=1517495, ConflictResolver.conflictItemCount=63, DefaultDependencyCollector.collectTime=242290697, DefaultDependencyCollector.transformTime=2140016}
[DEBUG] org.apache.maven.plugins:maven-compiler-plugin:jar:3.1:
[DEBUG]    org.apache.maven:maven-plugin-api:jar:2.0.9:compile
[DEBUG]    org.apache.maven:maven-artifact:jar:2.0.9:compile
[DEBUG]       org.codehaus.plexus:plexus-utils:jar:1.5.1:compile
[DEBUG]    org.apache.maven:maven-core:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-settings:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-plugin-parameter-documenter:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-profile:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-model:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-repository-metadata:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-error-diagnostics:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-project:jar:2.0.9:compile
[DEBUG]          org.apache.maven:maven-plugin-registry:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-plugin-descriptor:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-artifact-manager:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-monitor:jar:2.0.9:compile
[DEBUG]    org.apache.maven:maven-toolchain:jar:1.0:compile
[DEBUG]    org.apache.maven.shared:maven-shared-utils:jar:0.1:compile
[DEBUG]       com.google.code.findbugs:jsr305:jar:2.0.1:compile
[DEBUG]    org.apache.maven.shared:maven-shared-incremental:jar:1.1:compile
[DEBUG]       org.codehaus.plexus:plexus-component-annotations:jar:1.5.5:compile
[DEBUG]    org.codehaus.plexus:plexus-compiler-api:jar:2.2:compile
[DEBUG]    org.codehaus.plexus:plexus-compiler-manager:jar:2.2:compile
[DEBUG]    org.codehaus.plexus:plexus-compiler-javac:jar:2.2:runtime
[DEBUG]    org.codehaus.plexus:plexus-container-default:jar:1.5.5:compile
[DEBUG]       org.codehaus.plexus:plexus-classworlds:jar:2.2.2:compile
[DEBUG]       org.apache.xbean:xbean-reflect:jar:3.4:compile
[DEBUG]          log4j:log4j:jar:1.2.12:compile
[DEBUG]          commons-logging:commons-logging-api:jar:1.1:compile
[DEBUG]       com.google.collections:google-collections:jar:1.0:compile
[DEBUG]       junit:junit:jar:3.8.2:compile
[DEBUG] Created new class realm plugin>org.apache.maven.plugins:maven-compiler-plugin:3.1
[DEBUG] Importing foreign packages into class realm plugin>org.apache.maven.plugins:maven-compiler-plugin:3.1
[DEBUG]   Imported:  < maven.api
[DEBUG] Populating class realm plugin>org.apache.maven.plugins:maven-compiler-plugin:3.1
[DEBUG]   Included: org.apache.maven.plugins:maven-compiler-plugin:jar:3.1
[DEBUG]   Included: org.codehaus.plexus:plexus-utils:jar:1.5.1
[DEBUG]   Included: org.apache.maven.shared:maven-shared-utils:jar:0.1
[DEBUG]   Included: com.google.code.findbugs:jsr305:jar:2.0.1
[DEBUG]   Included: org.apache.maven.shared:maven-shared-incremental:jar:1.1
[DEBUG]   Included: org.codehaus.plexus:plexus-component-annotations:jar:1.5.5
[DEBUG]   Included: org.codehaus.plexus:plexus-compiler-api:jar:2.2
[DEBUG]   Included: org.codehaus.plexus:plexus-compiler-manager:jar:2.2
[DEBUG]   Included: org.codehaus.plexus:plexus-compiler-javac:jar:2.2
[DEBUG]   Included: org.apache.xbean:xbean-reflect:jar:3.4
[DEBUG]   Included: log4j:log4j:jar:1.2.12
[DEBUG]   Included: commons-logging:commons-logging-api:jar:1.1
[DEBUG]   Included: com.google.collections:google-collections:jar:1.0
[DEBUG]   Included: junit:junit:jar:3.8.2
[DEBUG] Configuring mojo org.apache.maven.plugins:maven-compiler-plugin:3.1:compile from plugin realm ClassRealm[plugin>org.apache.maven.plugins:maven-compiler-plugin:3.1, parent: sun.misc.Launcher$AppClassLoader@7852e922]
[DEBUG] Configuring mojo 'org.apache.maven.plugins:maven-compiler-plugin:3.1:compile' with basic configurator -->
[DEBUG]   (f) basedir = L:\ops\tonexus
[DEBUG]   (f) buildDirectory = L:\ops\tonexus\target
[DEBUG]   (f) classpathElements = [L:\ops\tonexus\target\classes]
[DEBUG]   (f) compileSourceRoots = [L:\ops\tonexus\src\main\java]
[DEBUG]   (f) compilerId = javac
[DEBUG]   (f) debug = true
[DEBUG]   (f) encoding = UTF-8
[DEBUG]   (f) failOnError = true
[DEBUG]   (f) forceJavacCompilerUse = false
[DEBUG]   (f) fork = false
[DEBUG]   (f) generatedSourcesDirectory = L:\ops\tonexus\target\generated-sources\annotations
[DEBUG]   (f) mojoExecution = org.apache.maven.plugins:maven-compiler-plugin:3.1:compile {execution: default-compile}
[DEBUG]   (f) optimize = false
[DEBUG]   (f) outputDirectory = L:\ops\tonexus\target\classes
[DEBUG]   (f) projectArtifact = com.scmgalaxy.mavensample:yoodle:jar:5.0.0
[DEBUG]   (f) showDeprecation = false
[DEBUG]   (f) showWarnings = false
[DEBUG]   (f) skipMultiThreadWarning = false
[DEBUG]   (f) source = 1.5
[DEBUG]   (f) staleMillis = 0
[DEBUG]   (f) target = 1.5
[DEBUG]   (f) useIncrementalCompilation = true
[DEBUG]   (f) verbose = false
[DEBUG]   (f) mavenSession = org.apache.maven.execution.MavenSession@59aa20b3
[DEBUG]   (f) session = org.apache.maven.execution.MavenSession@59aa20b3
[DEBUG] -- end configuration --
[DEBUG] Using compiler 'javac'.
[DEBUG] Source directories: [L:\ops\tonexus\src\main\java]
[DEBUG] Classpath: [L:\ops\tonexus\target\classes]
[DEBUG] Output directory: L:\ops\tonexus\target\classes
[DEBUG] CompilerReuseStrategy: reuseCreated
[DEBUG] useIncrementalCompilation enabled
[INFO] Nothing to compile - all classes are up to date
[INFO]
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ yoodle ---
[DEBUG] Configuring mojo org.apache.maven.plugins:maven-resources-plugin:2.6:testResources from plugin realm ClassRealm[plugin>org.apache.maven.plugins:maven-resources-plugin:2.6, parent: sun.misc.Launcher$AppClassLoader@7852e922]
[DEBUG] Configuring mojo 'org.apache.maven.plugins:maven-resources-plugin:2.6:testResources' with basic configurator -->
[DEBUG]   (f) buildFilters = []
[DEBUG]   (f) encoding = UTF-8
[DEBUG]   (f) escapeWindowsPaths = true
[DEBUG]   (s) includeEmptyDirs = false
[DEBUG]   (s) outputDirectory = L:\ops\tonexus\target\test-classes
[DEBUG]   (s) overwrite = false
[DEBUG]   (f) project = MavenProject: com.scmgalaxy.mavensample:yoodle:5.0.0 @ L:\ops\tonexus\pom.xml
[DEBUG]   (s) resources = [Resource {targetPath: null, filtering: false, FileSet {directory: L:\ops\tonexus\src\test\resources, PatternSet [includes: {}, excludes: {}]}}]
[DEBUG]   (f) session = org.apache.maven.execution.MavenSession@59aa20b3
[DEBUG]   (f) supportMultiLineFiltering = false
[DEBUG]   (f) useBuildFilters = true
[DEBUG]   (s) useDefaultDelimiters = true
[DEBUG] -- end configuration --
[DEBUG] properties used {java.vendor=AdoptOpenJDK, env.SYSTEMROOT=C:\WINDOWS, env.USERDOMAIN_ROAMINGPROFILE=MANISHALANKALA, sun.java.launcher=SUN_STANDARD, sun.management.compiler=HotSpot 64-Bit Tiered Compilers, env.ONEDRIVE=C:\Users\chintu\OneDrive, env.PROMPT=$P$G, env.WDIR=L:\, os.name=Windows 10, sun.boot.class.path=C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\lib\resources.jar;C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\lib\rt.jar;C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\lib\sunrsasign.jar;C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\lib\jsse.jar;C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\lib\jce.jar;C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\lib\charsets.jar;C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\lib\jfr.jar;C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\classes, env.COMPUTERNAME=MANISHALANKALA, env.ALLUSERSPROFILE=C:\ProgramData, sun.desktop=windows, java.vm.specification.vendor=Oracle Corporation, env.PLATFORMCODE=KV, java.runtime.version=1.8.0_212-b03, env.HOMEPATH=\Users\chintu, project.build.sourceEncoding=UTF-8, user.name=chintu, maven.build.version=Apache Maven 3.6.1 (d66c9c0b3152b2e69ee9bac180bb8fcc8e6af555; 2019-04-04T21:00:29+02:00), env.DRIVERDATA=C:\Windows\System32\Drivers\DriverData, env.ONLINESERVICES=Online Services, env.PATH=C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\bin;C:\Program Files (x86)\Intel\iCLS Client\;C:\Program Files\Intel\iCLS Client\;C:\WINDOWS\system32;C:\WINDOWS;C:\WINDOWS\System32\Wbem;C:\WINDOWS\System32\WindowsPowerShell\v1.0\;C:\Program Files (x86)\Intel\Intel(R) Management Engine Components\DAL;C:\Program Files\Intel\Intel(R) Management Engine Components\DAL;C:\Program Files (x86)\Intel\Intel(R) Management Engine Components\IPT;C:\Program Files\Intel\Intel(R) Management Engine Components\IPT;C:\WINDOWS\System32\OpenSSH\;C:\Program Files\Java\jdk1.8.0_171\bin;C:\Program Files\Java\jdk1.8.0_171\lib;C:\Program Files\Intel\WiFi\bin\;C:\Program Files\Common Files\Intel\WirelessCommon\;C:\Program Files\nodejs\;C:\Users\chintu\AppData\Local\Android\Sdk\platform-tools;C:\Tools\apache-maven-3.6.1\bin;C:\Users\chintu\AppData\Local\Programs\Python\Python37\Scripts\;C:\Users\chintu\AppData\Local\Programs\Python\Python37\;C:\Users\chintu\AppData\Local\Microsoft\WindowsApps;C:\Program Files\JetBrains\PyCharm Community Edition 2019.1.2\bin;C:\Users\chintu\AppData\Local\GitHubDesktop\bin;C:\Program Files\Java\jdk-12.0.1\bin;C:\Program Files\Java\jdk-12.0.1\lib;C:\Program Files\Java\jdk-12.0.1;C:\Users\chintu\AppData\Roaming\npm, user.language=en, env.JVMCONFIG=\.mvn\jvm.config, env.WINDIR=C:\WINDOWS, sun.boot.library.path=C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\bin, classworlds.conf=C:\Tools\apache-maven-3.6.1\bin\..\bin\m2.conf, env.REGIONCODE=NA, java.version=1.8.0_212, env.PROCESSOR_IDENTIFIER=Intel64 Family 6 Model 142 Stepping 10, GenuineIntel, user.timezone=, env.TEMP=C:\Users\chintu\AppData\Local\Temp, sun.arch.data.model=64, env.EXEC_DIR=L:\ops\tonexus, java.endorsed.dirs=C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\lib\endorsed, sun.cpu.isalist=amd64, env.HOMEDRIVE=C:, sun.jnu.encoding=Cp1252, file.encoding.pkg=sun.io, env.SYSTEMDRIVE=C:, file.separator=\, java.specification.name=Java Platform API Specification, maven.conf=C:\Tools\apache-maven-3.6.1\bin\../conf, env.JAVACMD=C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\\bin\java.exe, java.class.version=52.0, user.country=US, java.home=C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre, env.ANDROID_HOME=C:\Users\chintu\AppData\Local\Android\Sdk, env.APPDATA=C:\Users\chintu\AppData\Roaming, env.PUBLIC=C:\Users\Public, java.vm.info=mixed mode, env.OS=Windows_NT, os.version=10.0, path.separator=;, java.vm.version=25.212-b03, user.variant=, env.USERPROFILE=C:\Users\chintu, env.JAVA_HOME=C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\, java.awt.printerjob=sun.awt.windows.WPrinterJob, env.TMP=C:\Users\chintu\AppData\Local\Temp, env.=L:=L:\ops\tonexus, env.PROGRAMFILES=C:\Program Files, sun.io.unicode.encoding=UnicodeLittle, awt.toolkit=sun.awt.windows.WToolkit, sun.stdout.encoding=cp437, user.script=, user.home=C:\Users\chintu, env.COMMONPROGRAMFILES=C:\Program Files\Common Files, env.=EXITCODE=00000001, env.SESSIONNAME=Console, java.specification.vendor=Oracle Corporation, library.jansi.path=C:\Tools\apache-maven-3.6.1\bin\..\lib\jansi-native, java.library.path=C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\bin;C:\WINDOWS\Sun\Java\bin;C:\WINDOWS\system32;C:\WINDOWS;C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\bin;C:\Program Files (x86)\Intel\iCLS Client\;C:\Program Files\Intel\iCLS Client\;C:\WINDOWS\system32;C:\WINDOWS;C:\WINDOWS\System32\Wbem;C:\WINDOWS\System32\WindowsPowerShell\v1.0\;C:\Program Files (x86)\Intel\Intel(R) Management Engine Components\DAL;C:\Program Files\Intel\Intel(R) Management Engine Components\DAL;C:\Program Files (x86)\Intel\Intel(R) Management Engine Components\IPT;C:\Program Files\Intel\Intel(R) Management Engine Components\IPT;C:\WINDOWS\System32\OpenSSH\;C:\Program Files\Java\jdk1.8.0_171\bin;C:\Program Files\Java\jdk1.8.0_171\lib;C:\Program Files\Intel\WiFi\bin\;C:\Program Files\Common Files\Intel\WirelessCommon\;C:\Program Files\nodejs\;C:\Users\chintu\AppData\Local\Android\Sdk\platform-tools;C:\Tools\apache-maven-3.6.1\bin;C:\Users\chintu\AppData\Local\Programs\Python\Python37\Scripts\;C:\Users\chintu\AppData\Local\Programs\Python\Python37\;C:\Users\chintu\AppData\Local\Microsoft\WindowsApps;C:\Program Files\JetBrains\PyCharm Community Edition 2019.1.2\bin;C:\Users\chintu\AppData\Local\GitHubDesktop\bin;C:\Program Files\Java\jdk-12.0.1\bin;C:\Program Files\Java\jdk-12.0.1\lib;C:\Program Files\Java\jdk-12.0.1;C:\Users\chintu\AppData\Roaming\npm;., env.NUMBER_OF_PROCESSORS=8, java.vendor.url=http://java.oracle.com/, env.COMMONPROGRAMFILES(X86)=C:\Program Files (x86)\Common Files, env.PSMODULEPATH=C:\Program Files\WindowsPowerShell\Modules;C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules, env.CLASSWORLDS_LAUNCHER=org.codehaus.plexus.classworlds.launcher.Launcher, env.MAVEN_CMD_LINE_ARGS=deploy -X, java.vm.vendor=, maven.home=C:\Tools\apache-maven-3.6.1\bin\.., java.runtime.name=OpenJDK Runtime Environment, sun.java.command=org.codehaus.plexus.classworlds.launcher.Launcher deploy -X, java.class.path=C:\Tools\apache-maven-3.6.1\bin\..\boot\plexus-classworlds-2.6.0.jar, env.PROGRAMW6432=C:\Program Files, maven.version=3.6.1, env.PROGRAMFILES(X86)=C:\Program Files (x86), java.vm.specification.name=Java Virtual Machine Specification, env.LOGONSERVER=\\MANISHALANKALA, java.vm.specification.version=1.8, env.PROCESSOR_ARCHITECTURE=AMD64, env.COMMONPROGRAMW6432=C:\Program Files\Common Files, sun.cpu.endian=little, sun.os.patch.level=, java.io.tmpdir=C:\Users\chintu\AppData\Local\Temp\, env.PROCESSOR_REVISION=8e0a, java.vendor.url.bug=http://bugreport.sun.com/bugreport/, maven.multiModuleProjectDirectory=L:\ops\tonexus, env.PROGRAMDATA=C:\ProgramData, env.COMSPEC=C:\WINDOWS\system32\cmd.exe, os.arch=amd64, java.awt.graphicsenv=sun.awt.Win32GraphicsEnvironment, java.ext.dirs=C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\lib\ext;C:\WINDOWS\Sun\Java\lib\ext, user.dir=L:\ops\tonexus, env.MAVEN_HOME=C:\Tools\apache-maven-3.6.1\bin\.., env.LOCALAPPDATA=C:\Users\chintu\AppData\Local, env.PYCHARM COMMUNITY EDITION=C:\Program Files\JetBrains\PyCharm Community Edition 2019.1.2\bin;, line.separator=
, env.CLASSWORLDS_JAR="C:\Tools\apache-maven-3.6.1\bin\..\boot\plexus-classworlds-2.6.0.jar", java.vm.name=OpenJDK 64-Bit Server VM, env.PATHEXT=.COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC, env.ERROR_CODE=0, env.USERNAME=chintu, sun.stderr.encoding=cp437, file.encoding=Cp1252, env.USERDOMAIN=MANISHALANKALA, java.specification.version=1.8, env.=C:=C:\Users\chintu, env.PROCESSOR_LEVEL=6, env.MAVEN_PROJECTBASEDIR=L:\ops\tonexus, env.VBOX_MSI_INSTALL_PATH=C:\Program Files\Oracle\VirtualBox\}
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[DEBUG] resource with targetPath null
directory L:\ops\tonexus\src\test\resources
excludes []
includes []
[INFO] skip non existing resourceDirectory L:\ops\tonexus\src\test\resources
[DEBUG] no use filter components
[INFO]
[INFO] --- maven-compiler-plugin:3.1:testCompile (default-testCompile) @ yoodle ---
[DEBUG] Configuring mojo org.apache.maven.plugins:maven-compiler-plugin:3.1:testCompile from plugin realm ClassRealm[plugin>org.apache.maven.plugins:maven-compiler-plugin:3.1, parent: sun.misc.Launcher$AppClassLoader@7852e922]
[DEBUG] Configuring mojo 'org.apache.maven.plugins:maven-compiler-plugin:3.1:testCompile' with basic configurator -->
[DEBUG]   (f) basedir = L:\ops\tonexus
[DEBUG]   (f) buildDirectory = L:\ops\tonexus\target
[DEBUG]   (f) classpathElements = [L:\ops\tonexus\target\test-classes, L:\ops\tonexus\target\classes, C:\Users\chintu\.m2\repository\junit\junit\3.8.1\junit-3.8.1.jar]
[DEBUG]   (f) compileSourceRoots = [L:\ops\tonexus\src\test\java]
[DEBUG]   (f) compilerId = javac
[DEBUG]   (f) debug = true
[DEBUG]   (f) encoding = UTF-8
[DEBUG]   (f) failOnError = true
[DEBUG]   (f) forceJavacCompilerUse = false
[DEBUG]   (f) fork = false
[DEBUG]   (f) generatedTestSourcesDirectory = L:\ops\tonexus\target\generated-test-sources\test-annotations
[DEBUG]   (f) mojoExecution = org.apache.maven.plugins:maven-compiler-plugin:3.1:testCompile {execution: default-testCompile}
[DEBUG]   (f) optimize = false
[DEBUG]   (f) outputDirectory = L:\ops\tonexus\target\test-classes
[DEBUG]   (f) showDeprecation = false
[DEBUG]   (f) showWarnings = false
[DEBUG]   (f) skipMultiThreadWarning = false
[DEBUG]   (f) source = 1.5
[DEBUG]   (f) staleMillis = 0
[DEBUG]   (f) target = 1.5
[DEBUG]   (f) useIncrementalCompilation = true
[DEBUG]   (f) verbose = false
[DEBUG]   (f) mavenSession = org.apache.maven.execution.MavenSession@59aa20b3
[DEBUG]   (f) session = org.apache.maven.execution.MavenSession@59aa20b3
[DEBUG] -- end configuration --
[DEBUG] Using compiler 'javac'.
[DEBUG] Source directories: [L:\ops\tonexus\src\test\java]
[DEBUG] Classpath: [L:\ops\tonexus\target\test-classes
 L:\ops\tonexus\target\classes
 C:\Users\chintu\.m2\repository\junit\junit\3.8.1\junit-3.8.1.jar]
[DEBUG] Output directory: L:\ops\tonexus\target\test-classes
[DEBUG] CompilerReuseStrategy: reuseCreated
[DEBUG] useIncrementalCompilation enabled
[INFO] Nothing to compile - all classes are up to date
[INFO]
[INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ yoodle ---
[DEBUG] Dependency collection stats: {ConflictMarker.analyzeTime=375775, ConflictMarker.markTime=98699, ConflictMarker.nodeCount=132, ConflictIdSorter.graphTime=162956, ConflictIdSorter.topsortTime=19020, ConflictIdSorter.conflictIdCount=27, ConflictIdSorter.conflictIdCycleCount=0, ConflictResolver.totalTime=675984, ConflictResolver.conflictItemCount=77, DefaultDependencyCollector.collectTime=54946970, DefaultDependencyCollector.transformTime=1347342}
[DEBUG] org.apache.maven.plugins:maven-surefire-plugin:jar:2.12.4:
[DEBUG]    org.apache.maven:maven-plugin-api:jar:2.0.9:compile
[DEBUG]    org.apache.maven.surefire:surefire-booter:jar:2.12.4:compile
[DEBUG]       org.apache.maven.surefire:surefire-api:jar:2.12.4:compile
[DEBUG]    org.apache.maven.surefire:maven-surefire-common:jar:2.12.4:compile
[DEBUG]       org.apache.commons:commons-lang3:jar:3.1:compile
[DEBUG]       org.apache.maven.shared:maven-common-artifact-filters:jar:1.3:compile
[DEBUG]    org.codehaus.plexus:plexus-utils:jar:3.0.8:compile
[DEBUG]    org.apache.maven:maven-artifact:jar:2.0.9:compile
[DEBUG]    org.apache.maven:maven-project:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-settings:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-profile:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-model:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-artifact-manager:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-plugin-registry:jar:2.0.9:compile
[DEBUG]       org.codehaus.plexus:plexus-container-default:jar:1.0-alpha-9-stable-1:compile
[DEBUG]          junit:junit:jar:3.8.1:test
[DEBUG]    org.apache.maven:maven-core:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-plugin-parameter-documenter:jar:2.0.9:compile
[DEBUG]       org.apache.maven.reporting:maven-reporting-api:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-repository-metadata:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-error-diagnostics:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-plugin-descriptor:jar:2.0.9:compile
[DEBUG]       org.apache.maven:maven-monitor:jar:2.0.9:compile
[DEBUG]       classworlds:classworlds:jar:1.1:compile
[DEBUG]    org.apache.maven:maven-toolchain:jar:2.0.9:compile
[DEBUG]    org.apache.maven.plugin-tools:maven-plugin-annotations:jar:3.1:compile
[DEBUG] Created new class realm plugin>org.apache.maven.plugins:maven-surefire-plugin:2.12.4
[DEBUG] Importing foreign packages into class realm plugin>org.apache.maven.plugins:maven-surefire-plugin:2.12.4
[DEBUG]   Imported:  < maven.api
[DEBUG] Populating class realm plugin>org.apache.maven.plugins:maven-surefire-plugin:2.12.4
[DEBUG]   Included: org.apache.maven.plugins:maven-surefire-plugin:jar:2.12.4
[DEBUG]   Included: org.apache.maven.surefire:surefire-booter:jar:2.12.4
[DEBUG]   Included: org.apache.maven.surefire:surefire-api:jar:2.12.4
[DEBUG]   Included: org.apache.maven.surefire:maven-surefire-common:jar:2.12.4
[DEBUG]   Included: org.apache.commons:commons-lang3:jar:3.1
[DEBUG]   Included: org.apache.maven.shared:maven-common-artifact-filters:jar:1.3
[DEBUG]   Included: org.codehaus.plexus:plexus-utils:jar:3.0.8
[DEBUG]   Included: org.apache.maven.reporting:maven-reporting-api:jar:2.0.9
[DEBUG]   Included: org.apache.maven.plugin-tools:maven-plugin-annotations:jar:3.1
[DEBUG] Configuring mojo org.apache.maven.plugins:maven-surefire-plugin:2.12.4:test from plugin realm ClassRealm[plugin>org.apache.maven.plugins:maven-surefire-plugin:2.12.4, parent: sun.misc.Launcher$AppClassLoader@7852e922]
[DEBUG] Configuring mojo 'org.apache.maven.plugins:maven-surefire-plugin:2.12.4:test' with basic configurator -->
[DEBUG]   (s) basedir = L:\ops\tonexus
[DEBUG]   (s) childDelegation = false
[DEBUG]   (s) classesDirectory = L:\ops\tonexus\target\classes
[DEBUG]   (s) disableXmlReport = false
[DEBUG]   (s) enableAssertions = true
[DEBUG]   (s) forkMode = once
[DEBUG]   (s) junitArtifactName = junit:junit
[DEBUG]   (s) localRepository =       id: local
      url: file:///C:/Users/chintu/.m2/repository/
   layout: default
snapshots: [enabled => true, update => always]
 releases: [enabled => true, update => always]

[DEBUG]   (f) parallelMavenExecution = false
[DEBUG]   (s) perCoreThreadCount = true
[DEBUG]   (s) pluginArtifactMap = {org.apache.maven.plugins:maven-surefire-plugin=org.apache.maven.plugins:maven-surefire-plugin:maven-plugin:2.12.4:, org.apache.maven:maven-plugin-api=org.apache.maven:maven-plugin-api:jar:2.0.9:compile, org.apache.maven.surefire:surefire-booter=org.apache.maven.surefire:surefire-booter:jar:2.12.4:compile, org.apache.maven.surefire:surefire-api=org.apache.maven.surefire:surefire-api:jar:2.12.4:compile, org.apache.maven.surefire:maven-surefire-common=org.apache.maven.surefire:maven-surefire-common:jar:2.12.4:compile, org.apache.commons:commons-lang3=org.apache.commons:commons-lang3:jar:3.1:compile, org.apache.maven.shared:maven-common-artifact-filters=org.apache.maven.shared:maven-common-artifact-filters:jar:1.3:compile, org.codehaus.plexus:plexus-utils=org.codehaus.plexus:plexus-utils:jar:3.0.8:compile, org.apache.maven:maven-artifact=org.apache.maven:maven-artifact:jar:2.0.9:compile, org.apache.maven:maven-project=org.apache.maven:maven-project:jar:2.0.9:compile, org.apache.maven:maven-settings=org.apache.maven:maven-settings:jar:2.0.9:compile, org.apache.maven:maven-profile=org.apache.maven:maven-profile:jar:2.0.9:compile, org.apache.maven:maven-model=org.apache.maven:maven-model:jar:2.0.9:compile, org.apache.maven:maven-artifact-manager=org.apache.maven:maven-artifact-manager:jar:2.0.9:compile, org.apache.maven:maven-plugin-registry=org.apache.maven:maven-plugin-registry:jar:2.0.9:compile, org.codehaus.plexus:plexus-container-default=org.codehaus.plexus:plexus-container-default:jar:1.0-alpha-9-stable-1:compile, org.apache.maven:maven-core=org.apache.maven:maven-core:jar:2.0.9:compile, org.apache.maven:maven-plugin-parameter-documenter=org.apache.maven:maven-plugin-parameter-documenter:jar:2.0.9:compile, org.apache.maven.reporting:maven-reporting-api=org.apache.maven.reporting:maven-reporting-api:jar:2.0.9:compile, org.apache.maven:maven-repository-metadata=org.apache.maven:maven-repository-metadata:jar:2.0.9:compile, org.apache.maven:maven-error-diagnostics=org.apache.maven:maven-error-diagnostics:jar:2.0.9:compile, org.apache.maven:maven-plugin-descriptor=org.apache.maven:maven-plugin-descriptor:jar:2.0.9:compile, org.apache.maven:maven-monitor=org.apache.maven:maven-monitor:jar:2.0.9:compile, classworlds:classworlds=classworlds:classworlds:jar:1.1:compile, org.apache.maven:maven-toolchain=org.apache.maven:maven-toolchain:jar:2.0.9:compile, org.apache.maven.plugin-tools:maven-plugin-annotations=org.apache.maven.plugin-tools:maven-plugin-annotations:jar:3.1:compile}
[DEBUG]   (f) pluginDescriptor = Component Descriptor: role: 'org.apache.maven.plugin.Mojo', implementation: 'org.apache.maven.plugin.surefire.HelpMojo', role hint: 'org.apache.maven.plugins:maven-surefire-plugin:2.12.4:help'
role: 'org.apache.maven.plugin.Mojo', implementation: 'org.apache.maven.plugin.surefire.SurefirePlugin', role hint: 'org.apache.maven.plugins:maven-surefire-plugin:2.12.4:test'
---
[DEBUG]   (s) printSummary = true
[DEBUG]   (s) projectArtifactMap = {junit:junit=junit:junit:jar:3.8.1:test}
[DEBUG]   (s) redirectTestOutputToFile = false
[DEBUG]   (s) remoteRepositories = [      id: central
      url: https://repo.maven.apache.org/maven2
   layout: default
snapshots: [enabled => false, update => daily]
 releases: [enabled => true, update => never]
]
[DEBUG]   (s) reportFormat = brief
[DEBUG]   (s) reportsDirectory = L:\ops\tonexus\target\surefire-reports
[DEBUG]   (s) runOrder = filesystem
[DEBUG]   (s) skip = false
[DEBUG]   (s) skipTests = false
[DEBUG]   (s) testClassesDirectory = L:\ops\tonexus\target\test-classes
[DEBUG]   (s) testFailureIgnore = false
[DEBUG]   (s) testNGArtifactName = org.testng:testng
[DEBUG]   (s) testSourceDirectory = L:\ops\tonexus\src\test\java
[DEBUG]   (s) trimStackTrace = true
[DEBUG]   (s) useFile = true
[DEBUG]   (s) useManifestOnlyJar = true
[DEBUG]   (s) useSystemClassLoader = true
[DEBUG]   (s) useUnlimitedThreads = false
[DEBUG]   (s) workingDirectory = L:\ops\tonexus
[DEBUG]   (s) project = MavenProject: com.scmgalaxy.mavensample:yoodle:5.0.0 @ L:\ops\tonexus\pom.xml
[DEBUG]   (s) session = org.apache.maven.execution.MavenSession@59aa20b3
[DEBUG] -- end configuration --
[INFO] Surefire report directory: L:\ops\tonexus\target\surefire-reports
[DEBUG] Setting system property [user.dir]=[L:\ops\tonexus]
[DEBUG] Setting system property [localRepository]=[C:\Users\chintu\.m2\repository]
[DEBUG] Setting system property [basedir]=[L:\ops\tonexus]
[DEBUG] dummy:dummy:jar:1.0 (selected for null)
[DEBUG]   org.apache.maven.surefire:surefire-booter:jar:2.12.4:compile (selected for compile)
[DEBUG]     org.apache.maven.surefire:surefire-api:jar:2.12.4:compile (selected for compile)
[DEBUG] Adding to surefire booter test classpath: C:\Users\chintu\.m2\repository\org\apache\maven\surefire\surefire-booter\2.12.4\surefire-booter-2.12.4.jar Scope: compile
[DEBUG] Adding to surefire booter test classpath: C:\Users\chintu\.m2\repository\org\apache\maven\surefire\surefire-api\2.12.4\surefire-api-2.12.4.jar Scope: compile
[DEBUG] Using JVM: C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\bin\java
[DEBUG] dummy:dummy:jar:1.0 (selected for null)
[DEBUG]   org.apache.maven.surefire:surefire-junit3:jar:2.12.4:test (selected for test)
[DEBUG]     org.apache.maven.surefire:surefire-api:jar:2.12.4:test (selected for test)
[DEBUG] Adding to surefire test classpath: C:\Users\chintu\.m2\repository\org\apache\maven\surefire\surefire-junit3\2.12.4\surefire-junit3-2.12.4.jar Scope: test
[DEBUG] Adding to surefire test classpath: C:\Users\chintu\.m2\repository\org\apache\maven\surefire\surefire-api\2.12.4\surefire-api-2.12.4.jar Scope: test
[DEBUG] test classpath classpath:
[DEBUG]   L:\ops\tonexus\target\test-classes
[DEBUG]   L:\ops\tonexus\target\classes
[DEBUG]   C:\Users\chintu\.m2\repository\junit\junit\3.8.1\junit-3.8.1.jar
[DEBUG] provider classpath classpath:
[DEBUG]   C:\Users\chintu\.m2\repository\org\apache\maven\surefire\surefire-junit3\2.12.4\surefire-junit3-2.12.4.jar
[DEBUG]   C:\Users\chintu\.m2\repository\org\apache\maven\surefire\surefire-api\2.12.4\surefire-api-2.12.4.jar

-------------------------------------------------------
 T E S T S
-------------------------------------------------------
Forking command line: cmd.exe /X /C ""C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\bin\java" -jar L:\ops\tonexus\target\surefire\surefirebooter7239048830659627179.jar L:\ops\tonexus\target\surefire\surefire7660522688422277484tmp L:\ops\tonexus\target\surefire\surefire_03007084752278015383tmp"
Running com.scmgalaxy.mavensample.AppTest
Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.004 sec

Results :

Tests run: 1, Failures: 0, Errors: 0, Skipped: 0

[INFO]
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ yoodle ---
[DEBUG] Dependency collection stats: {ConflictMarker.analyzeTime=143422, ConflictMarker.markTime=77623, ConflictMarker.nodeCount=74, ConflictIdSorter.graphTime=169638, ConflictIdSorter.topsortTime=33414, ConflictIdSorter.conflictIdCount=28, ConflictIdSorter.conflictIdCycleCount=0, ConflictResolver.totalTime=1046105, ConflictResolver.conflictItemCount=70, DefaultDependencyCollector.collectTime=33407495, DefaultDependencyCollector.transformTime=1501044}
[DEBUG] org.apache.maven.plugins:maven-jar-plugin:jar:2.4:
[DEBUG]    org.apache.maven:maven-plugin-api:jar:2.0.6:compile
[DEBUG]    org.apache.maven:maven-project:jar:2.0.6:compile
[DEBUG]       org.apache.maven:maven-settings:jar:2.0.6:compile
[DEBUG]       org.apache.maven:maven-profile:jar:2.0.6:compile
[DEBUG]       org.apache.maven:maven-artifact-manager:jar:2.0.6:compile
[DEBUG]          org.apache.maven:maven-repository-metadata:jar:2.0.6:compile
[DEBUG]       org.apache.maven:maven-plugin-registry:jar:2.0.6:compile
[DEBUG]       org.codehaus.plexus:plexus-container-default:jar:1.0-alpha-9-stable-1:compile
[DEBUG]          junit:junit:jar:3.8.1:compile
[DEBUG]          classworlds:classworlds:jar:1.1-alpha-2:compile
[DEBUG]    org.apache.maven:maven-model:jar:2.0.6:runtime
[DEBUG]    org.apache.maven:maven-artifact:jar:2.0.6:compile
[DEBUG]    org.apache.maven:maven-archiver:jar:2.5:compile
[DEBUG]       org.apache.maven:maven-core:jar:2.0.6:compile
[DEBUG]          org.apache.maven:maven-plugin-parameter-documenter:jar:2.0.6:compile
[DEBUG]          org.apache.maven.reporting:maven-reporting-api:jar:2.0.6:compile
[DEBUG]             org.apache.maven.doxia:doxia-sink-api:jar:1.0-alpha-7:compile
[DEBUG]          org.apache.maven:maven-error-diagnostics:jar:2.0.6:compile
[DEBUG]          commons-cli:commons-cli:jar:1.0:compile
[DEBUG]          org.apache.maven:maven-plugin-descriptor:jar:2.0.6:compile
[DEBUG]          org.codehaus.plexus:plexus-interactivity-api:jar:1.0-alpha-4:compile
[DEBUG]          org.apache.maven:maven-monitor:jar:2.0.6:compile
[DEBUG]       org.codehaus.plexus:plexus-interpolation:jar:1.15:compile
[DEBUG]    org.codehaus.plexus:plexus-archiver:jar:2.1:compile
[DEBUG]       org.codehaus.plexus:plexus-io:jar:2.0.2:compile
[DEBUG]    commons-lang:commons-lang:jar:2.1:compile
[DEBUG]    org.codehaus.plexus:plexus-utils:jar:3.0:compile
[DEBUG] Created new class realm plugin>org.apache.maven.plugins:maven-jar-plugin:2.4
[DEBUG] Importing foreign packages into class realm plugin>org.apache.maven.plugins:maven-jar-plugin:2.4
[DEBUG]   Imported:  < maven.api
[DEBUG] Populating class realm plugin>org.apache.maven.plugins:maven-jar-plugin:2.4
[DEBUG]   Included: org.apache.maven.plugins:maven-jar-plugin:jar:2.4
[DEBUG]   Included: junit:junit:jar:3.8.1
[DEBUG]   Included: org.apache.maven:maven-archiver:jar:2.5
[DEBUG]   Included: org.apache.maven.reporting:maven-reporting-api:jar:2.0.6
[DEBUG]   Included: org.apache.maven.doxia:doxia-sink-api:jar:1.0-alpha-7
[DEBUG]   Included: commons-cli:commons-cli:jar:1.0
[DEBUG]   Included: org.codehaus.plexus:plexus-interactivity-api:jar:1.0-alpha-4
[DEBUG]   Included: org.codehaus.plexus:plexus-interpolation:jar:1.15
[DEBUG]   Included: org.codehaus.plexus:plexus-archiver:jar:2.1
[DEBUG]   Included: org.codehaus.plexus:plexus-io:jar:2.0.2
[DEBUG]   Included: commons-lang:commons-lang:jar:2.1
[DEBUG]   Included: org.codehaus.plexus:plexus-utils:jar:3.0
[DEBUG] Configuring mojo org.apache.maven.plugins:maven-jar-plugin:2.4:jar from plugin realm ClassRealm[plugin>org.apache.maven.plugins:maven-jar-plugin:2.4, parent: sun.misc.Launcher$AppClassLoader@7852e922]
[DEBUG] Configuring mojo 'org.apache.maven.plugins:maven-jar-plugin:2.4:jar' with basic configurator -->
[DEBUG]   (f) classesDirectory = L:\ops\tonexus\target\classes
[DEBUG]   (f) defaultManifestFile = L:\ops\tonexus\target\classes\META-INF\MANIFEST.MF
[DEBUG]   (f) finalName = yoodle-5.0.0
[DEBUG]   (f) forceCreation = false
[DEBUG]   (f) outputDirectory = L:\ops\tonexus\target
[DEBUG]   (f) project = MavenProject: com.scmgalaxy.mavensample:yoodle:5.0.0 @ L:\ops\tonexus\pom.xml
[DEBUG]   (f) session = org.apache.maven.execution.MavenSession@59aa20b3
[DEBUG]   (f) skipIfEmpty = false
[DEBUG]   (f) useDefaultManifestFile = false
[DEBUG] -- end configuration --
[DEBUG] isUp2date: false (Resource with newer modification date found.)
[INFO] Building jar: L:\ops\tonexus\target\yoodle-5.0.0.jar
[DEBUG] adding directory META-INF/
[DEBUG] adding entry META-INF/MANIFEST.MF
[DEBUG] adding directory com/
[DEBUG] adding directory com/scmgalaxy/
[DEBUG] adding directory com/scmgalaxy/mavensample/
[DEBUG] adding entry com/scmgalaxy/mavensample/App.class
[DEBUG] adding directory META-INF/maven/
[DEBUG] adding directory META-INF/maven/com.scmgalaxy.mavensample/
[DEBUG] adding directory META-INF/maven/com.scmgalaxy.mavensample/yoodle/
[DEBUG] adding entry META-INF/maven/com.scmgalaxy.mavensample/yoodle/pom.xml
[DEBUG] adding entry META-INF/maven/com.scmgalaxy.mavensample/yoodle/pom.properties
[INFO]
[INFO] --- maven-javadoc-plugin:3.1.0:jar (attach-javadocs) @ yoodle ---
[DEBUG] Dependency collection stats: {ConflictMarker.analyzeTime=300209, ConflictMarker.markTime=216418, ConflictMarker.nodeCount=237, ConflictIdSorter.graphTime=128515, ConflictIdSorter.topsortTime=161927, ConflictIdSorter.conflictIdCount=81, ConflictIdSorter.conflictIdCycleCount=0, ConflictResolver.totalTime=4390041, ConflictResolver.conflictItemCount=188, DefaultDependencyCollector.collectTime=496194441, DefaultDependencyCollector.transformTime=5238234}
[DEBUG] org.apache.maven.plugins:maven-javadoc-plugin:jar:3.1.0:
[DEBUG]    org.apache.maven:maven-core:jar:3.0:compile
[DEBUG]       org.apache.maven:maven-settings-builder:jar:3.0:compile
[DEBUG]       org.apache.maven:maven-repository-metadata:jar:3.0:compile
[DEBUG]       org.apache.maven:maven-model-builder:jar:3.0:compile
[DEBUG]       org.apache.maven:maven-aether-provider:jar:3.0:runtime
[DEBUG]       org.sonatype.aether:aether-impl:jar:1.7:compile
[DEBUG]          org.sonatype.aether:aether-spi:jar:1.7:compile
[DEBUG]       org.sonatype.aether:aether-api:jar:1.7:compile
[DEBUG]       org.sonatype.aether:aether-util:jar:1.7:compile
[DEBUG]       org.sonatype.sisu:sisu-inject-plexus:jar:1.4.2:compile
[DEBUG]          org.sonatype.sisu:sisu-inject-bean:jar:1.4.2:compile
[DEBUG]             org.sonatype.sisu:sisu-guice:jar:noaop:2.1.7:compile
[DEBUG]       org.codehaus.plexus:plexus-interpolation:jar:1.14:compile
[DEBUG]       org.codehaus.plexus:plexus-classworlds:jar:2.2.3:compile
[DEBUG]       org.codehaus.plexus:plexus-component-annotations:jar:1.7.1:compile
[DEBUG]       org.sonatype.plexus:plexus-sec-dispatcher:jar:1.3:compile
[DEBUG]          org.sonatype.plexus:plexus-cipher:jar:1.4:compile
[DEBUG]    org.apache.maven:maven-model:jar:3.0:compile
[DEBUG]    org.apache.maven:maven-settings:jar:3.0:compile
[DEBUG]    org.apache.maven:maven-plugin-api:jar:3.0:compile
[DEBUG]    org.apache.maven:maven-artifact:jar:3.0:compile
[DEBUG]    org.apache.maven.reporting:maven-reporting-api:jar:3.0:compile
[DEBUG]    org.apache.maven:maven-archiver:jar:3.2.0:compile
[DEBUG]       org.apache.maven.shared:maven-shared-utils:jar:3.2.0:compile
[DEBUG]    org.apache.maven.shared:maven-invoker:jar:3.0.0:compile
[DEBUG]    org.apache.maven.shared:maven-common-artifact-filters:jar:3.0.0:compile
[DEBUG]    org.apache.maven.shared:maven-artifact-transfer:jar:0.10.1:compile
[DEBUG]       commons-codec:commons-codec:jar:1.11:compile
[DEBUG]       org.slf4j:slf4j-api:jar:1.7.5:compile
[DEBUG]    org.apache.maven.doxia:doxia-sink-api:jar:1.7:compile
[DEBUG]       org.apache.maven.doxia:doxia-logging-api:jar:1.7:compile
[DEBUG]    org.apache.maven.doxia:doxia-site-renderer:jar:1.7.4:compile
[DEBUG]       org.apache.maven.doxia:doxia-core:jar:1.7:compile
[DEBUG]          xmlunit:xmlunit:jar:1.5:compile
[DEBUG]       org.apache.maven.doxia:doxia-decoration-model:jar:1.7.4:compile
[DEBUG]       org.apache.maven.doxia:doxia-skin-model:jar:1.7.4:compile
[DEBUG]       org.apache.maven.doxia:doxia-module-xhtml:jar:1.7:compile
[DEBUG]       org.codehaus.plexus:plexus-i18n:jar:1.0-beta-7:compile
[DEBUG]       org.codehaus.plexus:plexus-container-default:jar:1.0-alpha-30:compile
[DEBUG]          junit:junit:jar:3.8.1:compile
[DEBUG]       org.codehaus.plexus:plexus-velocity:jar:1.2:compile
[DEBUG]       org.apache.velocity:velocity:jar:1.7:compile
[DEBUG]       org.apache.velocity:velocity-tools:jar:2.0:compile
[DEBUG]          commons-beanutils:commons-beanutils:jar:1.7.0:compile
[DEBUG]          commons-digester:commons-digester:jar:1.8:compile
[DEBUG]          commons-chain:commons-chain:jar:1.1:compile
[DEBUG]          commons-validator:commons-validator:jar:1.3.1:compile
[DEBUG]          dom4j:dom4j:jar:1.1:compile
[DEBUG]          oro:oro:jar:2.0.8:compile
[DEBUG]          sslext:sslext:jar:1.2-0:compile
[DEBUG]          org.apache.struts:struts-core:jar:1.3.8:compile
[DEBUG]             antlr:antlr:jar:2.7.2:compile
[DEBUG]          org.apache.struts:struts-taglib:jar:1.3.8:compile
[DEBUG]          org.apache.struts:struts-tiles:jar:1.3.8:compile
[DEBUG]       commons-collections:commons-collections:jar:3.2.1:compile
[DEBUG]       commons-lang:commons-lang:jar:2.4:compile
[DEBUG]    org.apache.maven.wagon:wagon-provider-api:jar:1.0-beta-6:compile
[DEBUG]    org.apache.commons:commons-lang3:jar:3.5:compile
[DEBUG]    commons-io:commons-io:jar:2.5:compile
[DEBUG]    org.apache.httpcomponents:httpclient:jar:4.5.2:compile
[DEBUG]       org.apache.httpcomponents:httpcore:jar:4.4.4:compile
[DEBUG]       commons-logging:commons-logging:jar:1.2:compile
[DEBUG]    com.thoughtworks.qdox:qdox:jar:2.0-M10:compile
[DEBUG]    org.codehaus.plexus:plexus-java:jar:1.0.3:compile
[DEBUG]       org.ow2.asm:asm:jar:7.0:compile
[DEBUG]    org.codehaus.plexus:plexus-archiver:jar:3.6.0:compile
[DEBUG]       org.apache.commons:commons-compress:jar:1.16.1:compile
[DEBUG]          org.objenesis:objenesis:jar:2.6:compile
[DEBUG]       org.iq80.snappy:snappy:jar:0.4:compile
[DEBUG]       org.tukaani:xz:jar:1.8:runtime
[DEBUG]    org.codehaus.plexus:plexus-io:jar:3.1.1:compile
[DEBUG]    org.codehaus.plexus:plexus-utils:jar:3.0.24:compile
[DEBUG]    org.codehaus.plexus:plexus-interactivity-api:jar:1.0-alpha-6:compile
[DEBUG] Created new class realm plugin>org.apache.maven.plugins:maven-javadoc-plugin:3.1.0
[DEBUG] Importing foreign packages into class realm plugin>org.apache.maven.plugins:maven-javadoc-plugin:3.1.0
[DEBUG]   Imported:  < maven.api
[DEBUG] Populating class realm plugin>org.apache.maven.plugins:maven-javadoc-plugin:3.1.0
[DEBUG]   Included: org.apache.maven.plugins:maven-javadoc-plugin:jar:3.1.0
[DEBUG]   Included: org.sonatype.aether:aether-util:jar:1.7
[DEBUG]   Included: org.sonatype.sisu:sisu-inject-bean:jar:1.4.2
[DEBUG]   Included: org.sonatype.sisu:sisu-guice:jar:noaop:2.1.7
[DEBUG]   Included: org.codehaus.plexus:plexus-interpolation:jar:1.14
[DEBUG]   Included: org.codehaus.plexus:plexus-component-annotations:jar:1.7.1
[DEBUG]   Included: org.sonatype.plexus:plexus-sec-dispatcher:jar:1.3
[DEBUG]   Included: org.sonatype.plexus:plexus-cipher:jar:1.4
[DEBUG]   Included: org.apache.maven.reporting:maven-reporting-api:jar:3.0
[DEBUG]   Included: org.apache.maven:maven-archiver:jar:3.2.0
[DEBUG]   Included: org.apache.maven.shared:maven-shared-utils:jar:3.2.0
[DEBUG]   Included: org.apache.maven.shared:maven-invoker:jar:3.0.0
[DEBUG]   Included: org.apache.maven.shared:maven-common-artifact-filters:jar:3.0.0
[DEBUG]   Included: org.apache.maven.shared:maven-artifact-transfer:jar:0.10.1
[DEBUG]   Included: commons-codec:commons-codec:jar:1.11
[DEBUG]   Included: org.apache.maven.doxia:doxia-sink-api:jar:1.7
[DEBUG]   Included: org.apache.maven.doxia:doxia-logging-api:jar:1.7
[DEBUG]   Included: org.apache.maven.doxia:doxia-site-renderer:jar:1.7.4
[DEBUG]   Included: org.apache.maven.doxia:doxia-core:jar:1.7
[DEBUG]   Included: xmlunit:xmlunit:jar:1.5
[DEBUG]   Included: org.apache.maven.doxia:doxia-decoration-model:jar:1.7.4
[DEBUG]   Included: org.apache.maven.doxia:doxia-skin-model:jar:1.7.4
[DEBUG]   Included: org.apache.maven.doxia:doxia-module-xhtml:jar:1.7
[DEBUG]   Included: org.codehaus.plexus:plexus-i18n:jar:1.0-beta-7
[DEBUG]   Included: junit:junit:jar:3.8.1
[DEBUG]   Included: org.codehaus.plexus:plexus-velocity:jar:1.2
[DEBUG]   Included: org.apache.velocity:velocity:jar:1.7
[DEBUG]   Included: org.apache.velocity:velocity-tools:jar:2.0
[DEBUG]   Included: commons-beanutils:commons-beanutils:jar:1.7.0
[DEBUG]   Included: commons-digester:commons-digester:jar:1.8
[DEBUG]   Included: commons-chain:commons-chain:jar:1.1
[DEBUG]   Included: commons-validator:commons-validator:jar:1.3.1
[DEBUG]   Included: dom4j:dom4j:jar:1.1
[DEBUG]   Included: oro:oro:jar:2.0.8
[DEBUG]   Included: sslext:sslext:jar:1.2-0
[DEBUG]   Included: org.apache.struts:struts-core:jar:1.3.8
[DEBUG]   Included: antlr:antlr:jar:2.7.2
[DEBUG]   Included: org.apache.struts:struts-taglib:jar:1.3.8
[DEBUG]   Included: org.apache.struts:struts-tiles:jar:1.3.8
[DEBUG]   Included: commons-collections:commons-collections:jar:3.2.1
[DEBUG]   Included: commons-lang:commons-lang:jar:2.4
[DEBUG]   Included: org.apache.commons:commons-lang3:jar:3.5
[DEBUG]   Included: commons-io:commons-io:jar:2.5
[DEBUG]   Included: org.apache.httpcomponents:httpclient:jar:4.5.2
[DEBUG]   Included: org.apache.httpcomponents:httpcore:jar:4.4.4
[DEBUG]   Included: commons-logging:commons-logging:jar:1.2
[DEBUG]   Included: com.thoughtworks.qdox:qdox:jar:2.0-M10
[DEBUG]   Included: org.codehaus.plexus:plexus-java:jar:1.0.3
[DEBUG]   Included: org.ow2.asm:asm:jar:7.0
[DEBUG]   Included: org.codehaus.plexus:plexus-archiver:jar:3.6.0
[DEBUG]   Included: org.apache.commons:commons-compress:jar:1.16.1
[DEBUG]   Included: org.objenesis:objenesis:jar:2.6
[DEBUG]   Included: org.iq80.snappy:snappy:jar:0.4
[DEBUG]   Included: org.tukaani:xz:jar:1.8
[DEBUG]   Included: org.codehaus.plexus:plexus-io:jar:3.1.1
[DEBUG]   Included: org.codehaus.plexus:plexus-utils:jar:3.0.24
[DEBUG]   Included: org.codehaus.plexus:plexus-interactivity-api:jar:1.0-alpha-6
[DEBUG] Configuring mojo org.apache.maven.plugins:maven-javadoc-plugin:3.1.0:jar from plugin realm ClassRealm[plugin>org.apache.maven.plugins:maven-javadoc-plugin:3.1.0, parent: sun.misc.Launcher$AppClassLoader@7852e922]
[DEBUG] Configuring mojo 'org.apache.maven.plugins:maven-javadoc-plugin:3.1.0:jar' with basic configurator -->
[DEBUG]   (f) applyJavadocSecurityFix = true
[DEBUG]   (f) attach = true
[DEBUG]   (f) author = true
[DEBUG]   (f) bootclasspathArtifacts = []
[DEBUG]   (f) bottom = Copyright &#169; {inceptionYear}&#x2013;{currentYear} {organizationName}. All rights reserved.
[DEBUG]   (f) breakiterator = false
[DEBUG]   (f) classifier = javadoc
[DEBUG]   (f) debug = false
[DEBUG]   (f) defaultManifestFile = L:\ops\tonexus\target\classes\META-INF\MANIFEST.MF
[DEBUG]   (f) detectJavaApiLink = true
[DEBUG]   (f) detectLinks = false
[DEBUG]   (f) detectOfflineLinks = true
[DEBUG]   (f) docfilessubdirs = false
[DEBUG]   (f) docletArtifact = groupId = 'null'
artifactId = 'null'
version = 'null'
[DEBUG]   (f) docletArtifacts = []
[DEBUG]   (f) doctitle = my-maven 5.0.0 API
[DEBUG]   (f) encoding = UTF-8
[DEBUG]   (f) failOnError = true
[DEBUG]   (f) failOnWarnings = false
[DEBUG]   (f) finalName = yoodle-5.0.0
[DEBUG]   (f) includeDependencySources = false
[DEBUG]   (f) includeTransitiveDependencySources = false
[DEBUG]   (f) isOffline = false
[DEBUG]   (f) jarOutputDirectory = L:\ops\tonexus\target
[DEBUG]   (f) javaApiLinks = {}
[DEBUG]   (f) javadocDirectory = L:\ops\tonexus\src\main\javadoc
[DEBUG]   (f) javadocOptionsDir = L:\ops\tonexus\target\javadoc-bundle-options
[DEBUG]   (f) keywords = false
[DEBUG]   (f) links = []
[DEBUG]   (f) linksource = false
[DEBUG]   (f) localRepository =       id: local
      url: file:///C:/Users/chintu/.m2/repository/
   layout: default
snapshots: [enabled => true, update => always]
 releases: [enabled => true, update => always]

[DEBUG]   (f) mojo = org.apache.maven.plugins:maven-javadoc-plugin:3.1.0:jar {execution: attach-javadocs}
[DEBUG]   (f) nocomment = false
[DEBUG]   (f) nodeprecated = false
[DEBUG]   (f) nodeprecatedlist = false
[DEBUG]   (f) nohelp = false
[DEBUG]   (f) noindex = false
[DEBUG]   (f) nonavbar = false
[DEBUG]   (f) nooverview = false
[DEBUG]   (f) nosince = false
[DEBUG]   (f) notimestamp = false
[DEBUG]   (f) notree = false
[DEBUG]   (f) offlineLinks = []
[DEBUG]   (f) old = false
[DEBUG]   (f) outputDirectory = L:\ops\tonexus\target\apidocs
[DEBUG]   (f) overview = L:\ops\tonexus\src\main\javadoc\overview.html
[DEBUG]   (f) project = MavenProject: com.scmgalaxy.mavensample:yoodle:5.0.0 @ L:\ops\tonexus\pom.xml
[DEBUG]   (f) quiet = false
[DEBUG]   (f) reactorProjects = [MavenProject: com.scmgalaxy.mavensample:yoodle:5.0.0 @ L:\ops\tonexus\pom.xml]
[DEBUG]   (f) resourcesArtifacts = []
[DEBUG]   (f) serialwarn = false
[DEBUG]   (f) session = org.apache.maven.execution.MavenSession@59aa20b3
[DEBUG]   (f) settings = org.apache.maven.execution.SettingsAdapter@4beaf6bd
[DEBUG]   (f) show = protected
[DEBUG]   (f) skip = false
[DEBUG]   (f) sourceDependencyCacheDir = L:\ops\tonexus\target\distro-javadoc-sources
[DEBUG]   (f) splitindex = false
[DEBUG]   (f) stylesheet = java
[DEBUG]   (f) tagletArtifact = groupId = 'null'
artifactId = 'null'
version = 'null'
[DEBUG]   (f) tagletArtifacts = []
[DEBUG]   (f) taglets = []
[DEBUG]   (f) tags = []
[DEBUG]   (f) use = true
[DEBUG]   (f) useDefaultManifestFile = false
[DEBUG]   (f) useStandardDocletOptions = true
[DEBUG]   (f) validateLinks = false
[DEBUG]   (f) verbose = false
[DEBUG]   (f) version = true
[DEBUG]   (f) windowtitle = my-maven 5.0.0 API
[DEBUG] -- end configuration --
[DEBUG] No maven-compiler-plugin defined in ${build.plugins} or in ${project.build.pluginManagement} for the com.scmgalaxy.mavensample:yoodle:jar:5.0.0. Added Javadoc API link according the javadoc executable version i.e.: 1.8.0
[DEBUG] Found Java API link: https://docs.oracle.com/javase/8/docs/api/
[DEBUG] Trying to add links for modules...
[DEBUG] "C:\Program Files\AdoptOpenJDK\jdk-8.0.212.03-hotspot\jre\..\bin\javadoc.exe" @options @argfile
[INFO]
Loading source file L:\ops\tonexus\src\main\java\com\scmgalaxy\mavensample\App.java...
Constructing Javadoc information...
Standard Doclet version 1.8.0_212
Building tree for all the packages and classes...
Generating L:\ops\tonexus\target\apidocs\com\scmgalaxy\mavensample\App.html...
Generating L:\ops\tonexus\target\apidocs\com\scmgalaxy\mavensample\package-frame.html...
Generating L:\ops\tonexus\target\apidocs\com\scmgalaxy\mavensample\package-summary.html...
Generating L:\ops\tonexus\target\apidocs\com\scmgalaxy\mavensample\package-tree.html...
Generating L:\ops\tonexus\target\apidocs\constant-values.html...
Generating L:\ops\tonexus\target\apidocs\com\scmgalaxy\mavensample\class-use\App.html...
Generating L:\ops\tonexus\target\apidocs\com\scmgalaxy\mavensample\package-use.html...
Building index for all the packages and classes...
Generating L:\ops\tonexus\target\apidocs\overview-tree.html...
Generating L:\ops\tonexus\target\apidocs\index-all.html...
Generating L:\ops\tonexus\target\apidocs\deprecated-list.html...
Building index for all classes...
Generating L:\ops\tonexus\target\apidocs\allclasses-frame.html...
Generating L:\ops\tonexus\target\apidocs\allclasses-noframe.html...
Generating L:\ops\tonexus\target\apidocs\index.html...
Generating L:\ops\tonexus\target\apidocs\help-doc.html...
[INFO] Building jar: L:\ops\tonexus\target\yoodle-5.0.0-javadoc.jar
[DEBUG] adding directory META-INF/
[DEBUG] adding entry META-INF/MANIFEST.MF
[DEBUG] adding directory com/
[DEBUG] adding directory com/scmgalaxy/
[DEBUG] adding directory com/scmgalaxy/mavensample/
[DEBUG] adding directory com/scmgalaxy/mavensample/class-use/
[DEBUG] adding entry allclasses-frame.html
[DEBUG] adding entry allclasses-noframe.html
[DEBUG] adding entry com/scmgalaxy/mavensample/App.html
[DEBUG] adding entry com/scmgalaxy/mavensample/class-use/App.html
[DEBUG] adding entry com/scmgalaxy/mavensample/package-frame.html
[DEBUG] adding entry com/scmgalaxy/mavensample/package-summary.html
[DEBUG] adding entry com/scmgalaxy/mavensample/package-tree.html
[DEBUG] adding entry com/scmgalaxy/mavensample/package-use.html
[DEBUG] adding entry constant-values.html
[DEBUG] adding entry deprecated-list.html
[DEBUG] adding entry help-doc.html
[DEBUG] adding entry index-all.html
[DEBUG] adding entry index.html
[DEBUG] adding entry overview-tree.html
[DEBUG] adding entry package-list
[DEBUG] adding entry script.js
[DEBUG] adding entry stylesheet.css
[INFO]
[INFO] --- maven-install-plugin:2.4:install (default-install) @ yoodle ---
[DEBUG] Dependency collection stats: {ConflictMarker.analyzeTime=47807, ConflictMarker.markTime=22619, ConflictMarker.nodeCount=38, ConflictIdSorter.graphTime=15936, ConflictIdSorter.topsortTime=12851, ConflictIdSorter.conflictIdCount=15, ConflictIdSorter.conflictIdCycleCount=0, ConflictResolver.totalTime=253430, ConflictResolver.conflictItemCount=35, DefaultDependencyCollector.collectTime=17639844, DefaultDependencyCollector.transformTime=369093}
[DEBUG] org.apache.maven.plugins:maven-install-plugin:jar:2.4:
[DEBUG]    org.apache.maven:maven-plugin-api:jar:2.0.6:compile
[DEBUG]    org.apache.maven:maven-project:jar:2.0.6:compile
[DEBUG]       org.apache.maven:maven-settings:jar:2.0.6:compile
[DEBUG]       org.apache.maven:maven-profile:jar:2.0.6:compile
[DEBUG]       org.apache.maven:maven-plugin-registry:jar:2.0.6:compile
[DEBUG]       org.codehaus.plexus:plexus-container-default:jar:1.0-alpha-9-stable-1:compile
[DEBUG]          junit:junit:jar:3.8.1:compile
[DEBUG]          classworlds:classworlds:jar:1.1-alpha-2:compile
[DEBUG]    org.apache.maven:maven-model:jar:2.0.6:compile
[DEBUG]    org.apache.maven:maven-artifact-manager:jar:2.0.6:compile
[DEBUG]       org.apache.maven:maven-repository-metadata:jar:2.0.6:compile
[DEBUG]    org.apache.maven:maven-artifact:jar:2.0.6:compile
[DEBUG]    org.codehaus.plexus:plexus-utils:jar:3.0.5:compile
[DEBUG]    org.codehaus.plexus:plexus-digest:jar:1.0:compile
[DEBUG] Created new class realm plugin>org.apache.maven.plugins:maven-install-plugin:2.4
[DEBUG] Importing foreign packages into class realm plugin>org.apache.maven.plugins:maven-install-plugin:2.4
[DEBUG]   Imported:  < maven.api
[DEBUG] Populating class realm plugin>org.apache.maven.plugins:maven-install-plugin:2.4
[DEBUG]   Included: org.apache.maven.plugins:maven-install-plugin:jar:2.4
[DEBUG]   Included: junit:junit:jar:3.8.1
[DEBUG]   Included: org.codehaus.plexus:plexus-utils:jar:3.0.5
[DEBUG]   Included: org.codehaus.plexus:plexus-digest:jar:1.0
[DEBUG] Configuring mojo org.apache.maven.plugins:maven-install-plugin:2.4:install from plugin realm ClassRealm[plugin>org.apache.maven.plugins:maven-install-plugin:2.4, parent: sun.misc.Launcher$AppClassLoader@7852e922]
[DEBUG] Configuring mojo 'org.apache.maven.plugins:maven-install-plugin:2.4:install' with basic configurator -->
[DEBUG]   (f) artifact = com.scmgalaxy.mavensample:yoodle:jar:5.0.0
[DEBUG]   (f) attachedArtifacts = [com.scmgalaxy.mavensample:yoodle:javadoc:javadoc:5.0.0]
[DEBUG]   (f) createChecksum = false
[DEBUG]   (f) localRepository =       id: local
      url: file:///C:/Users/chintu/.m2/repository/
   layout: default
snapshots: [enabled => true, update => always]
 releases: [enabled => true, update => always]

[DEBUG]   (f) packaging = jar
[DEBUG]   (f) pomFile = L:\ops\tonexus\pom.xml
[DEBUG]   (s) skip = false
[DEBUG]   (f) updateReleaseInfo = false
[DEBUG] -- end configuration --
[INFO] Installing L:\ops\tonexus\target\yoodle-5.0.0.jar to C:\Users\chintu\.m2\repository\com\scmgalaxy\mavensample\yoodle\5.0.0\yoodle-5.0.0.jar
[DEBUG] Writing tracking file C:\Users\chintu\.m2\repository\com\scmgalaxy\mavensample\yoodle\5.0.0\_remote.repositories
[INFO] Installing L:\ops\tonexus\pom.xml to C:\Users\chintu\.m2\repository\com\scmgalaxy\mavensample\yoodle\5.0.0\yoodle-5.0.0.pom
[DEBUG] Writing tracking file C:\Users\chintu\.m2\repository\com\scmgalaxy\mavensample\yoodle\5.0.0\_remote.repositories
[DEBUG] Installing com.scmgalaxy.mavensample:yoodle/maven-metadata.xml to C:\Users\chintu\.m2\repository\com\scmgalaxy\mavensample\yoodle\maven-metadata-local.xml
[INFO] Installing L:\ops\tonexus\target\yoodle-5.0.0-javadoc.jar to C:\Users\chintu\.m2\repository\com\scmgalaxy\mavensample\yoodle\5.0.0\yoodle-5.0.0-javadoc.jar
[DEBUG] Writing tracking file C:\Users\chintu\.m2\repository\com\scmgalaxy\mavensample\yoodle\5.0.0\_remote.repositories
[DEBUG] Installing com.scmgalaxy.mavensample:yoodle/maven-metadata.xml to C:\Users\chintu\.m2\repository\com\scmgalaxy\mavensample\yoodle\maven-metadata-local.xml
[INFO]
[INFO] --- maven-deploy-plugin:2.7:deploy (default-deploy) @ yoodle ---
[DEBUG] Dependency collection stats: {ConflictMarker.analyzeTime=140337, ConflictMarker.markTime=70940, ConflictMarker.nodeCount=32, ConflictIdSorter.graphTime=41125, ConflictIdSorter.topsortTime=35470, ConflictIdSorter.conflictIdCount=14, ConflictIdSorter.conflictIdCycleCount=0, ConflictResolver.totalTime=187631, ConflictResolver.conflictItemCount=32, DefaultDependencyCollector.collectTime=7321191, DefaultDependencyCollector.transformTime=527936}
[DEBUG] org.apache.maven.plugins:maven-deploy-plugin:jar:2.7:
[DEBUG]    org.apache.maven:maven-plugin-api:jar:2.0.6:compile
[DEBUG]    org.apache.maven:maven-project:jar:2.0.6:compile
[DEBUG]       org.apache.maven:maven-settings:jar:2.0.6:compile
[DEBUG]       org.apache.maven:maven-profile:jar:2.0.6:compile
[DEBUG]       org.apache.maven:maven-artifact-manager:jar:2.0.6:compile
[DEBUG]          org.apache.maven:maven-repository-metadata:jar:2.0.6:compile
[DEBUG]       org.apache.maven:maven-plugin-registry:jar:2.0.6:compile
[DEBUG]       org.codehaus.plexus:plexus-container-default:jar:1.0-alpha-9-stable-1:compile
[DEBUG]          junit:junit:jar:3.8.1:compile
[DEBUG]          classworlds:classworlds:jar:1.1-alpha-2:compile
[DEBUG]    org.apache.maven:maven-model:jar:2.0.6:compile
[DEBUG]    org.apache.maven:maven-artifact:jar:2.0.6:compile
[DEBUG]    org.codehaus.plexus:plexus-utils:jar:1.5.6:compile
[DEBUG] Created new class realm plugin>org.apache.maven.plugins:maven-deploy-plugin:2.7
[DEBUG] Importing foreign packages into class realm plugin>org.apache.maven.plugins:maven-deploy-plugin:2.7
[DEBUG]   Imported:  < maven.api
[DEBUG] Populating class realm plugin>org.apache.maven.plugins:maven-deploy-plugin:2.7
[DEBUG]   Included: org.apache.maven.plugins:maven-deploy-plugin:jar:2.7
[DEBUG]   Included: junit:junit:jar:3.8.1
[DEBUG]   Included: org.codehaus.plexus:plexus-utils:jar:1.5.6
[DEBUG] Configuring mojo org.apache.maven.plugins:maven-deploy-plugin:2.7:deploy from plugin realm ClassRealm[plugin>org.apache.maven.plugins:maven-deploy-plugin:2.7, parent: sun.misc.Launcher$AppClassLoader@7852e922]
[DEBUG] Configuring mojo 'org.apache.maven.plugins:maven-deploy-plugin:2.7:deploy' with basic configurator -->
[DEBUG]   (f) artifact = com.scmgalaxy.mavensample:yoodle:jar:5.0.0
[DEBUG]   (f) attachedArtifacts = [com.scmgalaxy.mavensample:yoodle:javadoc:javadoc:5.0.0]
[DEBUG]   (s) localRepository =       id: local
      url: file:///C:/Users/chintu/.m2/repository/
   layout: default
snapshots: [enabled => true, update => always]
 releases: [enabled => true, update => always]

[DEBUG]   (f) offline = false
[DEBUG]   (f) packaging = jar
[DEBUG]   (f) pomFile = L:\ops\tonexus\pom.xml
[DEBUG]   (f) project = MavenProject: com.scmgalaxy.mavensample:yoodle:5.0.0 @ L:\ops\tonexus\pom.xml
[DEBUG]   (f) retryFailedDeploymentCount = 1
[DEBUG]   (f) skip = false
[DEBUG]   (f) updateReleaseInfo = false
[DEBUG] -- end configuration --
[DEBUG] Using transporter WagonTransporter with priority -1.0 for http://35.237.64.4:8083/nexus/content/repositories/airrelease/
[DEBUG] Using connector BasicRepositoryConnector with priority 0.0 for http://35.237.64.4:8083/nexus/content/repositories/airrelease/ with username=admin, password=***
Uploading to tiger: http://35.237.64.4:8083/nexus/content/repositories/airrelease/com/scmgalaxy/mavensample/yoodle/5.0.0/yoodle-5.0.0.jar
Uploaded to tiger: http://35.237.64.4:8083/nexus/content/repositories/airrelease/com/scmgalaxy/mavensample/yoodle/5.0.0/yoodle-5.0.0.jar (2.7 kB at 1.9 kB/s)
Uploading to tiger: http://35.237.64.4:8083/nexus/content/repositories/airrelease/com/scmgalaxy/mavensample/yoodle/5.0.0/yoodle-5.0.0.pom
Uploaded to tiger: http://35.237.64.4:8083/nexus/content/repositories/airrelease/com/scmgalaxy/mavensample/yoodle/5.0.0/yoodle-5.0.0.pom (1.5 kB at 1.2 kB/s)
Downloading from tiger: http://35.237.64.4:8083/nexus/content/repositories/airrelease/com/scmgalaxy/mavensample/yoodle/maven-metadata.xml
[DEBUG] Could not find metadata com.scmgalaxy.mavensample:yoodle/maven-metadata.xml in tiger (http://35.237.64.4:8083/nexus/content/repositories/airrelease/)
[DEBUG] Writing tracking file C:\Users\chintu\.m2\repository\com\scmgalaxy\mavensample\yoodle\resolver-status.properties
Uploading to tiger: http://35.237.64.4:8083/nexus/content/repositories/airrelease/com/scmgalaxy/mavensample/yoodle/maven-metadata.xml
Uploaded to tiger: http://35.237.64.4:8083/nexus/content/repositories/airrelease/com/scmgalaxy/mavensample/yoodle/maven-metadata.xml (311 B at 223 B/s)
[DEBUG] Using transporter WagonTransporter with priority -1.0 for http://35.237.64.4:8083/nexus/content/repositories/airrelease/
[DEBUG] Using connector BasicRepositoryConnector with priority 0.0 for http://35.237.64.4:8083/nexus/content/repositories/airrelease/ with username=admin, password=***
Uploading to tiger: http://35.237.64.4:8083/nexus/content/repositories/airrelease/com/scmgalaxy/mavensample/yoodle/5.0.0/yoodle-5.0.0-javadoc.jar
Uploaded to tiger: http://35.237.64.4:8083/nexus/content/repositories/airrelease/com/scmgalaxy/mavensample/yoodle/5.0.0/yoodle-5.0.0-javadoc.jar (23 kB at 18 kB/s)
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  13.810 s
[INFO] Finished at: 2019-06-03T16:47:50+02:00
[INFO] ------------------------------------------------------------------------







# Docker jenkins ( Setting Up Jenkins )


docker pull jenkins/jenkins

docker run -d -p 8084:8080 --name jenkins jenkins/jenkins


but default jenkins port is 8080
downloaded for windows  https://jenkins.io/download/
if password not working go to C:\Program Files (x86)\Jenkins\conf.xml  under sercuity make it as false but before we need to stop jenkins after making changes we need to start jenkins

http://localhost:8080/
 
http://35.237.64.4:8084


![image](https://user-images.githubusercontent.com/33985509/59152953-29368880-8a4f-11e9-93ec-d029fe0024b9.png)


# Install plugins under jenkins 

Go to Manage Jenkins ------> Plugin Manager



![image](https://user-images.githubusercontent.com/33985509/59152956-5c791780-8a4f-11e9-975f-1155962aa9e6.png)




![image](https://user-images.githubusercontent.com/33985509/59152979-da3d2300-8a4f-11e9-9663-4475680c64d5.png)




![image](https://user-images.githubusercontent.com/33985509/59152988-08226780-8a50-11e9-8cbb-7cecc30a5cac.png)




![image](https://user-images.githubusercontent.com/33985509/59152998-37d16f80-8a50-11e9-9256-a5729da47457.png)




Go to jenkins ---> global tool configuration and add SonarQube servers 



![image](https://user-images.githubusercontent.com/33985509/59153260-9baa6700-8a55-11e9-9157-b7feae700c76.png)



![image](https://user-images.githubusercontent.com/33985509/59153273-d8765e00-8a55-11e9-8a8e-d7184f424065.png)






commands to get public and private keys

ssh-keygen -t rsa

copy the public key in github

Go to git hub ---settings ----- ssh and gpg keys

then copy the private key in sonarqube build project where you give credentials



![image](https://user-images.githubusercontent.com/33985509/59153089-428d0400-8a52-11e9-8578-93c89cf14678.png)



# Build Job

Now i try to buildjob for sonarqube

sonar qube integration can be done by mavaen,Gradle
install sonarqube scanner
sonarqube is for static code analysis


Create new job in jenkins naming as sonarqube  

Go to new item  ----> Free style project -----> name it sonarqube

global configuration before running job download plugins sonar and sonar scanner

Now go to configure in the build job


under the build configuration ---> 
source code management ------> give Repository URL :git@github.com:manishalankala/helloworld-java-maven.git  and Credentials : 

in source code management click on git icon and give credentials

![image](https://user-images.githubusercontent.com/33985509/59153161-7e749900-8a53-11e9-9aff-c2a2d3cc686a.png)


If you are adding it newly then add the private key 

![image](https://user-images.githubusercontent.com/33985509/59153180-ce536000-8a53-11e9-89e1-ce051f73f57d.png)



![image](https://user-images.githubusercontent.com/33985509/59153189-09559380-8a54-11e9-82fa-807ae87a9094.png)




 Then go to dashboard and click buildnow  and check console output
 
 
 ![image](https://user-images.githubusercontent.com/33985509/59153630-8dad1400-8a5e-11e9-9ec6-b3bbf0e11c2f.png)
 
 
 
 
 
 
Another build job 
 
Go to global configuration in jenkins ,select maven and save the version
then build new job 

name : build
Tyepe : free style project 



![image](https://user-images.githubusercontent.com/33985509/59153244-3bb3c080-8a55-11e9-889e-5fe72b2cb8a9.png)





![image](https://user-images.githubusercontent.com/33985509/59153250-656ce780-8a55-11e9-8b18-05c04cd23375.png)




then run buildnow



![image](https://user-images.githubusercontent.com/33985509/59153626-327b2180-8a5e-11e9-9820-6b1037a94947.png)




if you run build you get following error
[build] $ mvn compile
FATAL: command execution failed  

Then follow below

Jenkins ----> Global tool configuration -----> Maven installations Name: Maven   Install automatically\

On build tab ------>  invoke top level maven targets ------> maven targets ------> Maven Version: maven Goals : compile





 
Creating one more build 

Name: Unit testing 
Type: free style project



![image](https://user-images.githubusercontent.com/33985509/59153352-90f0d180-8a57-11e9-911b-b2bb8e4eb170.png)



![image](https://user-images.githubusercontent.com/33985509/59153361-c695ba80-8a57-11e9-8d45-94cdc9221e23.png)



 goals is mentioned wrong!!!
 
 
 Then run build now
 
 
 ![image](https://user-images.githubusercontent.com/33985509/59153623-09f32780-8a5e-11e9-933b-839c3597e43c.png)
 
 
 Check in console output for the success result
 
 
 
Creating one more build 

Name: package
Type: multi configuration



![image](https://user-images.githubusercontent.com/33985509/59153397-9f8bb880-8a58-11e9-9bbe-96e8df414c36.png)



![image](https://user-images.githubusercontent.com/33985509/59153406-fdb89b80-8a58-11e9-9e9c-9e7b6a723cd5.png)



run build now

![image](https://user-images.githubusercontent.com/33985509/59153419-3fe1dd00-8a59-11e9-9eb6-d013f3bd4bd1.png)


Check in console output for the success result



Creating one more build 

Name: DeploytoNexus 
Type: free style project


![image](https://user-images.githubusercontent.com/33985509/59153445-ee861d80-8a59-11e9-9660-1d664eb2deb0.png)




![image](https://user-images.githubusercontent.com/33985509/59153455-3016c880-8a5a-11e9-8459-b24c5f84de91.png)




![image](https://user-images.githubusercontent.com/33985509/59153458-4d4b9700-8a5a-11e9-8bd6-969790856216.png)




![image](https://user-images.githubusercontent.com/33985509/59153470-8126bc80-8a5a-11e9-915e-7fe18d173dfa.png)




![image](https://user-images.githubusercontent.com/33985509/59153477-a74c5c80-8a5a-11e9-9d70-f16c81266c90.png)





![image](https://user-images.githubusercontent.com/33985509/59153595-3195c000-8a5d-11e9-981e-96609a43b172.png)




 
Deployment process 
 
sonarqube ---> build ----> unit testing ----> Package -----> DeploytoNexus

Now to do deployment process

go to sonarqube build job and click on configure tab ---> post build actions 



![image](https://user-images.githubusercontent.com/33985509/59153540-2e99d000-8a5b-11e9-8a1d-3a05a87df71c.png)



go to build job and click on configure tab ---> post build actions 



![image](https://user-images.githubusercontent.com/33985509/59153544-7b7da680-8a5b-11e9-8704-e8fae368a3bd.png)




go to Unit Testing build job and click on configure tab ---> post build actions 



![image](https://user-images.githubusercontent.com/33985509/59153549-a9fb8180-8a5b-11e9-891b-31c12552eda0.png)
 
 
 
 
go to package build job and click on configure tab ---> post build actions 



![image](https://user-images.githubusercontent.com/33985509/59153555-052d7400-8a5c-11e9-9c98-603de0b0c081.png)
 
 
 
 
 
 
install pipeline plugin 
 
https://wiki.jenkins.io/display/JENKINS/Pipeline+Plugin


we find the + icon  then add name sonarbuildphase


![image](https://user-images.githubusercontent.com/33985509/59153605-7de10000-8a5d-11e9-99ff-1942068915ff.png)



![image](https://user-images.githubusercontent.com/33985509/59153610-a963ea80-8a5d-11e9-8ad0-d7a7593d2270.png)






















(Diffrent )
docker pull jenkins/jenkins

#####Before ######
docker run --name test_jenkins -d -p 80:8080 -p 50000:50000 -v /var/lib/jenkins_docker:/var/jenkins_home jenkins

####After#######
docker run --name jm1 -d -p 80:8080 -p 50000:50000 -v /var/lib/docker/volumes/jm1_vol:/var/jenkins_home jenkinsci/blueocean:latest



########Grafana#######################
docker run -d --name=grafana -p 3000:3000 grafana/grafana

default it uses syslite database if we want to change we need to chnage grafana.ini file
if its not in in the same server mention external


##########Graphite######################

docker pull hopsoft/graphite-statsd

*exposing and running graphite & statsd

docker run -d --name graphite --restart=always-p 81:81 -p 8125:8125/udp hopsoft/graphite-statsd


to change smapling frequency and utention period ,go to docker container ---> docker exec -it graphite bash and look for below file

storage-schemas.conf

vi storage-schemas.conf

for every new configuration for example
[shoehub]
pattern = shoehub\.
retentions = 20s:5h




Note:
#sonarqube container exited
#docker start container id
#docker ps -f "status=exited"




















Chef

![image](https://user-images.githubusercontent.com/33985509/59063276-0322b400-88a8-11e9-82ae-9b412c50e384.png)




![image](https://user-images.githubusercontent.com/33985509/59063395-4715b900-88a8-11e9-995c-54ba01e926ae.png)




![image](https://user-images.githubusercontent.com/33985509/59063489-7e846580-88a8-11e9-9690-c066b2bda399.png)










