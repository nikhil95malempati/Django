pipeline {
    agent any

    environment {
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/nikhil95malempati/Django.git'
            }
        }

        stage('Build Docker') {
            steps {
                script {
                    sh '''
                    echo 'Buid Docker Image'
                    docker build -t nikhil3267/todoapp:${BUILD_NUMBER} .
                    '''
                }
            }
        }

        stage('Push the artifacts'){
           steps{
                script{
                    withCredentials([usernamePassword(credentialsId: 'dad507a0-be23-40e2-a37e-3308399e7c71', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh '''
                    echo 'Push to Repo'
                    docker push nikhil3267/todoapp:${BUILD_NUMBER}
                    '''
                    }
                }
            }
        }
    }
}
