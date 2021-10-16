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
//        stage('install npm') {
 //           steps {        
//                sh 'npm install -g uglify-js@3'
 //               sh 'npm install -g clean-css-cli@5.1'
 //           }
 //       }
         stage('build') {
             steps {
                 sh 'uglifyjs www/js/*.js -o www/min/*.min.js'
                 sh 'npm bin -g'
                 
              //parallel(
               //"parh" : { sh "npm bin -g"},  
               //"uglifyjs" : { sh "uglifyjs www/css/* -o www/min"},
              // "cleancss" : { sh "cleancss www/css/* -o www/min"} )
             }
         }
    }
}
