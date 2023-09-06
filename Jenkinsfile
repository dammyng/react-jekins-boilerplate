pipeline {
    agent any
    stages {
        stage('Building Docker Image') {
            steps {
                script {
                    echo 'Building Docker Image'
                    sh 'docker build -t <image name>:<image tag> .'
                }
            }
        }

        stage('Pushing to Docker Hub') {
            steps {
                script {
                    echo 'Pushing the Image to Docker Hub'
                    sh 'docker push <image-name>:<image-tag>'
                }
            }
        }

        stage('Deploying to Remote Server') {
            steps {
                script {
                    echo 'Deploying the application to Remote server'
                    def dockerCmd = 'docker run -p 3000:3000 -d <image name>:<image tag>'
                    sshagent(['credential_id']) {
                      sh "ssh -o StrictHostKeyChecking=no <remote-server-username>@<remote-server-IP> ${dockerCmd}"
                   }
                }
            }
        }
    }
}