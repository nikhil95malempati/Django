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
                withCredentials([usernamePassword(credentialsId: 'd0a1f0d1-d988-4519-9391-886b74bbb920', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                script {
                    sh '''
                    echo 'Build Docker Image'
                    docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
                    docker build -t nikhil3267/todoapp:${IMAGE_TAG} .
                    '''
                     }
                }
            }
        }


        stage('Push the artifacts') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'd0a1f0d1-d988-4519-9391-886b74bbb920', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh '''
                        echo 'Push to Repo'
                        docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
                        docker push nikhil3267/todoapp:${IMAGE_TAG}
                        '''
                    }
                }
            }
        }
        stage('Checkout K8S manifest SCM'){
            steps {
                git branch: 'main',
                url: 'https://github.com/nikhil95malempati/k8s-cicd-yaml.git'
                
            }
        }
        
        stage('Update K8S manifest & push to Repo'){
            steps {
                script{
                    withCredentials([string(credentialsId: '4f7a06f4-3a7a-45e6-9e6c-5ac270d7c79a', variable: 'gittoken')]) {
                        sh '''
                        cat django/deploy.yaml
                        sed -i "s|image: nikhil3267/todoapp:.*|image: nikhil3267/todoapp:${IMAGE_TAG}|g" django/deploy.yaml
                        cat django/deploy.yaml
                        git add django/deploy.yaml
                        git commit -m 'Updated the deploy yaml | Jenkins Pipeline'
                        git remote -v
                        git push  https://${gittoken}@github.com/nikhil95malempati/k8s-cicd-yaml.git HEAD:main
                        '''                        
                    }
                }
            }
        }
    }
    
    //sed -i "s/replaceImageTag/${BUILD_NUMBER}/g" django/deploy.yaml
}
