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



## •	connect agent to master node
3.	Configure tools – NodeJS - 1
•	Manage Jenkins -> Global tool configuration
-	Add NodeJS installations with version of NodeJS and global npm packages to install (uglify-js, clean-css-cli)
4.	Create “Multibranch Pipeline” pipeline job (work inside Lab folder) - 3
•	folder name – your name in camel case (LinusTorvalds)
•	Git: fork https://github.com/joashp/material-design-template repo
Write Jenkinsfile which describes declarative pipeline
•	define NPM tools in pipeline section
•	Run in parallel stages for compressing JS, CSS files by using next utils:
-	Uglify-js
-	clean-css
www/css -> www/min
www/js -> www/min
•	create tar archive (ignore .git, css and js folders)
•	archive result
5.	Setup the GitHub webhook to trigger the jobs - 2
•	GitHub plugin - http(s)://JENKINS_URL/github-webhook/
-	Enable ‘GitHub hook trigger for Git SCM polling’
![image](https://user-images.githubusercontent.com/63563263/137626393-4466fad9-b505-41d6-a9cc-5fc989dd572b.png)

