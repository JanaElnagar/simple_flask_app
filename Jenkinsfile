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
                   // docker.build("janaessam/simple_flask")
                    image = docker.build("janaessam/simple_flask")
	            image.tag("janaessam/simple_flask:0.2")
                }
            }
        }
        stage('Security scans using Trivy') {
            steps {
                script {
                    sh 'trivy image simple_flask:0.2'
                }
            }
        }
        stage('Upload image to Dockerhub') {
            steps {
                script {
                    docker.withRegistry("https://index.docker.io/v1/", registryCredential) {
                        docker.image('janaessam/simple_flask:0.2').push()
                    }
                }
            }
        }
        
    }
}
