pipeline {
    environment {
        registry = "janaessam/simpleflask2"
        registryCredential = 'dockerhub'
    }
    agent any
    stages {
        stage('Security Test') {
            steps {
                echo 'Testing...'
            }
        }
        stage('Create Docker Image') {
            steps {
                script {
                    docker.build("janaessam/simple_flask:latest")
                }
            }
        }
        stage('Security scans using Trivy') {
            steps {
                script {
                    sh 'trivy image simple_flask:latest'
                }
            }
        }
        stage('Upload image to Dockerhub') {
            steps {
                script {
                    docker.withRegistry("https://index.docker.io/v1/", registryCredential) {
                        docker.image('janaessam/simple_flask:latest').push()
                    }
                }
            }
        }
    }
}
