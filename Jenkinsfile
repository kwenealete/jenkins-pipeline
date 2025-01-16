#!/user/bin/env groovy

library identifier: 'jenkins-shared-library@master', retriever: modernSCM(
        [$class: 'GitSCMSource',
        remote: 'https://github.com/kwenealete/jenkins-shared-library.git',
        credentials: 'github-credentials'])
def gv

pipeline {
    agent any 
    tools {
        maven 'maven-3.9'
    }
    
    stages {
        stage ("init for webhook") {
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