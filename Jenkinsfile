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
         stage('build') {
             steps {
                 sh 'uglifyjs www/js/materialize.js -o www/min/1.min.js'
                 sh 'pwd'
                 sh 'npm bin -g'
                 sh 'npm list -g'
             }
          }     
          stage('compression') {         
             parallel {
                stage('uglyfyjs') {
                    steps {
                       sh 'uglifyjs www/js/materialize.js -o www/min/1.min.js'
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
