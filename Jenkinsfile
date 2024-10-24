pipeline {
    agent any 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('abiddockerhub')
    }
    stages { 
        stage('Build docker image') {
            steps {  
                sh 'docker build -t ylmt/flaskapp:$BUILD_NUMBER .'
            }
        }
        stage('Login to DockerHub') {
            steps {
                script {
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                sh 'docker push ylmt/flaskapp:$BUILD_NUMBER'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
