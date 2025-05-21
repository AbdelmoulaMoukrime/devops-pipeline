pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-python-app'
    }

    stages {
        stage('Build') {
            steps {
                bat "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Test') {
            steps {
                bat 'echo "Tests ici (optionnel)"'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'DOCKER_HUB_CREDENTIALS', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    bat "docker login -u %DOCKER_USERNAME% -p %DOCKER_PASSWORD%"
                    bat "docker tag ${IMAGE_NAME} $DOCKER_USERNAME/${IMAGE_NAME}:latest"
                    bat "docker push $DOCKER_USERNAME/${IMAGE_NAME}:latest"
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Déploiement ici...'
            }
        }
    }
}
