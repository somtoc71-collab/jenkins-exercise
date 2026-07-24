#!/usr/bin/env groovy
@library('jenkins-shared-library') _
def gv
pipeline {
    agent any
    tools {
     maven  'maven 3.9'
    }  
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage("build jar") {
            steps {
                script {
                   buildjar()
                }
            }

        }
        stage("build image") {
            steps {
                script {
                    buildimage()
                }
            
            }
        } 
        stage("deploy") {
            steps {
                script {
                    gv.deployapp()
                }
            
            }
        }         
               
    }
}



