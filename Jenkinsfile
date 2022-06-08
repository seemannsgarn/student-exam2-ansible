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
                sh 'if [ $(curl -LI 192.168.56.3:5100 -o /dev/null -w \'%{http_code}\n\' -s) == "200" ]; then echo 0; fi'
            }
            echo "DONE"
        }
    
    }
}
