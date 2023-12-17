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
                    def dockerfilePath = '/home/ec2-user/Dockerfile'
                    def imageTag = 'docker.io/prasanthk8/python-webapp:latest'
                    
                    // Check if the Dockerfile exists
                    if (fileExists(dockerfilePath)) {
                        // Check if the directory exists, create if not
                        dir('/home/ec2-user') {
                            // Build the Docker image
                            sh "docker build . --file $dockerfilePath --tag $imageTag"
                        }
                    } else {
                        error "Dockerfile not found at $dockerfilePath"
                    }
                }
            }
        }
        // Add your Docker Push and Docker Deploy stages here...
    }
}
