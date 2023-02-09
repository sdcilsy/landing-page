pipeline {
    agent any
    environment {
        DOCKER_HUB_REPO = "mydocker1907"
    }
    stages {
        stage("Checkout code") {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'fatkhurrozaq', url: 'https://github.com/fatkhurrozaq/landing-page.git']]])
            }
        }
        stage("Build Docker Image") {
            steps {
                script {
                    def dockerImage = docker.build("$mydocker1907:$1")
                }
            }
        }
        stage("Push Docker Image") {
            steps {
                script {
                    docker.withRegistry("https://index.docker.io/v1/", "mydocker1907") {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
