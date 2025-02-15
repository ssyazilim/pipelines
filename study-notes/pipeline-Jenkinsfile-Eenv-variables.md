Jenkinsfile içerisindeki environment bölümü, Jenkins pipeline'larında kullanılan ortam değişkenlerini tanımlamak için kullanılır. Bu bölüm, pipeline'ın çalışma ortamını yapılandırmak ve belirli değerleri her adımda (stage) veya pipeline genelinde kullanabilmek için oldukça faydalıdır.

``` groovy
pipeline {
    agent any

    environment {
        NAME = "Erol"
    }

    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: "", artifactNumToKeepStr: "", daysToKeepStr: "30", numToKeepStr: "2")
    }

    stages {
        stage("Usage of ENV variables") {
            steps {
                echo "My name is ${env.NAME}"
            }
        }
    }
}
