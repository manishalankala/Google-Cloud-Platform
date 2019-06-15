

# CI/CD using Google Cloud Platform


![image](https://user-images.githubusercontent.com/33985509/59151479-25493d00-8a34-11e9-9cff-90a50130124c.png)




* CI
* CD
* IAC
* Docker
* Jira
* Git
* Nexus
* Maven
* Sonarqube
* Jenkins
* Setting up Jira using Docker
* Setting up Nexus Using Docker
* Setting up Sonarqube Using Docker
* Setting up Jenkins using Docker
* Setting up build pipeline
* Setting up jacoco in Jenkins
* Setting up Deployment process in Jenkins
* Setting up Chef,Knife 







## CI

Continuous Integration (CI) is the process of automating the build and testing of code every time a team member commits changes to version control. 

CI encourages developers to share their code and unit tests by merging their changes into a shared version control repository after every small task completion. 

Committing code triggers an automated build system to grab the latest code from the shared repository and to build, test, and validate the full master branch



## CD


Continuous Delivery (CD) is the process to build, test, configure and deploy from a build to a production environment. 

Multiple testing or staging environments create a Release Pipeline to automate the creation of infrastructure and deployment of a new. 

Successive environments support progressively longer-running activities of integration, load, and user acceptance testing.

Continuous Integration starts the CD process and the pipeline stages each successive environment the next upon successful completion of tests.



## IAC


Infrastructure as Code (IaC) is the management of infrastructure (networks, virtual machines, load balancers, and connection topology) in a descriptive model, using the same versioning as DevOps team uses for source code. 

Like the principle that the same source code generates the same binary, an IaC model generates the same environment every time it is applied. 

IaC is a key DevOps practice and is used in conjunction with continuous delivery.




## Docker 

. Two containerized processes can run side-by-side on the same computer, but they can’t interfere with each other.

. They can’t access each other’s data unless explicitly configured to do so.

. Two different applications can run containers on the same hardware with confidence that their processes and data are secure.

. Shared hardware means less hardware. 

. Gone are the days when a company needs thousands of servers to run applications. 

. That hardware can be shared between different business units or entirely different enterprise clients. 

. The result is massive new economies of scale for private and public centers alike.

. The Docker command-line interface (CLI)

. The Docker Engine

. Faster scaling of systems

. Better software delivery

. Flexibility

. Software-defined networking

. The rise of microservices architecture


I did installed docker on Centos 7



## Steps to install Docker CE


yum update

Install the latest version of Docker CE and containerd, or go to the next step to install a specific version:

sudo yum install docker-ce docker-ce-cli containerd.io

yum list docker-ce --showduplicates | sort -r


Install a specific version by its fully qualified package name, 

which is the package name (docker-ce) plus the version string (2nd column) starting at the first colon (:), up to the first hyphen, separated by a hyphen (-). 

For example, docker-ce-18.09.1.

sudo yum install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io


sudo systemctl start docker

sudo systemctl status docker

sudo systemctl enable docker



Install from a package:


If you cannot use Docker’s repository to install Docker, you can download the .rpm file for your release and install it manually. 

You need to download a new file each time you want to upgrade Docker CE.


Go to https://download.docker.com/linux/centos/7/x86_64/stable/Packages/ and download the .rpm file for the Docker version you want to install.


Install Docker CE, changing the path below to the path where you downloaded the Docker package.


sudo yum install /path/to/package.rpm

sudo systemctl start docker

sudo systemctl status docker

sudo systemctl enable docker





Always examine scripts downloaded from the internet before running them locally.

curl -fsSL https://get.docker.com -o get-docker.sh\

sudo sh get-docker.sh

<output truncated>



If you would like to use Docker as a non-root user, you should now consider adding your user to the “docker” group with something like:

sudo usermod -aG docker your-user









![image](https://user-images.githubusercontent.com/33985509/59542620-259b7980-8f07-11e9-990d-50cfd6b28bb5.png)








## AWS (Amazon Web Services) – Pros and Cons

This is the dominant cloud platform in the IT space but it could not be suitable for each and every project.

Still, for IaaS services, Amazon will continue dominating the market for many years to come. One of the biggest reasons for the 
popularity of AWS is the massive scope of operations.

AWS has a massive array of services available so far and it is taken as the biggest network of data centers too. 

As per the Gartner report, AWS has the deepest capabilities of governing a large number of users and resources together.

The biggest problem with AWS is its pricing.

However, the Company is lowering down its costs continuously still it is difficult for enterprises understanding its cost structure and managing costs when running a large volume of services. 

These cons are quickly outweighed by a perfect range of benefits and Companies of all sizes are using AWS for a variety of workloads.


## Microsoft Azure – Pros and Cons

Microsoft entered the cloud market little late but it took a jump start with its effective range of services and cloud benefits. 

The major reason for the popularity of the Azure platform is that many Companies deploy Windows software today.

It can be quickly integrated with other applications and actually makes sense for large organizations. 

It is taken as the more loyal platform for Microsoft users. 

Also, if you are an existing Microsoft user then you may get attractive discounts on Azure cloud services.

According to Gartner, Azure is not that much perfect as it should be. 

The customers are facing problems with documentation, technical support, training materials etc. 

Additionally, it does not provide the suitable support to DevOps approaches because of selected automation features and much of management work is completed by the staff itself.




## Google Cloud Platform – Pros and Cons

Google is also a strong candidate in the cloud race since it started the Kubernetes in comparison to the AWS and the Azure. 

Some of the major offerings of Google Cloud Platform includes machine learning, big data analytics and more. 

The other highlights are perfect load balancing, or considerable scaling etc.

GCP has an excellent response time and he knows data centers well. 

Google is ranked third in the IT marketplace because it does not provide as many services as AWS or Azure. Soo, it will expand as needed.

According to Gartner, GCP is not a strategic partner but it is taken as the secondary partner only. 

If your business competes with Amazon then you can freely choose GCP in that case. This is open source platform that is highly DevOps centric and well-aligned to Microsoft Azure.



![image](https://user-images.githubusercontent.com/33985509/59542595-000e7000-8f07-11e9-8186-1d2b643ec6a5.png)







## Create a vm instance in Google cloud account and create external ip 



![image](https://user-images.githubusercontent.com/33985509/59151716-5af02500-8a38-11e9-8210-1edfa9209c38.png)



## Create a firewall port for each application



![image](https://user-images.githubusercontent.com/33985509/59151728-9a1e7600-8a38-11e9-9aca-803ce4c15b6e.png)



## Create a specific port for jira application to run



![image](https://user-images.githubusercontent.com/33985509/59151745-db168a80-8a38-11e9-9d22-ff02006b9b2f.png)



## SSH


![image](https://user-images.githubusercontent.com/33985509/59151763-27fa6100-8a39-11e9-91df-36d99394965c.png)





Install docker on my linux instance



![image](https://user-images.githubusercontent.com/33985509/59153698-d2d24580-8a60-11e9-96dd-7c2cf7bc75cf.png)





## Jira 


Reference link :   https://www.atlassian.com/software/jira


JIRA is an Incident Management Tool used for Project Management, Bug Tracking, Issue Tracking and Workflow. JIRA is based on the following three concepts – Project, Issue and Workflow.


JIRA is used in Bugs, Issues and Change Request Tracking.


JIRA can be used in Help desk, Support and Customer Services to create tickets and track the resolution and status of the created tickets.


JIRA is useful in Project Management, Task Tracking and Requirement Management.


JIRA is very useful in Workflow and Process management.



# Docker  Jira  (Setting up Jira)




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



# Integrate jira with git      (Jira tool with Git repository)


Go to manage apps in jira 



Click on free



Pop up on new Evaluation license & click on generate license
Apply license

we can see Your trial is expiring on 30/Jun/19. Buy a license for this app.



![image](https://user-images.githubusercontent.com/33985509/59152168-2fbd0400-8a3f-11e9-9bdc-772ed76dd758.png)


## Git 


Reference link:   https://git-scm.com/



Git 

. Simultaneous development


. Faster releases


. Built-in integration


. Strong community support


. Git works with your team


. Pull requests


. Branch policies






## Git integration with JIRA


Go to applications tab on in administration


click on Git repositories tab and click on connect to git repository


![image](https://user-images.githubusercontent.com/33985509/59152190-9fcb8a00-8a3f-11e9-9d13-cb7355f85bce.png)




Go to git hub and change your pom.xml file and scroll below




https://github.com/manishalankala/helloworld-java-maven/blob/master/pom.xml



Commit changes fix for AIR-1(which is key of the task created )



open the task in dashboard you can see on the tab git commits(reindexing takes a bit moment)



Go to Git repositories tab in application in administration click on actions and reindex(if you find reindexing is slow this for manual process)



## Sonarqube

Reference link : https://www.sonarqube.org/

SonarQube is an automatic code review tool to detect bugs, vulnerabilities and code smells in your code. 

It can integrate with your existing workflow to enable continuous code inspection across your project branches and pull requests.


SonarQube is NOT (only) a static code analyzer : 

It’s not a replacement for FindBugs or CPPCheck or any other similar tool. 

On the contrary, not only it offers its own static code analysis mechanism that detects coding rules violations but at the same time it’s integrated with external tools like the ones I mentioned. 

The result is that you can get, homogenized, in a single report all issues detected by a variety of static and dynamic analysis tools.


SonarQube is NOT a code coverage tool : 

Clearly NOT. Again it’s integrated with the most popular test coverage tools like JaCoCo, Cobertura, PHPUnit etc. but it doesn’t compute code coverage itself. 

It reads pre-generated unit test report files and displays them in an extremely convenient dasboard.

SonarQube is NOT a code formatter. 

It’s not allowed to modify your code in any way. However you can get formatting suggestions by enabling the CheckStyle, CPPCheck, ScalaStyle rules you want to follow.

SonarQube is NOT a continuous integration system to run your nightly builds : 

You can integrate it with the most popular CI Engines to apply Continuous Inspection but it’s not their replacement.

SonarQube is NOT just another manual code review tool. Indeed SonarQube offers a very powerful mechanism that facilitates code reviews but this is not a standalone features. 

It’s tight to the issues detection mechanism so every code review can be easily associated to the exact part of the problematic code and the developer that caused it.



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




## Nexus


"Nexus is a repository manager. It allows you to proxy, collect, and manage your dependencies so that you are not constantly juggling a collection of JARs.

It makes it easy to distribute your software. 

Internally, you configure your build to publish artifacts to Nexus and they then become available to other developers. 

Will get the benefits of having your own 'central', and there is no easier way to collaborate."

"what is Nexus?" for the Non-programmer

think of it as a library. You can ask it for "artifacts", it will store and retrieve them and assign a standard coordinate system to the artifacts it stores.

If you are developing software, having this facility available allows you to catalog and store your own artifacts using the same "numbering" system that the library uses. 

When a group develops a new system or a library, they submit it to the repository manager. 

Other groups then have a standard way to access these libraries. This standard for cataloging and addressing files brings efficiency.

Source control systems, issue trackers, mailing lists, continuous integration servers, wikis, integrated development environment, and repository managers.


## Maven

Maven leverages the concept of a repository by retrieving the artifacts necessary to build an application and deploying the result of the build process into a repository. 

Maven uses the concept of structured repositories so components can be retrieved to support the build. 

These components or dependencies include libraries, frameworks, containers, etc. 

Maven can identify components in repositories, understand their dependencies, retrieve all that are needed for a successful build, and deploy its output back to repositories when the build is complete.



Maven is a "build management tool", it is for defining how your .java files get compiled to .class, packaged into .jar (or .war or .ear) files, (pre/post)processed with tools, managing your CLASSPATH, and all others sorts of tasks that are required to build your project. It is similar to Apache Ant or Gradle or Makefiles in C/C++, but it attempts to be completely self-contained in it that you shouldn't need any additional tools or scripts by incorporating other common tasks like downloading & installing necessary libraries etc.


It is also designed around the "build portability" theme, so that you don't get issues as having the same code with the same buildscript working on one computer but not on another one (this is a known issue, we have VMs of Windows 98 machines since we couldn't get some of our Delphi applications compiling anywhere else). 

Because of this, it is also the best way to work on a project between people who use different IDEs since IDE-generated Ant scripts are hard to import into other IDEs, but all IDEs nowadays understand and support Maven (IntelliJ, Eclipse, and NetBeans). Even if you don't end up liking Maven, it ends up being the point of reference for all other modern builds tools.


. Maven will (after you declare which ones you are using) download all the libraries that you use and the libraries that they use for you automatically. This is very nice, and makes dealing with lots of libraries ridiculously easy. This lets you avoid "dependency hell". It is similar to Apache Ant's Ivy.

. It uses "Convention over Configuration" so that by default you don't need to define the tasks you want to do. You don't need to write a "compile", "test", "package", or "clean" step like you would have to do in Ant or a Makefile. Just put the files in the places in which Maven expects them and it should work off of the bat.

. Maven also has lots of nice plug-ins that you can install that will handle many routine tasks from generating Java classes from an XSD schema using JAXB to measuring test coverage with Cobertura. Just add them to your pom.xml and they will integrate with everything else you want to do.


# Docker nexus    (Setting up Nexus)


docker pull sonatype/nexus

docker run -d -p 8083:8081 --name nexus sonatype/nexus:oss

![image](https://user-images.githubusercontent.com/33985509/59152239-63e4f480-8a40-11e9-9656-68dc857880d9.png)



http://35.237.64.4:8083/nexus/

Credentials
admin / admin123


![image](https://user-images.githubusercontent.com/33985509/59152258-c4743180-8a40-11e9-91de-ac6a3446776c.png)






# Important nexus modification on the below files



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
.
.
.
.
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  13.810 s
[INFO] Finished at: 2019-06-03T16:47:50+02:00
[INFO] ------------------------------------------------------------------------




## Jenkins

Reference link :  https://jenkins.io/

Jenkins is a powerful application that allows continuous integration and continuous delivery of projects, regardless of the platform you are working on. 

It is a free source that can handle any kind of build or continuous integration. 

You can integrate Jenkins with a number of testing and deployment technologies



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




















# Chef


https://manage.chef.io/login



Here i used 

dockerdemo ----  Master server


jmslave ---    node


Create an origanization name 



You can download the starter kit 


![image](https://user-images.githubusercontent.com/33985509/59154512-0ff40300-8a74-11e9-9082-2179d640e0c7.png)


knife command is found when we install the chefdk



>Chef server

>knife configuration

>cookbooks

>nodes


wget https://packages.chef.io/files/stable/chefdk/4.0.60/el/7/chefdk-4.0.60-1.el7.x86_64.rpm (Installed on worker machine)


curl -O https://packages.chef.io/files/stable/chefdk/4.0.60/el/7/chefdk-4.0.60-1.el7.x86_64.rpm


yum install chefdk-4.0.60-1.el7.x86_64.rpm 


![image](https://user-images.githubusercontent.com/33985509/59154614-5b0f1580-8a76-11e9-8010-a6aff2159ad0.png)


cd 

mkdir chef-repo (Created repo)

[root@dockerdemo ~]# ls
chefdk-4.0.60-1.el7.x86_64.rpm  chef-repo


mkdir cookbooks


mkdir .chef (Created repo)


![image](https://user-images.githubusercontent.com/33985509/59154640-5565ff80-8a77-11e9-9a1e-6098da6229f0.png)


ssh-keygen -t rsa


place the public key in .chef 
      
      
    
it looks for the .chef directory default

[alma252@jmslave1 ~]$ cd ~/.ssh
[alma252@jmslave1 .ssh]$ ls
known_hosts

vi authorized_keys 

copy the public key and save it  else can't able to ssh



ssh -i .chef/jmslave alma252@35.211.155.102 ( ssh to node )


knife bootstrap 35.211.155.102 --ssh-user alma252 -i .chef/jmslave --sudo --node-name gce-jmslave -VV -y





For Reference here 
https://linuxacademy.com/community/posts/show/topic/22511-bootstrap-a-node-using-ssh-publicprivate-key-asking-sudo-pwd



https://linuxacademy.com/community/posts/show/topic/22511-bootstrap-a-node-using-ssh-publicprivate-key-asking-sudo-pwd
https://docs.chef.io/chef_client_overview.html
http://blog.asquareb.com/blog/2014/06/09/basic-chef-knife-commands/
https://linoxide.com/linux-how-to/chef-workstation-server-node-centos-7/
https://www.itzgeek.com/how-tos/linux/centos-how-tos/setup-chef-12-centos-7-rhel-7.html
https://blog.andreev.it/?p=3522
https://docs.chef.io/knife_node.html 
https://docs.chef.io/knife_bootstrap.html
https://serverfault.com/questions/653543/chef-ssh-without-password





https://api.chef.io/organizations/eurodrone/cookbooks





![image](https://user-images.githubusercontent.com/33985509/59154712-6879cf00-8a79-11e9-9e55-e700a7328748.png)



[root@dockerdemo .chef]# knife client list
/opt/chefdk/embedded/lib/ruby/gems/2.6.0/gems/chef-15.0.300/lib/chef/knife/bootstrap.rb:31: warning: already initialized constant Chef::Knife::Bootstrap::SUPPORTED_CONNECTION_
PROTOCOLS
/opt/chefdk/embedded/lib/ruby/gems/2.6.0/gems/chef-15.0.300/lib/chef/knife/bootstrap.rb:31: warning: previous definition of SUPPORTED_CONNECTION_PROTOCOLS was here
/opt/chefdk/embedded/lib/ruby/gems/2.6.0/gems/chef-15.0.300/lib/chef/knife/bootstrap.rb:32: warning: already initialized constant Chef::Knife::Bootstrap::WINRM_AUTH_PROTOCOL_L
IST
/opt/chefdk/embedded/lib/ruby/gems/2.6.0/gems/chef-15.0.300/lib/chef/knife/bootstrap.rb:32: warning: previous definition of WINRM_AUTH_PROTOCOL_LIST was here
/opt/chefdk/embedded/lib/ruby/gems/2.6.0/gems/chef-15.0.300/lib/chef/knife/bootstrap.rb:350: warning: already initialized constant Chef::Knife::Bootstrap::DEPRECATED_FLAGS
/opt/chefdk/embedded/lib/ruby/gems/2.6.0/gems/chef-15.0.300/lib/chef/knife/bootstrap.rb:350: warning: previous definition of DEPRECATED_FLAGS was here
eurodrone-validator
gce-jmslave




[root@dockerdemo .chef]# knife node list
/opt/chefdk/embedded/lib/ruby/gems/2.6.0/gems/chef-15.0.300/lib/chef/knife/bootstrap.rb:31: warning: already initialized constant Chef::Knife::Bootstrap::SUPPORTED_CONNECTION_
PROTOCOLS
/opt/chefdk/embedded/lib/ruby/gems/2.6.0/gems/chef-15.0.300/lib/chef/knife/bootstrap.rb:31: warning: previous definition of SUPPORTED_CONNECTION_PROTOCOLS was here
/opt/chefdk/embedded/lib/ruby/gems/2.6.0/gems/chef-15.0.300/lib/chef/knife/bootstrap.rb:32: warning: already initialized constant Chef::Knife::Bootstrap::WINRM_AUTH_PROTOCOL_L
IST
/opt/chefdk/embedded/lib/ruby/gems/2.6.0/gems/chef-15.0.300/lib/chef/knife/bootstrap.rb:32: warning: previous definition of WINRM_AUTH_PROTOCOL_LIST was here
/opt/chefdk/embedded/lib/ruby/gems/2.6.0/gems/chef-15.0.300/lib/chef/knife/bootstrap.rb:350: warning: already initialized constant Chef::Knife::Bootstrap::DEPRECATED_FLAGS
/opt/chefdk/embedded/lib/ruby/gems/2.6.0/gems/chef-15.0.300/lib/chef/knife/bootstrap.rb:350: warning: previous definition of DEPRECATED_FLAGS was here
gce-jmslave





[root@dockerdemo .chef]# cat knife.rb 


see http://docs.chef.io/config_rb_knife.html for more information on knife configuration options
current_dir = File.dirname(__FILE__)
log_level                :info
log_location             STDOUT
node_name                "manishalankala"
client_key               "#{current_dir}/manishalankala.pem"
chef_server_url          "https://api.chef.io/organizations/eurodrone"
cookbook_path            ["#{current_dir}/../cookbooks"]


knife cookbook site download learn_chef_httpd

tar -xvf learn_chef_httpd-0.2.0.tar.gz

rm -rf learn_chef_httpd-0.2.0.tar.gz

chef generate template httpd_deploy index.html

knife cookbook upload learn_chef_httpd -VV


it didn't worked 




chef generate cookbook httpd_deploy
[root@dockerdemo chef-repo]# cd cookbooks/
[root@dockerdemo cookbooks]# ls
httpd_deploy  learn_chef_httpd




knife node run_list add gce-jmslave "recipe[httpd_deploy]"



![image](https://user-images.githubusercontent.com/33985509/59154929-e50eac80-8a7d-11e9-9f97-59733869a513.png)






Errors:

![image](https://user-images.githubusercontent.com/33985509/59220295-e7c7e980-8bc4-11e9-82b2-3d5ee9d91e38.png)

knife ssh 'gce-jmslave' 'sudo chef-client' alma252 --sudo .chef/jmslave  -VV

knife ssh 'gce-jmslave' 'sudo chef-client' --ssh-user alma252 -i /root/chef-repo/.chef/jmslave -VV    (./chef/jmslave has public key)



![image](https://user-images.githubusercontent.com/33985509/59220515-75a3d480-8bc5-11e9-890e-6465abd24ced.png)






Resolution at here is 

knife ssh "name:gce-jmslave" "sudo chef-client" -x alma252 -i .chef/jmslave


Observation : 

![image](https://user-images.githubusercontent.com/33985509/59220743-ffec3880-8bc5-11e9-93d3-ee196808b176.png)



![image](https://user-images.githubusercontent.com/33985509/59220853-33c75e00-8bc6-11e9-8372-3f912e7d62cd.png)



to confirm on node machine

![image](https://user-images.githubusercontent.com/33985509/59220960-78eb9000-8bc6-11e9-921e-21fb92c3f262.png)



in other screnario we can do this by jenkins

jenkins ---> New Item -----> Free style project ------> name i gave is Deploytochefnodes -----> configure 

![image](https://user-images.githubusercontent.com/33985509/59221518-b8ff4280-8bc7-11e9-8bb0-52c9b6d95447.png)

Then click  on build now will get the errors 


because 

![image](https://user-images.githubusercontent.com/33985509/59221610-fe237480-8bc7-11e9-8ccd-4547e4773f42.png)

its under root permissions we need to change to chown -r jenkins:jenkins /chef-repo

then try giving build now still we face issue the last step would be mv chef-repo/ /opt/ will fix this

i didn't try this scenario in jenkins


so from chef-repo directory 

git init
git add -A .
git -m commit "chef"
git push https://github.com/manishalankala/Google-Cloud-Platform.git

else push to a new repository in git 

the git url can be specified 







# JaCoCo - Java Code Coverage Library 


Reference : https://www.jacoco.org/jacoco/trunk/index.html


https://github.com/manishalankala/jacoco-maven




![image](https://user-images.githubusercontent.com/33985509/59267582-e93bf500-8c4a-11e9-8c4a-2a81a70a0aed.png)



![image](https://user-images.githubusercontent.com/33985509/59267629-fce75b80-8c4a-11e9-81cb-7740abdc45cf.png)



![image](https://user-images.githubusercontent.com/33985509/59267686-1f797480-8c4b-11e9-96d4-f6580d708f42.png)



![image](https://user-images.githubusercontent.com/33985509/59267527-c578af00-8c4a-11e9-83ea-443589d9e70c.png)



![image](https://user-images.githubusercontent.com/33985509/59267481-a712b380-8c4a-11e9-87d9-bf32036e8b76.png)
















