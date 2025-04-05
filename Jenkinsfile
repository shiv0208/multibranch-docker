pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t image1 .'
            }
        }
        stage ("Tag") {
            steps {
                sh 'docker tag image1 shiv0208/paytm:bank'
            }
        }
        stage ("Push") {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockerhub') {
                        sh 'docker push shiv0208/paytm:bank'
                    }
                }
            }
        }
        stage ("Deploy") {
            steps {
                sh '''
        docker stop bank-app || true
        docker rm bank-app || true
        docker run -itd --name bank-app -p 1111:80 shiv0208/paytm:bank
        '''
            }
        }
    }
}
