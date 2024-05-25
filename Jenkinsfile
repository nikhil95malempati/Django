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
                    withCredentials([string(credentialsId: 'a07a9776-beca-466f-8460-0bf795427ced', variable: 'DOCKER_TOKEN')]) {
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

//a07a9776-beca-466f-8460-0bf795427ced - nikhil32673