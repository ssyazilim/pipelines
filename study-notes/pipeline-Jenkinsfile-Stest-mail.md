``` groovy
pipeline {
    agent any

    stages {
        stage("Test mail") {
            steps {
                echo "Hello World"
            }
        }
    }
    post {
        always {
            emailext body: "Job is completed", subject: "Job status", to: "ckkykoks@sharklasers.com"
        }
    }
}
