pipeline {
    agent any

    environment {
        IMAGE_NAME = 'nodejs-docker-app'
        CONTAINER_NAME = 'nodejs-docker-container'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                    docker rm -f $CONTAINER_NAME || true
                    docker run -d --name $CONTAINER_NAME -p 3000:3000 $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully. Node.js Docker container is running on port 3000.'
        }

        failure {
            echo 'Pipeline failed. Check the console output for errors.'
        }
    }
}
