pipeline {
    agent {
        label master
    }
    tools {
        nodejs 'nodejs'
    }
    stages {
        stage('checkout') {
            steps {
                checkout scm
            }
        stage('install npm') {
            steps {        
                sh 'npm install -g uglify-js@3'
                sh 'npm install -g clean-css-cli@5.1'
            }
        }
        stage('parallel') {
                parallel(
                         "uglifyjs" : {sh 'uglifyjs /www/css/* -o min'})
        }
    }
}
