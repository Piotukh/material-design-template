pipeline {
    agent any
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
