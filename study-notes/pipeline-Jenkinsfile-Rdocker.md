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
        dockerhub_cred = credentials("DOCKERHUB_AUTH")
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
                sh "docker build -t davidmashadow/addressbook:1.0 ."
            }
        }
        stage("Dockerhub push") {
            steps {
                sh "echo $dockerhub_cred_PSW | docker login -u $dockerhub_cred_USR --password-stdin"
                sh "docker push davidmashadow/addressbook:1.0"
            }
        }
        stage("Docker run") {
            steps {
                sh "docker run -d -p 80:8080 --name add davidmashadow/addressbook:1.0"
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
