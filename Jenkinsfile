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
                    withCredentials([string(credentialsId: '28c9564a-faba-440e-a778-005883cb7ae9', variable: 'DOCKER_TOKEN')]) {
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
