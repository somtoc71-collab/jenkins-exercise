pipeline {
    agent any
    parameters {
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: 'select a version to deploy')
        booleanparam(name: 'executeTests', defaultvalue: true, description: 'execute tests during deployment')

    }
    stages {
        stage("build") {

            steps {
                echo 'building the application'
            }
        }

        stage("test") {
            when {
                expression { 
                    params.executeTests == true
                }
            }
            steps {
                echo 'testing the application..' 
            }
        } 

        stage("deploy") {
            steps {
                echo 'deploying the aplication..'
                echo "deploying version ${params.VERSION}"
               }
        }         
               
    }//
}

