def gv

pipeline {
    agent any
    parameters {
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: 'select a version to deploy')
        booleanParam(name: 'executeTests', defaultValue: true, description: 'execute tests during deployment')

    }
    stages {
        stage(init) {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }

        }
        stage("build") {
            steps {
                script {
                    gv.buildapp()
                }
            
            }
        }

        stage("test") {
            when {
                expression { 
                    params.executeTests == true
                }
            }
            steps {
                script {
                    gv.testapp()
                }
            
            }
        } 

        stage("deploy") {
            input {
                message "select the environment to deploy to"
                ok "done"
                parameters {
                    choice(name: 'env', choices: ['dev', 'staging', 'prod'], description: 'select a version to deploy')
                }
            }
            steps {
                script {
                    gv.deployapp()
                    echo "deploying to ${params.env}"
                }
            
            }
        }         
               
    }//
}

