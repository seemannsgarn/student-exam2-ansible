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
        stage("ansible") {
            steps {
                ansiblePlaybook( 
                playbook: 'playbooks/deploy_flask_app.yml',
                inventory: 'hosts.ini', 
                credentialsId: 'ssh-key-ansible')
            }
        }
        stage("check"){
            steps {
                echo "###################################"
                echo "#                OK               #"
                echo "###################################"
            }
        }
    
    }
}
