# 1.	 Create Jenkins VM with internet access 
## •	AWS – t2.micro should be enough

![Alt text](https://github.com/Piotukh/material-design-template/blob/master/Week2_CI_CD_tools/1.png)

## •	install openjdk-8-jdk or openjdk-11-jdk, Git

    sudo apt update
    sudo apt update
    sudo apt install -y openjdk-11-jdk
    sudo apt install -y git
    java -version
    
![Alt text](https://github.com/Piotukh/material-design-template/blob/master/Week2_CI_CD_tools/7.png)    
    
## •	install Jenkins with enabling autostart on startup

    wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
    sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
    sudo apt-get install -y jenkins
    sudo systemctl enable jenkins.service

## •	setup custom port 8081 for Jenkins
Edited file /etc/default/jenkins (uncomment string HTTP_PORT and change port 8081)

![Alt text](https://github.com/Piotukh/material-design-template/blob/master/Week2_CI_CD_tools/2.png)

    sudo systemctl restart jenkins.service

## •	plugins – select plugins, add GitHub and Role-based authorization strategy

![Alt text](https://github.com/Piotukh/material-design-template/blob/master/Week2_CI_CD_tools/4.png)
![Alt text](https://github.com/Piotukh/material-design-template/blob/master/Week2_CI_CD_tools/5.png)

## •	add new user – jenkins-NAME (your fullname, jenkins-linustorvalds)

![Alt text](https://github.com/Piotukh/material-design-template/blob/master/Week2_CI_CD_tools/3.png)

# 2.	 Create Agent VM 

![Alt text](https://github.com/Piotukh/material-design-template/blob/master/Week2_CI_CD_tools/1.png)

## •	openjdk-8-jre, Git

    sudo apt update
    sudo apt update
    sudo apt install -y openjdk-8-jre
    sudo apt install -y git
    java -version
    
![Alt text](https://github.com/Piotukh/material-design-template/blob/master/Week2_CI_CD_tools/6.png)    

## •	prepare SSH keys
on master

    cd /var/lib/jenkins
    sudo mkdir .ssh
    cd .ssh
    sudo ssh-keygen
    sudo su
    useradd -d /var/lib/jenkins jenkins

on Agent 

    mkdir /var/lib/jenkins/.ssh
    touch /var/lib/jenkins/.ssh/authorized_keys
    
copy id_rsa.pub to Agent (/var/lib/jenkins/.ssh/) 

    chown -R jenkins /var/lib/jenkins/.ssh
    chmod 600 /var/lib/jenkins/.ssh/authorized_keys
    chmod 700 /var/lib/jenkins/.ssh

## •	connect agent to master node

+ Firstly create credential. Go to Manade Jenkins -> Manage Credentials
![Alt text](https://github.com/Piotukh/material-design-template/blob/master/Week2_CI_CD_tools/9.png)
![Alt text](https://github.com/Piotukh/material-design-template/blob/master/Week2_CI_CD_tools/11.png)
![Alt text](https://github.com/Piotukh/material-design-template/blob/master/Week2_CI_CD_tools/12.png)

+ go to Manage Jenkins -> Mahage Nodes and Clouds -> New Node
![Alt text](https://github.com/Piotukh/material-design-template/blob/master/Week2_CI_CD_tools/8.png)
![Alt text](https://github.com/Piotukh/material-design-template/blob/master/Week2_CI_CD_tools/13.png)

# 3.	Configure tools – NodeJS 

## •	Manage Jenkins -> Global tool configuration. Add NodeJS installations with version of NodeJS and global npm packages to install (uglify-js, clean-css-cli).

![Alt text](https://github.com/Piotukh/material-design-template/blob/master/Week2_CI_CD_tools/14.png)

# 4.	Create “Multibranch Pipeline” pipeline job 

 + Go to New Item -> Write name of Pipeline -> Choose Multibranch Pipeline
 
 + Add Credentials and repo https

![Alt text](https://github.com/Piotukh/material-design-template/blob/master/Week2_CI_CD_tools/15.png)

+ Add Jenkinsfile

![Alt text](https://github.com/Piotukh/material-design-template/blob/master/Week2_CI_CD_tools/16.png)

## • Write Jenkinsfile which describes declarative pipeline

[See Jenkinsfile](https://github.com/Piotukh/material-design-template/blob/master/Jenkinsfile)
[See Build log]

# 5.	Setup the GitHub webhook to trigger the jobs 
## •	GitHub plugin - http(s)://JENKINS_URL/github-webhook/
-	Enable ‘GitHub hook trigger for Git SCM polling’


