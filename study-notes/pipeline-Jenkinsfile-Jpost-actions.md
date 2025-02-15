Post Actions, Jenkins'te bir iş (job) veya pipeline aşaması (stage) tamamlandıktan sonra çalıştırılan adımlardır. Bu adımlar, işin sonucuna (başarılı, başarısız, kararsız, vb.) bağlı olarak belirli eylemler gerçekleştirmek için kullanılır. Post Actions, genellikle temizlik, bildirim gönderme, sonuçları raporlama veya başka işleri tetikleme gibi görevler için kullanılır.

``` groovy
pipeline {
    agent any
    
    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: "", artifactNumToKeepStr: "", daysToKeepStr: "30", numToKeepStr: "2")
    }

    stages {
        stage("First Stage") {
            steps {
                echo "Hello world"
            }
        }
    }

    post {
        always {
            echo "Job is completed"
        }
        success {
            echo "It is a Success"
        }
        failure {
            echo "It is a Failure"
        }
    }
}
