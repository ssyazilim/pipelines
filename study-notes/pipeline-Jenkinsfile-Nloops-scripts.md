Jenkinsfile, Jenkins'te Pipeline'ları tanımlamak için kullanılan bir script dosyasıdır. Bu dosya, projenizin build, test, deploy gibi süreçlerini otomatikleştirmek için adımları (stages) ve bu adımlarda gerçekleştirilecek işlemleri (steps) tanımlar. Jenkinsfile, genellikle Groovy tabanlı bir sözdizimi (syntax) kullanır ve projenizin kaynak kod deposunda (örneğin, Git) saklanır.

``` groovy
pipeline {
    agent any

    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: "", artifactNumToKeepStr: "", daysToKeepStr: "30", numToKeepStr: "2")
    }

    stages {
        stage("Checkout stage") {
            steps {
                checkout scmGit(branches: [[name: "*/main"]], extensions: [], userRemoteConfigs: [[url: "https://github.com/ssyazilim/pipelines.git"]])
            }
        }
        stage("Script usage") {
            script {
                def values = ["uat", "dev", "prod"]
                sh "chmod +x hello-world.sh"
                for (name in values) {
                    sh "sh hello-world.sh ${name}"
                }
            }
        }
    }
}