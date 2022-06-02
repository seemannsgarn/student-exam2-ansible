#!#!groovy

properties([disableConcurrentBuilds()])

pipeline {
    agent {
        label 'slave-1'
    }
    triggers {pollSCM('* * * * *')}
    options {
        buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '10'))
        timestamps()
    }
    stages {
       stage("check connect") {
            steps {
                echo " ============== check connect =================="
                    sh 'ansible all -m ping'
            }
        }
    }
}
