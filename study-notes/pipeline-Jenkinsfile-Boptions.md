Jenkinsfile'daki options bölümü, pipeline'ın genel davranışını ve ayarlarını yapılandırmak için kullanılır. Bu bölüm, pipeline'ın nasıl çalışacağını, zaman aşımı sürelerini, build tutma politikalarını ve diğer genel özellikleri belirler. options bölümü, Declarative Pipeline yapısında kullanılır ve pipeline'ın başında tanımlanır.

``` groovy
pipeline {
    agent any

    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: "", artifactNumToKeepStr: "", daysToKeepStr: "30", numToKeepStr: "2")
    }

    stages {
        stage("Hello") {
            steps {
                echo "Hello World"
            }
        }
    }
}