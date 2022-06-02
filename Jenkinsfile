#!groovy
// Check ub1 properties
properties([disableConcurrentBuilds()])

pipeline {
    agent { 
        label 'master'
        }
    triggers {pollSCM('* * * * *')}
    options {
        buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '10'))
        timestamps()
    }
    stages {
       stage("ansible ver") {
            steps {
                echo " ============== ansible ver =================="
                    sh 'pwd'
                    sh 'ls -lh'
                    sh 'ansible --version'
                }
            }
        }
    }
