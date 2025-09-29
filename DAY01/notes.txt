Jenkins by KK FUNDA
====================

Explain the flow diagram : developer --> GitHub --> maven --> SonarQube --> Nexus --> Tomcat  --> mail


Jenkins
=======

IQ] what is Jenkins?

-->Jenkins is an open source Continuous Integration[CI] tool, cross-platform tool, written in Java.

--> Kohsuke Kawaguchi is Creator of the Jenkins CI server in 2004

-->Initially, it was called Hudson, but in 2011 it was renamed to Jenkins


Advantages  of Jenkins
======================
--> It’s an open source tool with great community support.

--> Easy to install and It has a simple configuration through a web-based GUI, which speeds up the Job[deployment process]

--> It has around 1900+ plugins to ease your work. If a plugin does not exist, just code it up and share with the community (https://plugins.jenkins.io/).

--> Its built with Java and hence, it is portable on all major platforms.

--> Good documentation and enriched support articles/information available on internet which will help beginners to start easy.



Continuous Integration[CI]:
==========================

---> explain diagram 

Continuous Integration (CI) is the process of automating the build and testing of code every time a team member commits changes to version control.

(OR)

Continuous Integration is a development practice where developers integrate their code into a shared remote repository frequently, preferably several times a day. Each integration is verified by an automated build (including test) to detect integration errors as quickly as possible.


CI Advantages
-------------
--> Immediate bug detection
--> Less Merge Conflicts
--> Deploy an application at any given point
--> Improved Code Quality [Consistent Testing, Code Reviews]
--> Developers receive immediate feedback on their code changes, allowing them to address issues promptly.


Continuous Delivery:
====================
every successful build that has passed all the relevant automated tests and quality gates can potentially be deployed in to production via fully automated one click process.

diagram 
-------

code done --> unit tests --> Integrate --> Acceptance Test ---> Deploy into production
         AUTO           AUTO          AUTO                 MANUAL 

NOTE: Once we get the approval from the client and the sign-off mail from the QA team then we are going   to deploy


Continuous Deployment: 
======================

The practicing of automatically deploying every successful build directly into production without any manual steps knows as Continuous deployment.


code done --> unit tests --> Integrate --> Acceptance Test ---> Deploy into production
         AUTO           AUTO          AUTO                 AUTO 









IQ] Which one you are using continuous delivery or continuous deployment ?

ANS: I involved in many projects so we are using continuous deployment in "IN-HOUSE PROJECTS"   
     
      EX: Company internal Project : HR, company website ---> 

    Coming to continuous delivery , We used for "client (external) projects"

     EX: jio, flipkart, amazon, etc







What Jenkins can do?


• Integrate with many different Version Control Systems (GitHub, BitBucket , GitLab, ...)
• Generate test reports (JUnit)
• Push the builds to various artifact repositories[nexus/jfrog]
• Deploys directly to production or test environments
• Notify stakeholders of build status (Through Email/slack,etc)



List of popular Continuous Integration tools
============================================

SNO     Product           Is Open Source?
===========================================
1       Jenkins              Yes  [community edition]
2       Cloudbees Jenkins    No   [Enterprise edition] 
2       Bamboo               No
3       Cruise Control       Yes
4       Travis CI            Yes and Paid also
5       Circle CI            Yes and Paid also
6       GitLab CI            Yes and Paid
7       TeamCity             Yes and Paid


NOTE: default port for jenkins: 8080


Jenkins Installation
====================
prerequsite : JAVA, min: t2.medium

JAVA Installation
-----------------

step 1: launch an ec2 machine(t2.medium), connect to that machine

step 2: switch to root user [sudo su - ]





JENKINS Installation
====================

--> LTS[Long Term Support] ---> stable version without any issues.
--> search on google [ download jenkins ] --> LTS --> Redhat/fedora/centos


step 1: sudo su -

step 2: 

yum install wget tree -y




sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo yum upgrade
# Add required dependencies for the jenkins package
sudo yum install fontconfig java-21-openjdk
sudo yum install jenkins
sudo systemctl daemon-reload




step 3: 

 systemctl enable jenkins

step 4: 

  systemctl status jenkins
  systemctl start jenkins
  systemctl status jenkins

step 5: 

http://13.201.93.75:8080/  --> please make sure to enable 8080 port 

cat /var/lib/jenkins/secrets/initialAdminPassword

step 6:

click on suggested plugins

step 7:

user_name:  kkfunda
password: kkfunda
confirm password: kkfunda
Full Name: KK FUNDA

save And Continue  --> Save and finish --> start using jenkins 
