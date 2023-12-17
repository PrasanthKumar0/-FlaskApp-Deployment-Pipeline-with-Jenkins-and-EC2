pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/PrasanthKumar0/FlaskApp-Deployment-Pipeline-with-Jenkins-and-EC2.git'
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    // Build the Docker image
                    sh "docker build . --file Dockerfile --tag docker.io/prasanthk8/python-webapp:latest"
                }
            }
        }
        stage('Docker Push') {
            steps {
                script {
                    // Push the Docker image to the registry
                    withDockerRegistry(credentialsId: 'DockerCred', toolName: 'docker') {
                        sh "docker push docker.io/prasanthk8/python-webapp:latest"
                    }
                }
            }
        }
        stage('Docker Deploy') {
            steps {
                script {
                    // Run the Docker container
                    withDockerRegistry(credentialsId: 'DockerCred', toolName: 'docker') {
                        sh "docker run -d -it -p 5000:5000 --name FlaskApp prasanthk8/python-webapp:latest"
                    }
                }
            }
        }
    }
}
