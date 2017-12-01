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
                script{
                    sh script: """
                        cd roles/elasticsearch
                        molecule create
                        molecule converge
                    """
                }
            }
        }
    }
    post{
        always{
            sh script: """
                cd roles/elasticsearch
                molecule destroy
            """
            deleteDir()
        }
    }
}