pipeline {
    agent any
    options {
        timestamps()
        disableConcurrentBuilds()
    }
    stages {
        stage('Checkout code'){
            steps{
                script{
                    codeCo = checkout scm:[
                                $class: 'GitSCM',
                                poll: true,
                                branches: [[
                                    name: "*/master"
                                ]],
                                userRemoteConfigs: [[
                                    credentialsId: '',
                                    url: "https://github.com/h4rdL1nk/ansible"
                                ]]
                            ]
                }
            }
        }
        stage('Role check'){
            steps{
                    sh script: """
                        virtualenv -p /usr/bin/python2.7 .venv
                        source .venv/bin/activate
                        pip install -r requirements.txt
                        cd roles/elasticsearch
                        molecule create
                    """

                    sh script: """
                        molecule converge
                    """
            }
        }
    }
    post{
        always{
            deleteDir()
        }
    }
}