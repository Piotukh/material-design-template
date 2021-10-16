pipeline {
    agent {
        label slave1
    }
    tools {
        nodejs 'nodejs'
    }
    stages {
        stage('checkout') {
            steps {
                checkout scm
            }
        }
        stage('install npm') {
            steps {        
                sh 'npm install -g uglify-js@3'
                sh 'npm install -g clean-css-cli@5.1'
            }
        }
    }
}
