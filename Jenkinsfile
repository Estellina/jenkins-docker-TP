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
        stage('Login to DockerHub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'estelle-dockerhub', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                        bat 'docker login -u %DOCKER_USERNAME% -p %DOCKER_PASSWORD%'
                    }
                }
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
