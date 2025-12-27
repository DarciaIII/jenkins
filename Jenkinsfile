// Jenkinsfile
pipeline {
    agent any

    environment {
        APP_IMAGE = "flask-hello:${BUILD_NUMBER}"
        CONTAINER_NAME = "flask-app"
    }

    stages {
        stage('Clone & Prepare') {
            steps {
                checkout scm  // клонирует текущий репозиторий
            }
        }

        stage('Build App Image') {
            steps {
                script {
                    sh 'docker build -t ${APP_IMAGE} .'
                }
            }
        }

        stage('Stop Old Container') {
            steps {
                script {
                    sh 'docker stop ${CONTAINER_NAME} || true'
                    sh 'docker rm ${CONTAINER_NAME} || true'
                }
            }
        }

        stage('Run App') {
            steps {
                script {
                    sh 'docker run -d --name ${CONTAINER_NAME} -p 5000:5000 ${APP_IMAGE}'
                }
            }
        }
    }

    post {
        success {
            echo "✅ Приложение запущено на порту 5000"
        }
    }
}
