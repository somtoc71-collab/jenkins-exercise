pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage("build jar") {
            steps {
                script {
                    echo "building the application.."
                    sh 'mvn package'
                }
            }
          stage("build image") {
            steps {
                script {
                    echo "building the image.."
                    withCredentials([usernamePassword(credentialsId:'docker-hub-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) 
                     sh 'docker build -t bamzy14/my-repo:jma-2.0 .'
                     sh "echo $PASSWORD | docker login -u $USERNAME --password-stdin"
                     sh  'docker push bamzy14/my-repo:jma-2.0'  
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

