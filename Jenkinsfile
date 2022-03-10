pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('viveky255-docker-hub')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/viveky255/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t viveky255/sampleproject-war:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push viveky255/sampleproject-war:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

