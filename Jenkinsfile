pipeline {
    agent any 
    parameters {
        // choice (name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'],  description:'')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }
    stages {
        stage ("build") {
            steps {
                echo 'building the application...'
            }
        }
        stage ("test") {
            when {
                expression {
                    params.executeTests
                }
            }
            steps {
                echo 'testing the application...'
            }
        }
        stage ("deploy") {
            input{
                message "select the environment to deploy to"
                ok "Done"
                parameters{
                    choice(name: 'ENV', choices: ['dev', 'staging', 'prod', description: ''])
                }
            }
            steps {
                echo 'deploying the application...'
                echo "deploying version ${ENV}"
            }
        }
    }
}