pipeline {
    agent any
    
    environment {
        IMAGE_TAG = "${BUILD_NUMBER}"
    }
    
    stages {
        stage('Checkout') {
            steps {
                git credentialsId: '184b2aa9-6a9a-418f-aca3-11268b2abda8', 
                url: 'https://github.com/Shree1434/cicd-end-to-end-1.git',
                branch: 'main'
            }
        }

        stage('Build Docker') {
            steps {
                script {
                    sh '''
                    echo 'Build Docker Image'
                    docker build -t shree1434/cicd-e2e:${BUILD_NUMBER} .
                    '''
                }
            }
        }

        stage('Push the artifacts') {
            steps {
                script {
                    sh '''
                    echo 'Push to Repo'
                    docker push shree1434/cicd-e2e:${BUILD_NUMBER}
                    '''
                }
            }
        }
        
        stage('Deploy to Docker') {
            steps {
                script {
                    sh '''
                    echo 'Deploying to Docker'
                    docker stop my-app || true
                    docker rm my-app || true
                    docker run -d --name my-app -p 8000:8000 shree1434/cicd-e2e:${BUILD_NUMBER}
                    '''
                }
            }
        }
    }
}
