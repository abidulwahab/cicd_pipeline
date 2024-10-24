pipeline {
    agent any 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('abiddockerhub')
    }
    stages { 

        stage('Build docker image') {
            steps {  
                sh 'docker build -t abiddockerhub/flaskapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push abiddockerhub/flaskapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
