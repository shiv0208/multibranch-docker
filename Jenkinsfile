pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t image3 .'
            }
        }
        stage ("Tag") {
            steps {
                sh 'docker tag image3 shiv0208/paytm:movie'
            }
        }
        stage ("Push") {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockerhub') {
                        sh 'docker push shiv0208/paytm:movie'
                    }
                }
            }
        }
        stage ("Deploy") {
            steps {
                sh '''
            docker rm -f movie-app || true
            docker run -itd --name movie-app -p 3333:80 shiv0208/paytm:movie
        '''
            }
        }
    }
}
