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
         stage('npm info') {
             steps {
                 sh 'npm bin -g'
                 sh 'npm list -g'
             }
          }     
          stage('compression') {         
             parallel {
                stage('uglyfyjs') {
                    steps {
                        sh 'rm -f www/min/*.min.js'
                        sh 'ls www/js | xarg -I{i} uglifyjs www/js/{i} -o www/min/{i}'
                     }
                }
                stage('cleancss') {
                    steps {
                         sh "cleancss www/css/* -o www/min/new.css"
                         }
                     }   
                        
                 }
             }     
         }       
    }
