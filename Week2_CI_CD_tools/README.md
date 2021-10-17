1.	 Create Jenkins VM with internet access 
•	AWS – t2.micro should be enough

![Alt text]

•	install openjdk-8-jdk or openjdk-11-jdk, Git

    sudo apt update
    sudo apt update
    sudo apt install -y openjdk-11-jdk
    sudo apt install -y git
    
•	install Jenkins with enabling autostart on startup

•	setup custom port 8081 for Jenkins

•	plugins – select plugins, add GitHub and Role-based authorization strategy

•	add new user – jenkins-NAME (your fullname, jenkins-linustorvalds)

2.	 Create Agent VM - 1
•	openjdk-8-jre, Git
•	prepare SSH keys
•	connect agent to master node
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

