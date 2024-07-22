pipeline {
    agent any 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('estelle-dockerhub')
    }
    stages { 
        stage('Build docker image') {
            steps {
                bat 'docker build -t thecatalyst112/flaskapp:%BUILD_NUMBER% .'
            }
        }
       stage('login to dockerhub') {
            steps{
                bat 'echo  Campusfrance1*  | docker login -u thecatalyst112 --password-stdin'
            }
        }
        stage('Push image') {
            steps {
                bat 'docker push thecatalyst112/flaskapp:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}
