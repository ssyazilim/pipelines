Built-in Variables (Yerleşik Değişkenler), Jenkins ve Jenkins Pipeline'larında otomatik olarak tanımlanan ve kullanıma hazır olan değişkenlerdir. Bu değişkenler, pipeline'ın çalışma süreciyle ilgili bilgilere erişmek, ortam ayarlarını yönetmek veya iş akışını özelleştirmek için kullanılır. Built-in variables, Jenkinsfile veya script'ler içinde doğrudan kullanılabilir.

``` groovy
pipeline {
    agent any
    
    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: "", artifactNumToKeepStr: "", daysToKeepStr: "30", numToKeepStr: "2")
    }

    stages {
        stage("Built in variables") {
            steps {
                echo "Job number : ${env.BUILD_NUMBER}"
                echo "Job name : ${env.JOB_NAME}"
            }
        }
    }
}
