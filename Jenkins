pipeline {
    agent any
    environment {     
    DOCKERHUB_CREDENTIALS= credentials('dockerhub')     
  }
    stages {
        stage('github clone') {
            steps {
                echo 'code cloaning'
                git url:"https://github.com/krunal2401/cicd-project.git" , branch:"main"
            }
        }
        stage('build docker img') {
            steps {
                echo 'img building'
                sh "docker build -t krunal2401/django-app ."
            }
        }
        stage('push to dockerhub') {
            steps {
                echo 'push to docker hub'
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'                 
	                echo 'Login Completed'
	                sh "docker push $DOCKERHUB_CREDENTIALS_USR/django-app"
            }
        }
        stage('Deploy the code') {
            steps {
                echo 'deploying code'
                sh "docker-compose down && docker-compose up -d"
            }
        }
        
    }
}