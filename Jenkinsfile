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
        
        stage('Checkout K8S manifest SCM') {
            steps {
                git credentialsId: '184b2aa9-6a9a-418f-aca3-11268b2abda8', 
                url: 'https://github.com/Shree1434/cicd-end-to-end-1.git',
                branch: 'main'
            }
        }
        
        stage('Update K8S manifest & push to Repo') {
            steps {
                script {
                    // Navigate to the directory containing the Kubernetes manifest file
                    dir('deploy/') {
                        // Perform the substitution operation using sed
                        sh '''
                        cat deploy.yaml
                        sed -i 's/32/18/g' deploy.yaml
                        cat deploy.yaml
                        '''
                    }
                }
            }
        }
    }
}

