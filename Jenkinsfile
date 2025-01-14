#!/user/bin/env groovy

@Library('jenkins-shared-library')
def gv

pipeline {
    agent any 
    tools {
        maven 'maven-3.9'
    }
    
    stages {
        stage ("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage ("build jar") {
            steps {
                script{
                   buildJar()
                }
            }
        }
        stage ("build and push image") {
            
            steps {
                script {
                    buildImage 'monyakwene/demo-app:jma-4.0'
                    dockerLogin()
                    dockerPush 'monyakwene/demo-app:jma-4.0'
                }
            }
        }
        stage ("deploy") {
            
            steps {
                script {
                     gv.deployApp()
                }
            }
        }
    }
}