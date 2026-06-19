pipeline {
    agent any
    environment {
        IMAGE     = 'fastapi-poc'
        CONTAINER = 'fastapi-poc'
    }
    stages {
        stage('Checkout') {
            steps { checkout scm }
        }
        stage('Build') {
            steps {
                sh 'docker build -t $IMAGE:$BUILD_NUMBER -t $IMAGE:latest .'
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                    docker rm -f $CONTAINER || true
                    docker run -d --name $CONTAINER -p 8000:8000 $IMAGE:latest
                '''
            }
        }
    }
}