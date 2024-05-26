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
                    echo 'Build Docker Image'
                    
                    '''
                }
            }
        }
        // stage('Build Docker') {
        //     steps {
        //         script {
        //             sh '''
        //             echo 'Build Docker Image'
        //             docker build -t nikhil3267/todoapp:${IMAGE_TAG} .
        //             '''
        //         }
        //     }
        // }

        // stage('Push the artifacts') {
        //     steps {
        //         script {
        //             withCredentials([usernamePassword(credentialsId: 'd0a1f0d1-d988-4519-9391-886b74bbb920', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
        //                 sh '''
        //                 echo 'Push to Repo'
        //                 docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
        //                 docker push nikhil3267/todoapp:${IMAGE_TAG}
        //                 '''
        //             }
        //         }
        //     }
        // }
    }
}
