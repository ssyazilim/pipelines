Jenkinsfile, Jenkins'te pipeline'ları tanımlamak için kullanılan bir dosyadır. Bu dosya, genellikle Groovy tabanlı bir sözdizimi kullanır ve projenizin build, test ve deploy gibi adımlarını otomatikleştirir.

pipeline {
    agent any
    stages {
        stage('Build stage') {
            steps {
                echo "This is a Build stage"
            }
        }
        stage('Test stage') {
            steps {
                echo "This is a Test stage"
            }
        }
        stage('Deploy stage') {
            steps {
                echo "This is a Deploy stage"
            }
        }
    }
}