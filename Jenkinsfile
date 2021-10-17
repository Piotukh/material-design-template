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
          stage('compressing') {         
             parallel {
                stage('uglyfyjs') {
                    steps {
                        sh 'rm -f www/min/*.js'
                        sh 'ls -l www/js | wc -l'
                        sh 'cat www/js/* | uglifyjs -o www/min/min.js'
                     }
                }
                stage('cleancss') {
                    steps {
                         sh 'rm -f www/min/*.css'
                         sh "cat www/css/* | cleancss -o www/min/min.css"
                         }
                     }   
                        
                 }
             } 
        stage('archiving') {
            steps {
            
            }
        }
         }       
    }
