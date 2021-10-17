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
                        sh 'rm -f www/min/*.js'
                        sh 'ls -l www/js | wc -l'
                        sh 'uglifyjs www/js/* -oe www/min/'
                     }
                }
                stage('cleancss') {
                    steps {
                         sh 'rm -f www/min/*.css'
                         sh "cleancss www/css/* -oe www/min/"
                         }
                     }   
                        
                 }
             }     
         }       
    }
