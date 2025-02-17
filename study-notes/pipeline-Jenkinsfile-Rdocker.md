``` groovy
pipeline {
    agent any
    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: "", artifactNumToKeepStr: "", daysToKeepStr: "30", numToKeepStr: "2")
    }
    tools {
        maven "Maven"
    }
    environment {
        DOCKER_AUTH = credentials("DOCKERHUB_AUTH")
        DOCKER_IMAGE = "davidmashadow:addressbook"
        DOCKER_TAG = "$BUILD_NUMBER"
    }
    stages {
        stage("Checkout") {
            steps {
                checkout scmGit(branches: [[name: "*/master"]], extensions: [], userRemoteConfigs: [[url: "https://github.com/DevopsWorking/addressbook.git"]])
            }
        }
        stage("Maven build") {
            steps {
                sh "mvn package -DskipTests"
            }
        }
        stage("Docker build") {
            steps {
                sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
            }
        }
        stage("DockerHub push") {
            steps {
                sh "echo $DOCKER_AUTH_PSW | docker login -u $DOCKER_AUTH_USR --password-stdin"
                sh "docker push ${DOCKER_IMAGE}:${DOCKER_TAG}"
                sh "docker tag ${DOCKER_IMAGE}:${DOCKER_TAG} ${DOCKER_IMAGE}:latest"
                sh "docker push ${DOCKER_IMAGE}:latest"
            }
        }
        stage("Docker run") {
            steps {
                sh "docker run -d -p 80:8080 --name addressbook ${DOCKER_IMAGE}:latest"
            }
        }
    }
    post {
        always {
            echo "Job is completed"
        }
        success {
            echo "It is a success"
        }
        failure {
            echo "It has failed"
        }
    }
}
