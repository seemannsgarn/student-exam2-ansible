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
        stage("ansible deploy app") {
            steps {
                ansiblePlaybook( 
                playbook: 'deploy_flask_app.yml',
                inventory: 'hosts.ini', 
                credentialsId: 'ssh-key-ansible')
            }
        }
        stage("check"){
            steps {
                sh '''if [ $(curl -LI http://google.com -o /dev/null -w '%{http_code}\n' -s) == "200" ]; then 
                        echo 0; 
                      fi'''
            }
        }
    
    }
}
