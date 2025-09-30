SonarQube installation
======================

pls use github link


Nexus installation
==================

pls use github link

Installation of tomcat
======================

pls use github link

Install jenkins
===============

pls use github link



Automate all the tasks using jenkins
=====================================

How to create a job
===================

Jenkins DashBoard --> New item --> enter an item name(jio-dev) --> freestyle project --> ok --> general --> description --> scroll down --> source code management -->  select git(GitHub,bitbucket,gitlab) --> repository url --> After that we will get an error --> pls install git in jenkins server --> yum install git -y --> save --> click on configure for any updates --> 



--> branches to build --> */development --> scroll down --> build -->add build --> Invoke maven toplevel targets ---> goals [clean package] --> save 


--> for run the job click on job --> In left side click on buid now --> failed --> click on job --> console output --> Due maven not instaled uild is failing 

--> check maven is installed or not in jenkins server 

  mvn -version


IQ] Where we need to install maven in linux server or in the jenkins server itself ?

ANS: If you go for linux server only one maven install is possible but in jenkins many versions possible so we are going to install in the jenkins server.



How to download maven in jenkins ?
==================================

go to jenkins dashboard --> manage jenkins --> tools -->scroll down --> add maven -->  maven 3.9.8 --> select version 3.9.8 --> add many versions --> save 

click on job --> configure --> scroll down --> build steps -->  select maven version --> save 

--> again run the job --> It will success 


/var/lib/jenkins/workspace/jio-dev/target/ --> warfile location




SonarQube server integration
============================

take ip address of SonarQube server [http://3.110.105.157:9000/] --> go to GitHub repository --> select the correct branch [development] --> pom.xml --> edit the file --> in <properties> tag keep sonarqube server details 


--> go to job --> configure --> scroll down --> build [ clean package sonar:sonar ] --> save

--> go and see the sonarqube server --> check the projects --> now build the job --> success.





Nexus integration with jenkins
===============================

step 1: connect to maven server, Where java projects are available

step 2: where to keep our repository details?

update the details in pom.xml

          <distributionManagement>

            <repository>
              <id>nexus</id>
              <name>KK FUNDA Releases Nexus Repository</name>
              <url>http://13.204.46.151:8081/repository/jio-release/</url>
            </repository>

            <snapshotRepository>
              <id>nexus</id>
              <name>KK FUNDA Snapshot Nexus Repository </name>
              <url>http://13.204.46.151:8081/repository/jio-snapshot/</url>
            </snapshotRepository>

        </distributionManagement>

step 3: Where we need to keep nexus credentials?

--> In SonarQube we updated credentials in pom.xml


NOTE: maven is installed in jenkins pls check correct path of settings.xml


find / -name settings.xml

--> In nexus, repo details in pom.xml and credentials in 
 cd /var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven_3.9.9/conf/


   <server>
      <id>nexus</id>
      <username>admin</username>
      <password>password</password>
    </server>


--> click on job --> configure --> build --> clean deploy sonar:sonar --> save build now 


tomcat integration
===================

step 1: install "deploy to container" plugin

step 2: goto post build actions ---> deploy war/ear container 
   
        **/maven-web-application.war
      
        Containers --> add containers --> tomcat 9 --> URL , add credentials

step 3: build now
