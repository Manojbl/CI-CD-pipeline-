pipeline {
    agent any

    environment {
        CONTAINER_NAME = "student-management-app"
        IMAGE_NAME = "student-management-app"
        EMAIL = "manojshaiva555@gmail.com"
        PORT = "3000"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/Manojbl/CI-CD-pipeline-.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME'
            }
        }
        stage('Stop & Remove previous Container') {
            steps {
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                '''
            }
        }
        stage('Run Docker Container') {
            steps {
                sh '''
                    docker run -d -p ${PORT}:${PORT} --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
        stage('SEND EMAIL NOTIFICATION') {
            steps {
                emailtext{
                    subject : "Student Management App Deployment Successful",
                    body : "The Docker container for the student management app has been successfully built and deployed  http://16.171.40.235:${PORT}/",
                    to : "${EMAIL}"
                }
            }
        }
    }
}