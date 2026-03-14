pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "jovany971/my-python-app"
    }

    stages {
        stage("Clone") {
            steps {
                checkout scm
            }
        }
        stage("Tests") {
            steps {
                sh "pip3 install pytest --break-system-packages"
                sh "python3 -m pytest test_app.py -v"
            }
        }
        stage("Build Docker Image") {
            steps {
                sh "docker build -t ${DOCKER_IMAGE}:${BUILD_NUMBER} ."
            }
        }
        stage("Push Docker Hub") {
            steps {
                withCredentials([usernamePassword(credentialsId: "dockerhub-credentials", usernameVariable: "DOCKER_USER", passwordVariable: "DOCKER_PASS")]) {
                    sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                    sh "docker push ${DOCKER_IMAGE}:${BUILD_NUMBER}"
                }
            }
        }
    }

    post {
        success { echo "Image poussee sur Docker Hub !" }
        failure { echo "Echec du pipeline !" }
    }
}