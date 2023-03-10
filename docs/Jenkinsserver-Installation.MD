# Jenkins server Installation
------------------------------
Prerequisites
-------------------
EC2 Linux 7.x Instance (t2.small for 2GB RAM and Allow port 8080 in SG level)

Java v1.8.x

Install Java

We will be using open java for our demo, Get latest version from http://openjdk.java.net/install/

yum install java-1.8* -y // needed but in amazon linux you can directly install 

yum install java // this is for amazon linux

#yum -y install java-1.8.0-openjdk

Confirm Java Version

Lets install java and set the java home

java -version

find /usr/lib/jvm/java-1.8* | head -n 3

JAVA_HOME=/usr/lib/jvm/java-17-amazon-corretto.x86_64/bin/java

export JAVA_HOME

PATH=$PATH:$HOME/bin:$JAVA_HOME

# To set it permanently update your .bash_profile
--------------------------------------------------
source ~/.bash_profile

The output should be something like this,

[root@jenkins-master ~]# java -version

openjdk version "17.0.5" 2022-10-18 LTS

OpenJDK Runtime Environment Corretto-17.0.5.8.1 (build 17.0.5+8-LTS)

OpenJDK 64-Bit Server VM Corretto-17.0.5.8.1 (build 17.0.5+8-LTS, mixed mode, sharing)

# Install Jenkins
-----------------

You can install jenkins using the rpm or by setting up the repo. We will setup the repo so that we can update it easily in future. Get latest version of jenkins from 

https://pkg.jenkins.io/redhat-stable/

yum -y install wget

wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo

rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key

yum -y install jenkins


# Start the Jenkins service
---------------------------
systemctl start jenkins

# Enable the Jenkins service even after reboot to start Jenkins automatically
--------------------------------------------------------------------------
systemctl enable jenkins


# Accessing the jenkins with below way
--------------------------------------


Accessing Jenkins

By default jenkins runs at port 8080, You can access jenkins at

http://YOUR-SERVER-PUBLIC-IP:8080
Configure Jenkins

# Take the below path to generate password
------------------------------------------

cat /var/lib/jenkins/secrets/initialAdminPassword

The default Username is admin

Grab the default password

Password Location:/var/lib/jenkins/secrets/initialAdminPassword

Skip Plugin Installation; We can do it later

Change admin password

Admin > Configure > Password

Configure java path

Manage Jenkins > Global Tool Configuration > JDK

Create another admin user id

Test Jenkins Jobs

Create ???new item???

Enter an item name ??? My-First-Project

Chose Freestyle project

Under Build section Execute shell : echo "Welcome to Jenkins Demo"

Save your job

Build job

Check "console output"