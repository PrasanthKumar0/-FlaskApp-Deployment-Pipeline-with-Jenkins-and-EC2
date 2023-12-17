pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/PrasanthKumar0/FlaskApp-Deployment-Pipeline-with-Jenkins-and-EC2.git'
            }
        }
        stage('Docker Pull') {
            steps {
                script {
                    // Pull the Docker image from Docker Hub
                    withDockerRegistry(credentialsId: 'DockerCred', toolName: 'docker') {
                        sh "docker pull docker.io/prasanthk8/python-webapp:latest"
                    }
                }
            }
        }
        stage('Docker Deploy') {
            steps {
                script {
                    // Run the Docker container
                    sh "docker run -d -it -p 5000:5000 --name FlaskApp prasanthk8/python-webapp:latest"
                }
            }
        }
    }
}
