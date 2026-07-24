#!/usr/bin/env groovy
@Library('jenkins-shared-library') _
pipeline {
    agent any
    tools {
     maven  'maven 3.9'
    }  
    stages {
        stage("init") {
            steps {
                script {
                    echo "initializing pipeline.."
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
                    def gv = load "script.groovy"
                    gv.deployapp()
                }
            
            }
        }         
               
    }
}



